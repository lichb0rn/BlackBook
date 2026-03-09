---
created: 2026-03-09
tags:
  - type/note
source:
related:
area:
up:
aliases:
  - breadth first search
---
```python
def bfs(root):
	q = [root]
	while q:
		level_size = len(q)
		for _ in range level_size:
			node = q.popLeft()
			q <- node.left
			q <- node.right
	return
```