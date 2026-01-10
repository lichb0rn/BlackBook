---
uuid: 20230126091227
created: 2023-01-26T09:12:27
alias: linked-list queue
---

# [[python linked-list queue]]


```python
class Queue:
    def __init__(self):
        self.front = None
        self.back = None

    def enqueue(self, elem):
        node = LinkedList.Node(elem)
        if self.back == None:
            self.front = node
            self.back = node
        else:
            self.back.next = node
            self.back = node

    def dequeue(self):
        if self.front == None:
            return None

        value = self.front.value
        self.front = self.front.next
        if self.front == None:
            self.back = None
        return value

    def length(self):
        length = 0
        if self.back == None:
            return length
        else:
            current = self.front
            while current != None:
                current = current.next
                length += 1
        return length
```


---

## 📇 Additional Metadata

- 🗂 Type:: #type/snippet 
- ℹ️ Source:: 
- 🏷️ Tags:: [[Python]], [[Algorithms|data structure]]