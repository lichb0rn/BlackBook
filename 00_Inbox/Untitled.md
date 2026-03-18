MongoDB Assistant
You’re right to think about this now—schema design will make a huge difference in how smooth this feels.
Given your workload:
Reads of a single Device with “full component information” are very frequent.
Creating/updating components is less frequent.
You have a global catalog (Component collection) and task-specific usage (Task, Device).
You’re essentially facing the classic “catalog + orders” / “products + order lines” problem. MongoDB’s documentation recommends patterns that optimize for reads and use denormalization with references for this.
Below is a concrete direction tailored to your case.
1. Separate concerns: catalog vs usage
You already have:
Component = global catalog
Task = task-level info
Device = device-level info
That’s good. The question is: how much of the component info do you embed into Task and Device?
There are two main patterns relevant here:
Extended Reference / Subset pattern (recommended)
Fully normalized, use $lookup for every read (not ideal for your “very frequent read” use case)
2. Recommended pattern: Extended Reference / Subset
Core idea:
Keep the authoritative, complete component document in Component collection.
Embed a subset of “display” fields (the ones you need to show the Device view/table) inside the Device document together with the component_id.
Optionally also keep a task-local list of components (similar subset) if needed for other task-level screens.
So your DeviceDoc could look like:
```go
type DeviceDoc struct {
    ID           bson.ObjectID `bson:"_id"`
    TaskID       bson.ObjectID `bson:"task_id"`
    SerialNumber string        `bson:"serial_number"`
    Components   []DeviceComponentDoc `bson:"components"`
}
type DeviceComponentDoc struct {
    ComponentID bson.ObjectID `bson:"component_id"` // reference to global catalog
    // Denormalized subset of fields you need for fast display:
    PartNumber           string   `bson:"part_number"`
    Alternatives         []string `bson:"alternative_part_numbers"`
    Description          string   `bson:"description"`
    LocalizedDescription string   `bson:"localized_description"`
    Vendor               string   `bson:"vendor"`
    ProductCategoryName  string   `bson:"product_category_name"`
    Comment              string   `bson:"comment"`
    Count int `bson:"count"`
}
```

Key points:
When you display a Device, a single findOne on devices returns everything needed for the table. No extra queries, no $lookup.
If you ever need full / authoritative details, you still have ComponentID to look up the full catalog entry in the Component collection.
You only duplicate the fields that are needed frequently in read queries.
This is exactly what the documentation calls “Extended Reference” or “Subset” pattern and is recommended when you want to reduce $lookup operations and optimize reads.
3. What about writes being “3 writes” or “2 writes”?
You observed:
Create new component: catalog + task + device = up to 3 writes.
Update component: task + device = 2 writes.
In MongoDB this is usually acceptable when:
These operations are less frequent than reads (true in your case).
There is a clear trade-off in favor of simpler, faster reads (your “most often operation”).
Some refinements that can help:
Use multi-document transactions if you need strict consistency
For example, when you create a new component and insert into both components and devices, wrap them in a transaction so either both succeed or both fail.
Be selective about what you propagate
Only propagate fields that really matter for the Device table. If MTBF or some fields are rarely shown, you can keep them only in catalog.
Asynchronous / background sync for less-critical fields
If certain catalog changes don’t need to be visible immediately in all devices, you can update Device.components asynchronously (e.g., via a job or trigger).
MongoDB’s design patterns explicitly trade a few extra writes for fewer reads / lookups and improved latency for the main screen—your case matches that.
4. Should Task also have its own components array?
Ask yourself:
Do you view or filter components at the “task” level often, independently of Devices?
Or is the main view always “Device with components”?
If most interaction is per-device, you might simplify:
Task only has high-level info + maybe list of DeviceIDs.
Components are only embedded at the Device level, with a reference to Component.
If you do have a strong “task-level components” screen (e.g., “all components planned for this task”), then you can:
Keep a Task.components array similar to Device.components but without counts (or with aggregated counts).
Still follow the same subset/extended reference idea: embed only what you need to show at the task screen.
5. Alternative: fully normalized + $lookup aggregation
For completeness:
You could keep Device.components as:
type InstalledComponentDoc struct {
    ComponentID bson.ObjectID `bson:"component_id"`
    Count       int           `bson:"count"`
}

And then every time you read a Device you run an aggregation:
pipeline := mongo.Pipeline{
    {{"$match", bson.D{{"_id", deviceID}}}},
    {{"$unwind", "$components"}},
    {{"$lookup", bson.D{
        {"from", "components"},
        {"localField", "components.component_id"},
        {"foreignField", "_id"},
        {"as", "component"},
    }}},
    // reshape to your table format
}

This keeps writes simpler (only 1 write to Device, 1 to Component), but:
Every Device read is more complex and typically slower.
You do more work on your most frequent operation, which the schema design docs recommend avoiding.
Given your description, I would not choose this as the main approach unless the component catalog changes extremely often and you cannot tolerate stale data in Device documents.
6. Concrete recommendation for your case
Make Component the authoritative catalog (your current ComponentDoc is fine).
Embed a subset of component fields in Device.components along with ComponentID (extended reference).
Decide whether you truly need Task.components; if you do, treat it similarly:
Either just keep references to ComponentIDs
Or keep a subset of fields if you need fast task-level views.
Accept the extra writes as a deliberate trade-off for fast, single-read device views.
Use transactions if you need strong consistency between catalog and device/task documents.
If you share:
A sample JSON of the Device table you need to render (columns),
How often catalog data (description, vendor, etc.) actually changes,
I can help you define an exact Go struct layout and which fields should be denormalized where.