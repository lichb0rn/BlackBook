---
uuid: 20220916164042
created: 2022-09-16T16:40:42
alias:
---

# [[Resource struct]]

Because a URL and the parse function to decode the data returned from that URL naturally belong together, it makes sense to group them together in a `Resource` [[Swift Structures|struct]]

```swift
struct Resource<A> { 
	let url: URL

	let parse: (Data) throws -> A 
}
```
  
Here are the same two endpoints defined as Resources:
```swift
let profile = Resource<User>(url: profileURL, parse: { 
	try JSONDecoder().decode(User.self, from: $0)
})

let post = Resource<BlogPost>(url: postURL, parse: {
	try JSONDecoder().decode(BlogPost.self, from: $0) 
})
```

Because the `Resource`’s parse function doesn’t know anything about [[JSON]] decoding, we can use `Resource` to represent other kinds of resources as well. To avoid duplication in each [[JSON]] resource, we create a convenience initializer that’s conditional on `A` being [[Decodable]]

```swift
extension Resource where A: Decodable { 
	init(json url: URL) {
		self.url = url 
		self.parse = { data in
			try JSONDecoder().decode(A.self, from: data) 
		}
	} 
}
```


This allows us to define the same resources in a much shorter way:

```swift
let profile = Resource<User>(json: profileURL)
let blogPost = Resource<BlogPost>(json: postURL)
```

Finally, we write a version of the load method that takes a `Resource` value:
```swift
extension URLSession {
	func load<A>(_ r: Resource<A>, callback: @escaping (Result<A, Error>) -> ()) {
	dataTask(with: r.url) { data, response, err in
		callback(Result {
			if let e = err { throw e }
			guard let d = data else { throw NoDataError() }
			return try r.parse(d)
		})
	}.resume()
}	
```

We can now call load with our profile resource, and in the callback, we’ll receive either a
User value or an error:
```swift
URLSession.shared.load(profile) { result in
	print(result)
}
```

As a nice side benefit of creating the generic `Resource` type, we have made the code
easier to test. A `Resource` is fully synchronous, which makes it easy to unit test the
parsing. The load method on `URLSession` is still hard to test, because it’s asynchronous.
But the asynchrony is now isolated in a single method, rather than in multiple methods.

---

## 📇 Additional Metadata

- 🗂 Type:: #type/snippet 
- Source:: [[Advanced Swift]]
- 🏷️ Tags:: [[Swift]]