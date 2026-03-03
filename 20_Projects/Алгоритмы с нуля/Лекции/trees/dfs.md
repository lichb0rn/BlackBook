---
created: 2026-03-03
tags:
  - type/note
source:
related:
area:
up:
aliases:
  - обход в глубину
  - depth-first search
---

## Рекурсивный обход в глубину

```python
def dfs(node):
	if not node:
		return
	# 1. pre-order 
	# print(node.val)
	dfs(node.left)
	# 2. in-order
	# print(node.val)
	dfs(node.right)
	# 3. post-order
	# print(node.val)
	return
```

## Обход в глубину на стеке

```python
def dfs(node):
	stack <- node
	while stack:
		node <- stack
		stack <- node.right
		stack <- node.left
		print(node.val)
```