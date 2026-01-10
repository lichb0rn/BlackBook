---
uuid: 20221011093914
created: 2022-10-11T09:39:14
alias:
- breadth-first
- breadth first
- поиск в ширину
- bfs
tags:
---

# [[Breadth-First Search]]
 
  - Идея [[Algorithms|алгоритма]] в том, что мы выбираем вершину и помещаем всех её соседей в [[Очередь]]. Далее мы убираем элементы из стека по одному и помещаем их соседей в стек, если до этого не были помещены в него.
   
   ### Код
   ```swift
   extension Graph where Element: Hashable {
    public func breadthFirstSearch(from source: Vertex<Element>) -> [Vertex<Element>] {
        
        // Queue keeps track of neighboring vertices to visit next
        var queue = QueueStack<Vertex<Element>>()
        
        // Set to remember what has been equeued before
        var enequeued: Set<Vertex<Element>> = []
        
        // Visited vertices in the order they were explored
        var visited: [Vertex<Element>] = []
        
        queue.enqueue(source)
        enequeued.insert(source)
        
        while let vertex = queue.dequeue() {
            visited.append(vertex)
            
            // Getting all edges from the vertex
            // Add them to the queue if they aren't there
            let neighborEdges = edges(from: vertex)
            neighborEdges.forEach { edge in
                if !enequeued.contains(edge.destination) {
                    queue.enqueue(edge.destination)
                    enequeued.insert(edge.destination)
                }
            }
        }
        
        return visited
    }
}
   ```
   
   ### Производительность
   - Вставка в стек - $O(V)$
   - Обход граней - $O(E)$
   - Общая сложность алгоритма: *$O(V+E)$*
   - Затраты на память: *$O(V)$* т.к. мы помещаем все вершины в стек.

Алгоритм удобно использовать, если у вершин графа много соседей или если нужно найти все возможные случаи.


---

## 📇 Additional Metadata

- 🗂 Type:: #type/snippet
- ℹ️ Source:: [[Data Structures & Algorithms in Swift]]
- Реализация [[Графы (реализация)|графа]]