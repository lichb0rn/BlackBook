---
uuid: 20230701104639
created: 2023-07-01T10:46:39
alias: PageRank
---

# [[Page rank]]

The basic concept behind the page rank algorithm is that if many highly ranked pages are pointing to a page, then the rank of that page will be measured as high. So, the rank of a page depends upon the ranks of the pages pointing to it. The process of ranking the pages is done iteratively until the ranks of all the pages are determined.

$$
PR(p) = \frac{d}{n} + (1 - d)\sum(PR(q) Outdegree(q))
$$
где $(q,p) \in G$, $G$ - [[Граф (теория)| направленный граф]]

If a Web page, for example, A is connected to another Web page B, with a pointing arrow toward B, then the `Indegree` of B will be represented as 1, and the `Outdegree` of A will be represented as 1.

Now, in the given equation, $n$ is the number of nodes in the graph, and $OutDegree (q)$ is the number of hyperlinks on page $q$.

The [[Классическая вероятность|вероятность]] that a random Web surfer arrives at a page $p$ by typing the URL or from a bookmark is represented by the first term on the right-hand side of the given equation - $PR(q)$.

The probability that the surfer chooses a URL directly is represented by $d$. The probability that a person arrives at a page by traversing a link is represented by $1−d$. The second term on the right-hand side of the equation is the probability of arriving at a page by traversing a link.

One easy-to-understand equation has been used by practicalecommerce.com, which states:
$PageRank\ for\ a\ given\ page = Initial\ PageRank + (total\ ranking\ power\ +\ number\ of\ outbound\ links)\ + ...$

---

## 📇 Additional Metadata
- 🛠️ Status:: 
- 🗂 Type:: #type/note
- ℹ️ Source::  [[Web Data Mining with Python]]
-  🏷️ Tags:: [[Algorithms]]