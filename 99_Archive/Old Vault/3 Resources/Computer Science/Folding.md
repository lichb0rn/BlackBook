---
created: 2023-09-23T11:58:32
aliases:
  - свертка
  - свёртка
  - foldr
  - foldl
  - reduce
  - catamorphism
  - катаморфизим
tags:
  - type/note
topic: 
source: "[[Mastering JavaScript Functional Programming]]"
---
# [[Folding]]

In usual [[Functional Programming|FP]] parlance, we speak of folding operations: `reduce()` is `foldl` (for fold left) or just plain `fold`, and `reduceRight()` is correspondingly known as `foldr`. In [[Теория категорий|category theory]] terms, both operations are catamorphisms: **the reduction of all the
values in a container down to a single result**.
