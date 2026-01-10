---
aliases: ["three-way set disjointness"]
tags: [""]
---
MOC:  [[Algorithms]]

---

Алгоритм определяет, являются ли три [[Множество|множества]] непересекающимися.

## Наивная реализация
Просто проходим по всем элементам и сравниваем.
Сложность: $O(n^3)$
```python
# Naive implementation: O(n^3)
def disjoint_naive(A, B, C):
    """Return True if there is no element common to all three lists."""
    for a in A:
        for b in B:
            for c in C:
                if a == b == c:
                    return False
    return True
```

## Оптимизированная версия
Сравниваем элементы из множества `C` только, если есть пересечение `A` и `B`.
Сложность: $O(n^2)$
```python
# Optimized naive algorithm: O(n^2)
def disjoint_naive_optimized(A, B, C):
    """Return True if there is no element common to all three lists."""
    for a in A:
        for b in B:
            if a == b:
                for c in C:
                    if a == c:
                        return False
    return True
```
Алгоритм работает в худшем случае за $O(n^2)$. 
Пояснение:
- существует $n^2$ пар $(a, b)$. Соответственно, если мы не нашли совпадения в них, в `C` не идём.
- если же мы нашли на последних позициях, то $O_{a,b}(n^2) + O_C(n) = O(n^2)$.