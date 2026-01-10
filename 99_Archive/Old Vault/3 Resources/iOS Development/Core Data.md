---
aliases: ["Core Data", "CoreData"]
---
MOC:  [[iOS Development]]

---

# Core Data Stack

Стек состоит из 4-х основных классов:
- *NSManagedObjectModel*
- *NSPersistentStore*
- *NSPersistentStoreCoordinator*
- *NSManagedObjectContext*

## NSManagedObjectModel
NSManagedObjectModel определяет тип объекта, его свойства и связи. Core Data использует модель для создания объектов, хранения свойств и сохранения данных.

В случае [[SQLite]] NSManagedObjectModel определяет схему [[Базы Данных|базы данных]].

>Note: You may be wondering how NSManagedObjectModel relates to the data model editor you’ve been using all along. Good question!
>
The visual editor creates and edits an `xcdatamodel` file. There’s a special compiler, `momc`, that compiles the model file into a set of files in a `momd` folder.
>
Just as your Swift code is compiled and optimized so it can run on a device, the compiled model can be accessed efficiently at runtime. Core Data uses the compiled contents of the `momd` folder to initialize an `NSManagedObjectModel` at runtime.

## NSPersistentStore
NSPersistentStore осуществляет чтение и запись данных. Core Data предоставляет 4 типа NSPersistentStore: 3 атомарных и 1 неатомарный:
- **NSSQLiteStoreType** - SQLite БД. Единственный неатомарный store.
- **NSXMLStoreType** - [[XML]]-файл. 
- **NSBinaryStoreType** - бинарный файл. Должен быть полностью загружен в память, прежде чем с ним можно будет работать.
- **NSInMemoryStoreType** - store в памяти устройства. Удобен для кэширование и тестирования.

Если не хватает этих store'ов, то можно сделать свой наследованием от `NSIncrementalStore`.

## NSPersistentStoreCoordinator
NSPersistentStoreCoordinator выступает мостом между NSPersistentStore и NSManagedObjectModel. 

## NSManagedObjectContext
- A context is an in-memory scratchpad for working with your managed objects.
- You do all of the work with your Core Data objects within a managed object context.
- Any changes you make won’t affect the underlying data on disk until you call `save()` on the context.

The context manages the lifecycle of the objects it creates or fetches. This lifecycle management includes powerful features such as faulting, inverse relationship handling and validation.

## NSPersistentContainer
NSPersistentContainer соединяет остальные компоненты Core Data вместе.


### Модель
> When Xcode compiles your app into its app bundle, it will also compile your data models. The app bundle will have at its root a `.momd` folder that contains `.mom `files. MOM, or Managed Object Model, files are the compiled versions of `.xcdatamodel` files. You’ll have a `.mom` for each data model version.

### Полезное
[[Копирование подготовленной базы CoreData]]