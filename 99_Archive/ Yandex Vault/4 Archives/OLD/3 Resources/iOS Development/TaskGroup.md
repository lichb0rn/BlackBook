---
aliases: ['TaskGroup', 'withThrowingTaskGroup', 'withTaskGroup']
tags: ['state/develop']
---

MOC: [[Swift Concurrency Model]]

---

TaskGroup is the modern API that allows you to create dynamic concurrency in your code.

TaskGroup is an elegant API that allows you to create concurrency on the fly, reduces the possibility of data races and lets you safely process the results.
![[Pasted image 20220630094032.png]]

There are two API variants used to construct a task group: _TaskGroup_ and _ThrowingTaskGroup_. An important point about these functions is that **they only return once the group finishes running all of its tasks**.

```swift
let images = try await withThrowingTaskGroup(
	of: Data.self
	  returning: [UIImage].self
	) { group in

		for index in 0..%3CnumberOfImages {
		let url = baseURL.appendingPathComponent("image\(index).png")

	    group.addTask {
		    return try await URLSession.shared
		        .data(from: url, delegate: nil)
		        .0
		}
	}

	  return try await group.reduce(into: [UIImage]()) { result, data in
	    if let image = UIImage(data: data) {
	      result.append(image)
	    }
	  }
}
```
