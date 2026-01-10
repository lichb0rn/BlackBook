---
uuid: 20221111173903
created: 2022-11-11T17:39:03
alias:
- swift trie
tags:
---

# [[Trie на Swift]]

Код на [[Swift]]
- Узел дерева
```swift
public class TrieNode<Key: Hashable> {
    
    public var key: Key?
    public weak var parent: TrieNode?
    public var children: [Key: TrieNode] = [:]
    public var isTerminating: Bool = false
    
    public init(key: Key?, parent: TrieNode?) {
        self.key = key
        self.parent = parent
    }
}

```

- Построение
```swift
public class Trie<CollectionType: Collection & Hashable> where CollectionType.Element: Hashable {
    
    public typealias Node = TrieNode<CollectionType.Element>
    
    private let root = Node(key: nil, parent: nil)
    
    public init() {}
    
    public private(set) var collections: Set<CollectionType> = []
    public var isEmpty: Bool {
        return collections.isEmpty
    }
    public var count: Int {
        return collections.count
    }
    
    // O(n), where n is the number of elements in the collection
    public func insert(_ collection: CollectionType) {
        var current = root
        
        for element in collection {
            if current.children[element] == nil {
                current.children[element] = Node(key: element, parent: current)
            }
            current = current.children[element]!
        }
        
        if current.isTerminating {
            return
        } else {
            current.isTerminating = true
            collections.insert(collection)
        }
    }
    
    // O(n), where n is the number of elements in the collection
    public func contains(_ collection: CollectionType) -> Bool {
        var current = root
        
        for element in collection {
            guard let child = current.children[element] else {
                return false
            }
            current = child
        }
        return current.isTerminating
    }
    
    public func remove(_ collection: CollectionType) {
        var current = root
        for element in collection {
            guard let child = current.children[element] else {
                return
            }
            current = child
        }
        
        guard current.isTerminating else {
            return
        }
        
        current.isTerminating = false
        collections.remove(collection)
        
        while let parent = current.parent,
                current.children.isEmpty && !current.isTerminating {
            
            parent.children[current.key!] = nil
            current = parent
        }
    }

}

public extension Trie where CollectionType: RangeReplaceableCollection {
    func collections(startingWidth prefix: CollectionType) -> [CollectionType] {
        var current = root
        for element in prefix {
            guard let child = current.children[element] else {
                return []
            }
            current = child
        }
        
        return collections(startingWith: prefix, after: current)
    }
    
    private func collections(startingWith prefix: CollectionType, after node: Node) -> [CollectionType] {
        var results: [CollectionType] = []
        
        if node.isTerminating {
            results.append(prefix)
        }
        
        for child in node.children.values {
            var prefix = prefix
            prefix.append(child.key!)
            results.append(contentsOf: collections(startingWith: prefix, after: child))
        }
        return results
    }
}
```


---

## 📇 Additional Metadata

- 🗂 Type:: #type/snippet 
- ℹ️ Source:: [[Data Structures & Algorithms in Swift]]