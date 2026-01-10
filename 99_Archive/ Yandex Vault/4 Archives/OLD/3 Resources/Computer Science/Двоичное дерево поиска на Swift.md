---
uuid: 20221011104212
created: 2022-10-11T10:42:12
alias:
- binary search tree in swift
- двоичное дерево поиска на swift
---

# [[Двоичное дерево поиска на Swift]]

```swift
public class BinaryNode<Element> {
    
    public var value: Element
    public var leftChild: BinaryNode?
    public var rightChild: BinaryNode?
    
    public init(value: Element) {
        self.value = value
    }
}

extension BinaryNode {
    
    public func traverseInOrder(visit: (Element) -> Void) {
        leftChild?.traverseInOrder(visit: visit)
        visit(value)
        rightChild?.traverseInOrder(visit: visit)
    }
    
    public func traversePreOrder(visit: (Element) -> Void) {
        visit(value)
        leftChild?.traversePreOrder(visit: visit)
        rightChild?.traversePreOrder(visit: visit)
    }
    
    public func traversePostOrder(visit: (Element) -> Void) {
        leftChild?.traversePostOrder(visit: visit)
        rightChild?.traversePostOrder(visit: visit)
        visit(value)
    }
}

extension BinaryNode where Element: Comparable {
    
    var isBinarySearchTree: Bool {
        return isBST(self, min: nil, max: nil)
    }
    
    private func isBST(_ tree: BinaryNode<Element>?, 
					   min: Element?, 
					   max: Element?) -> Bool {
		
        guard let tree = tree else {
            return true
        }
        
        if let min = min, tree.value <= min {
            return false
        } else if let max = max, tree.value > max {
            return false
        }
        
        return isBST(tree.leftChild, min: min, max: tree.value) && 
				isBST(tree.rightChild, min: tree.value, max: max)
    }
}

extension BinarySearchTree: Equatable {
    // Checking if two BSTs are equal
    public static func == (lhs: BinarySearchTree<Element>, 
						   rhs: BinarySearchTree<Element>) -> Bool {
        return isEqual(lhs.root, rhs.root)
    }

    // O(n)
    private static func isEqual<Element: Equatable>(
        _ node1: BinaryNode<Element>?,
        _ node2: BinaryNode<Element>?) -> Bool {
            
            guard let leftNode = node1, let rightNode = node2 else {
                return node1 == nil && node2 == nil
            }
            
            return leftNode.value == rightNode.value &&
                isEqual(leftNode.leftChild, rightNode.leftChild) &&
                isEqual(leftNode.rightChild, rightNode.rightChild)
        }
}

extension BinarySearchTree where Element: Hashable {
    
    // Check if a tree is subtree of the given tree
    // O(n)
    public func contains(_ subtree: BinarySearchTree) -> Bool {
        // The idea is to put elements in a set
        // To contain a tree the given tree must be a supset of the other tree
        var set: Set<Element> = []
        root?.traverseInOrder {
            set.insert($0)
        }
        
        var isEqual = true
        subtree.root?.traverseInOrder {
            isEqual = isEqual && set.contains($0)
        }
        
        return isEqual
    }
}

extension BinaryNode: CustomStringConvertible {
    public var description: String {
        return diagram(for: self)
    }
    
    private func diagram(for node: BinaryNode?,
                         _ top: String = "",
                         _ root: String = "",
                         _ bottom: String = "") -> String {
        
        guard let node = node else {
            return root + "nil\n"
        }
        
        if node.leftChild == nil && node.rightChild == nil {
            return root + "\(node.value)\n"
        }
        
        return diagram(for: node.rightChild,
                          top + " ", top + "┌──", top + "│ ")
        + root + "\(node.value)\n"
        + diagram(for: node.leftChild,
                     bottom + "│ ", bottom + "└──", bottom + " ")
    }
}
```

---

## 📇 Additional Metadata

- 🗂 Type:: #type/snippet 
- ℹ️ Source:: [[Data Structures & Algorithms in Swift]]
- 🏷️ Tags:: [[Algorithms]], [[Swift]]