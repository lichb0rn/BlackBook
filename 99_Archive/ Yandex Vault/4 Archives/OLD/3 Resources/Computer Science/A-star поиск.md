---
aliases: ["A*", "A-star", "A star", "А звезда"]
---
MOC:  [[Algorithms]]

---

Алгоритм поиска маршрута с наименьшей стоимостью от одной вершины [[Граф (теория)|графа]] к другой.
Часто применяется для поиска пути в лабиринтах.

Порядок обхода определяется *эвристической функцией* "расстояние + стоимость" (обозначается $f(x)$). $f(x)$ является суммой двух других функций:
- функция стоимости достижения рассматриваемой вершины $g(x)$ (например, стоимость передвижения из одной ячейки в лабиринте в другую).
- функция эвристической оценки расстояния от рассматриваемой вершины к конечной $h(x)$

[[Обход графа|breadth-first]] и [[Обход графа|depth-first]] являются частными случаями алгоритма A*. 
При $h(x)=0$ получим ещё один частный случай -  [[Алгоритм Дийкстры]].

## Код

 ```swift
 public func aStar<StateType: Hashable>(initialState: StateType,
                                       goalTextFn: (StateType) -> Bool,
                                       successorFn: (StateType) -> [StateType],
                                       heauristicFn: (StateType) -> Float) -> AdvancingNode<StateType>? {
    
    var frontier = PriorityQueue<AdvancingNode<StateType>>(
        sort: <,
        elements: [AdvancingNode(state: initialState,
                                 parent: nil,
                                 cost: 0,
                                 heuristic: heauristicFn(initialState))]
    )
    
    var explored = Dictionary<StateType, Float>()
    explored[initialState] = 0
    
    while let currentNode = frontier.dequeue() {
        let currentState = currentNode.state
        
        // if we found the goal, we are done
        if goalTextFn(currentState) { return currentNode }
        
        // if not, check where we can go next
        for child in successorFn(currentState) {
            // this assumes the grid, there should be a cost function in more sofisticated applications
            let newCost = currentNode.cost + 1
            if (explored[child] == nil) || (explored[child]! > newCost) {
                explored[child] = newCost
                frontier.enqueue(AdvancingNode(state: child,
                                               parent: currentNode,
                                               cost: newCost,
                                               heuristic: heauristicFn(child)))
            }
        }
    }
    return nil
}
 
 ```