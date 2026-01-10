---
uuid: 20221023161724
created: 2022-10-23T16:17:24
alias:
- model layer
- слой модели
tags:
---

# [[Model layer]]

The model layer is responsible for all create, read, update and delete (CRUD) operations.

You can design the model layer in many different ways; yet, two of the most common are push-and-pull and observe-and-push designs:
- **Push-and-pull** designs require consumers to ask for data and wait for the response, which is the “pull” part. Consumers can also update model data and tell the model layer to send it, which is the “push” part.
- **Observe-and-push** designs require consumers to “observe” the model layer, instead of asking for data directly. Like push-and-pull designs, consumers can also update model data and tell the model layer to “push” it.

[[Repository pattern]]
Repositories contain data access objects that can call out to a server or read from disk.

The repository pattern provides a façade for networking, persistence and in-memory caching. This [[Facade pattern|façade]] creates, reads, updates and deletes data on disk and in the cloud. The repository doesn’t expose to consumers how it retrieves or stores the data.  

When combined with [[Model-View-ViewModel|MVVM]], view models use the repository façade, instead of performing these operations themselves. In turn, view models transform and expose model data to views to display on-screen.

The repository provides a set of asynchronous CRUD methods. The underlying implementations can be either stateless or stateful. Stateless implementations don’t keep data around after retrieving it, whereas stateful implementations save data for later.

Under the hood, the repository has multiple layers of data access. Each implementation of a repository may implement all or only one of these layers:

The **cloud-remote-API layer** makes calls to a server to read and update data. This may make REST calls, get data from a socket connection or another means. The data at this layer always comes from outside of the app.

The **persistent-store** layer puts data in a local database. The database can be Core Data, Realm or a Plist file on disk. The data at this layer always comes from the app. The data gets persisted after the app closes.  

The **in-memory-cache layer** stores data in objects that stay around for the lifetime of the repository. The cache doesn’t persist between app sessions. The in-memory cache is useful for showing pre-fetched data before making a network call to the cloud.![[Returns.jpeg]]

---

## 📇 Additional Metadata

- 🗂 Type:: #type/note
- ℹ️ Source:: [[Advanced iOS App Architecture]]