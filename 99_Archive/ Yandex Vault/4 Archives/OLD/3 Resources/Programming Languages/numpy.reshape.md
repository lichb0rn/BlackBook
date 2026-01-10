---
aliases: ["reshape"]
tags: [""]
---
MOC:  [[NumPy]]

---

У `numpy` есть интересный метод `reshape`, который позволяет трансформировать массив из одной формы в другую. 

```python
numpy.reshape(a, newshape, order='C')
```

Пример:
`nyc.Date.values.reshape(-1, 2)` - переделаем одномерный массив в двумерный: 1 колонка по 2 элемента.