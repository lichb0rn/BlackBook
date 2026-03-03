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