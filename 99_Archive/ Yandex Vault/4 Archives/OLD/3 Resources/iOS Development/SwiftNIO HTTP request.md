---
uuid: 20220905204131
created: 2022-09-05T20:41:31
alias:
- clever copy-on-write trick
---

# [[SwiftNIO HTTP request]]

We start out with an extremely simplified version of an HTTP request struct:
```swift
struct HTTPRequest {
	var path: String
	var headers: [String: String]
	// ...
}
```

To minimize the reference counting overhead we’ve outlined above, we’ll first wrap all
the properties in a private storage class:
```swift
struct HTTPRequest {
	fileprivate class Storage {
		var path: String
		var headers: [String: String]
	
		init(path: String, headers: [String: String]) {
			self.path = path
			self.headers = headers
		}
	}

	private var storage: Storage

	init(path: String, headers: [String: String]) {
		storage = Storage(path: path, headers: headers)
	}
}
```

That way, our HTTPRequest struct only contains one property, storage, and it only requires one reference count of the internal storage instance to be incremented on copy. To expose the now private path and headers properties of the internal storage instance, we add computed properties to the struct:
```swift
extension HTTPRequest {
	var path: String {
	get { return storage.path }
	set { /* to do */ }
}

	var headers: [String: String] {
		get { return storage.headers }
		set { /* to do */ }
	}
}
```

The important part is the implementation of the setters for these properties: **we should not just set the new value on the internal storage instance**, because this object is potentially shared among multiple variables.

As a first step, we can create a copy of the internal storage class every time a setter is invoked. To make a copy, we add a copy method on Storage:
```swift
extension HTTPRequest.Storage {
	func copy() -> HTTPRequest.Storage {
		print("Making a copy...") // For debugging
		return HTTPRequest.Storage(path: path, headers: headers)
	}
}
```

Then we can assign a copy of the current storage to the storage property before we set the new value:
```swift
extension HTTPRequest {
	var path: String {
		get {
			return storage.path
		}
		set {
			storage = storage.copy()
			storage.path = newValue
		}
	}

	var headers: [String: String] {
		get {
			return storage.headers
		}
		set {
			storage = storage.copy()
			storage.headers = newValue
		}
	}
}
```

However, the current implementation is still inefficient. We create a copy of the internal storage anytime we make a change, no matter if any other variable references the same storage or not:
```swift
var req = HTTPRequest(path: "/home", headers: [:])
for x in 0..<5 {
	req.headers["X-RequestId"] = "\(x)"
}
/*
Making a copy...
Making a copy...
Making a copy...
Making a copy...
Making a copy...
*/
```

Each time we mutate the request, another copy is made. All of these copies are unnecessary though; there’s only the one `HTTPRequest` value in req that references the internal storage instance.

To provide efficient [[Copy-on-Write in Swift|copy-on-write]] behavior, we need to know whether an object (the `Storage` instance in our case) is uniquely referenced, i.e. if it has a single owner. If it does, we can modify the object in place. Otherwise, we create a copy of the object before modifying it.

We can use the `isKnownUniquelyReferenced` function to find out if a reference has only one owner. If you pass in an instance of a [[Swift|swift]] class to this function, and if no one else has a strong reference to the object, the function returns `true`. If there are other strong references, it returns `false`.

Using this knowledge, we can now write a variant of `HTTPRequest` that checks whether storage is uniquely referenced before mutating it. To avoid writing these checks in every property setter, we’ll wrap the logic in a `storageForWriting` property:

```swift
extension HTTPRequest {
	private var storageForWriting: HTTPRequest.Storage {
		mutating get {
			if !isKnownUniquelyReferenced(&storage) {
				self.storage = storage.copy()
			}
			return storage
		}
	}

	var path: String {
		get { return storage.path }
		set { storageForWriting.path = newValue }
	}
	
	var headers: [String: String] {
		get { return storage.headers }
		set { storageForWriting.headers = newValue }
	}
}
```

To test out our code, let’s write the loop again:
```swift
var req = HTTPRequest(path: "/home", headers: [:])
var copy = req
for x in 0..<5 {
	req.headers["X-RequestId"] = "\(x)"
} // Making a copy...
```

---

## 📇 Additional Metadata

- 🗂 Type:: #type/note
- Source:: [[Advanced Swift]]
- 🏷️ Tags:: [[Swift]]