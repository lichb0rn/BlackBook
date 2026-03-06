---
created: 2026-03-06
alias: apriori algorithm
tags:
  - type/note
source: "[[Web Data Mining with Python]]"
related:
  - "[[Data Mining]]"
up:
---
# [[Алгоритм Apriori]]

**Алгоритм Apriori** ищет [[Ассоциативные правила|ассоциативные правила]] и применяется по отношению к базам данных, содержащим огромное количество транзакций.

Пусть у нас имеется некий датасет (или коллекция) _D,_ такой, что $D = {d_0 ... d_j}$, где _d_ — уникальная транзакция-itemset (например, кассовый чек). Внутри каждой _d_ представлен набор _items (i — item)_, причем в идеальном случае он представлен в бинарном виде: _d1 = [{Пиво: 1}, {Вода: 0}, {Кола: 1}, {...}], d2 = [{Пиво: 0}, {Вода: 1}, {Кола: 1}, {...}]_. Принято каждый itemset описывать через количество ненулевых значений (_k-itemset_), например, _[{Пиво: 1}, {Вода: 0}, {Кола: 1}]_ является _2-itemset_.

- Основные компоненты:
	- Поддержка (support)
	- Достоверность (confidence)
	- Лифт (lift)

- Поддержка
	- $$supp(X) = \frac{t \in T; X \in t}{|T|}$$
	- где X — itemset, содержащий в себе i-items, а T — количество транзакций. Т.е. в общем виде это показатель «частотности» данного itemset во всех анализируемых транзакциях.
- Достоверность
	- $$conf(x_1 \cup x_2) = \frac{supp(x_1 \cup x_2)}{supp(x_1)}$$
	- Confidence refers to the likelihood that Item B is also bought if item A is bought. It can be calculated by finding the number of transactions where A and B are bought together, divided by the total number of transactions where A is bought.
- Лифт
	- Lift(A -> B) refers to the increase in the ratio of sale of B when A is sold. Lift(A –> B) can be calculated by dividing Confidence(A -> B) divided by Support(B).
	- $$Lift(x_1 \cup x_2)=\frac{conf(x1 \cup x_2)}{supp(x_2)}$$