---
uuid: 20221009152621
created: 2022-10-09T15:26:21
alias:
- autorelease pool
tags:
---

# [[Autorelease pool]]

Your code runs in the presence of something called an **autorelease** pool. When [[ARC]] autoreleases an object, that object is placed in the autorelease pool, and a number is incremented saying how many times this object has been placed in this autorelease pool. From time to time, when nothing else is going on, the autorelease pool is automatically drained.  

In general, autoreleasing and the autorelease pool are merely an implementation detail. You can’t see them; they are just part of how ARC works. But sometimes, on very rare occasions, you might want to drain the autorelease pool yourself.

Swift provides such a way — the global autoreleasepool function, which takes a single argument that you’ll supply as an anonymous function using trailing closure syntax.

Before the anonymous function called, a special temporary autorelease pool is created, and is used for all autoreleased objects thereafter. After the anonymous function exits, the temporary autorelease pool is drained and goes out of existence. Here’s the same method with an autoreleasepool call wrapping the inner loop:

  
```swift
func test() {
	let path = Bundle.main.path(forResource:"001", ofType: "png")!
		for j in 0 ..< 50 {
			autoreleasepool {
                for i in 0 ..< 100 {
                    let im = UIImage(contentsOfFile: path)
                }
		} 
	}
}
```

---

## 📇 Additional Metadata

- 🗂 Type:: #type/note
- ℹ️ Source:: [[iOS 15 Programming Fundamentals with Swift]]