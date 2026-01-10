---
aliases: ["scatterplot", "диаграмма рассеяния"]
tags: [""]
---
MOC:  [[Seaborn]]

---

Построить диаграмму рассеяния в `seaborn` можно так:

```python
import seaborn as sns

axes = sns.scatterplot(data=nyc, 
					   x='Date', 
					   y='Temperature', 
					   hue='Temperature', 
					   palette='winter', 
					   legend=False)
```
где:
- `data` - [[DataFrame]] с данными
- `x` и `y` - названия колонок/векторов в `data`
- `hue` - определяет, какой вектор/колонка должен определять цвета точек
- `palette` - цветовая карта [[Matplotlib]]
- `legend=False` - нужно ли отображать легенду.

Результат:
![[Pasted image 20220704100659.png]]
### Построение линейной регрессии
С помощью [[NumPy]]  и [[scikit-learn]] можно построить линейную регрессию на диаграмме:
- заводим lambda:
```python
predict = (lambda x: linear_regression.coef_ * x + linear_regression.intercept_)
```

- скейлим оси:
```python
axes.set_ylim(10, 70)
```

- строим:
```python
import numpy as np
import matplotlib.pyplot as plt

x = np.array([min(nyc.Date.values), max(nyc.Date.values)])
y = preduct(x)

line = plt.lot(x, y)
```

![[Pasted image 20220704103637.png]]

source: [[Intro to Python for Computer Science and Data Science: Learning to Program with AI, Big Data and The Cloud]], case study 15.4: Time Series and Simple Linear Regression