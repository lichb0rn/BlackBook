---
uuid: 20221002141245
created: 2022-10-02T14:12:45
alias:
---

# [[Task sleep extension]]

```swift
extension Task where Success == Never, Failure == Never {
	static func sleep(_ seconds:Double) async {
		await self.sleep(UInt64(seconds * 1_000_000_000))
	}

	static func sleepThrowing(_ seconds:Double) async throws {
		try await self.sleep(nanoseconds: UInt64(seconds * 1_000_000_000))
	} 
}
```

---

## 📇 Additional Metadata

- 🗂 Type:: #type/snippet 
- ℹ️ Source:: [[iOS 15 Programming Fundamentals with Swift|iOS 15 Programming Fundamentals with Swift]]
- 🏷️ Tags:: [[Swift Concurrency Model]], [[Software Testing]]