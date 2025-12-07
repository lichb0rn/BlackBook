---
up:
  - "[[Jet Spares Go]]"
related: "[[MongoDB]]"
created: 2025-04-10
---

> [!QUOTE]
> I am writing a web application in go with mongodb as a database.
> It's main purpose - to calculate spares parts for different hardware (servers, storage systems, switches and so on).
> 
> The process looks like so:
> 1. Engineer creates a calculation task.
> 2. Engineer adds to the task device configurations
> 3. Engineer adds to the device configurations components and their quantities.
> 
> Device could be the same model, but different in serial numbers, or completely different hardware. Devices could share components (hard drives can be placed in different storage systems or servers).
> 
> Calculation is based on the term (12 months, 24 months or else). Each calculation task is given to an engineer with defined terms. It could be 12 months, or 12 + 24 months, or more.
> 
> I think of these properties. 
> Calculation task:
> - task number
> - terms (a collection of some sort)
> - title (for ease of distinction)
> 
> Device Configuration:
> - serial number
> - model name
> - vendor
> - device type (server, storage, switch, etc
> - device components with count in the device (collection of some sort)
> 
> Component:
> - part number
> - alternative part numbers (collection of some sort)
> - description
> - vendor
> - comment
> - product category (business specific thing used for calculation)
> 
> Engineer can change task number, terms and title for the task. He also is able to edit device configuration properties, add or remove device components. 
> Engineer can add new components to the database, edit their properties.
> 
> Upon add/remove device configuration or device component the app should recalculation spares.
> 
> From all these points suggest a mongodb document schema. Use the best practices for working with mongodb.

## Response

Since **configurations are always accessed via a task** and **each calculation is handled by one engineer**, embedding them makes sense for performance reasons.

---

**Final MongoDB Schema**

  

This version optimizes for queries where engineers work on tasks and calculations without unnecessary lookups.

  

**1. Calculation Tasks Collection (calculation_tasks)**

```
{
  "_id": ObjectId(),
  "task_number": "TASK-001",
  "title": "Storage System Spare Parts Calculation",
  "terms": [12, 24], 
  "device_configurations": [
    {
      "serial_number": "SN123456",
      "model_name": "PowerEdge R750",
      "vendor": "Dell",
      "device_type": "server",
      "device_components": [
        { "component_id": ObjectId("..."), "quantity": 4 },
        { "component_id": ObjectId("..."), "quantity": 2 }
      ]
    }
  ],
  "calculations": [
    {
      "term": 12,
      "engineer_id": ObjectId("..."),
      "timestamp": ISODate("2025-04-10T12:00:00Z"),
      "spares": [
        { "component_id": ObjectId("..."), "quantity": 5 },
        { "component_id": ObjectId("..."), "quantity": 3 }
      ],
      "comment": "Initial estimate"
    },
    {
      "term": 12,
      "engineer_id": ObjectId("..."),
      "timestamp": ISODate("2025-04-11T14:30:00Z"),
      "spares": [
        { "component_id": ObjectId("..."), "quantity": 6 }
      ],
      "comment": "Alternative proposal"
    }
  ],
  "created_at": ISODate("2025-04-10T12:00:00Z"),
  "updated_at": ISODate("2025-04-10T12:00:00Z")
}
```

  

---

**Why This Works Well**

  

**✅ Embeds Data That is Accessed Together**

• Engineers work **within tasks**, so embedding configurations avoids extra queries.

• Calculations **belong to a task**, so they’re stored within it.

  

**✅ Supports Multiple Alternative Calculations per Term**

• Each calculation has:

• term: Defines the calculation period.

• engineer_id: Identifies the engineer who made it.

• timestamp: Differentiates calculations for the same term.

• comment: Provides reasoning for changes.

  

**✅ Efficient Queries**

1. **Find a task and its configurations + calculations**

```
db.calculation_tasks.findOne({ task_number: "TASK-001" });
```

• **Fast** because all data is embedded.

  

2. **Get latest calculation for a term**

```
db.calculation_tasks.aggregate([
  { $match: { task_number: "TASK-001" } },
  { $unwind: "$calculations" },
  { $match: { "calculations.term": 12 } },
  { $sort: { "calculations.timestamp": -1 } },
  { $limit: 1 }
]);
```

• **Efficient** since we filter within the document.

---

**Alternative Approach: Separate calculations Collection**

  

If tasks become **too large**, we can split calculations:

```
{
  "_id": ObjectId(),
  "task_id": ObjectId("..."),
  "term": 12,
  "engineer_id": ObjectId("..."),
  "timestamp": ISODate("2025-04-10T12:00:00Z"),
  "spares": [
    { "component_id": ObjectId("..."), "quantity": 5 },
    { "component_id": ObjectId("..."), "quantity": 3 }
  ],
  "comment": "Initial estimate"
}
```

• This allows **faster writes and history tracking**.

• But it requires **joins** (using $lookup).

---

**Final Recommendation**

• **Keep calculations embedded** unless they grow too large.

• **Embed device configurations** within tasks since they’re always accessed together.

• **Keep components as separate documents** for reuse.

  

Would you like a specific indexing strategy to optimize queries?

