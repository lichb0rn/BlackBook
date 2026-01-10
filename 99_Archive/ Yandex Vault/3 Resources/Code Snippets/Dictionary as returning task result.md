---
uuid: 20221002141454
created: 2022-10-02T14:14:54
alias:
---

# [[Dictionary as returning task result]]

Вернуть результат [[TaskGroup]] в виде словаря

```swift
func fetchManyURLs() async throws -> [URL:Data] {
	let urls: [URL] = // ...
	return try await withThrowingTaskGroup(
		of: [URL:Data].self,
		returning: [URL:Data].self) { group in
		
			var result = [URL:Data]()
			for url in urls {
				group.addTask {
					return [url: try await self.download(url: url)]
				} 
			}
			
			for try await d in group {
				result.merge(d) {cur,_ in cur}
			}

			 return result
	} 
}
```

---

## 📇 Additional Metadata

- 🗂 Type:: #type/snippet 
- ℹ️ Source::  [[iOS 15 Programming Fundamentals with Swift]]
- 🏷️ Tags:: [[Swift Concurrency Model]]