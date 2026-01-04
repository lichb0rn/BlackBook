---
tags:
  - type/note
domain: "[[MongoDB]]"
topics:
sources: "[[MongoDB in Action]]"
---
Capped collections in MongoDB are collections of a fixed size (the number of documents can also be capped) that facilitate operations with high throughput for inserting and retrieving documents according to the order of insertion. They operate similarly to circular buffers: when a capped collection reaches its size limit, it accommodates new documents by replacing the oldest documents within the collection. 

Capped collections ensure the maintenance of insertion order, eliminating the need for an index to retrieve documents in the order in which they were added. 


As an alternative to capped collections, consider MongoDB’s time-to-live (TTL) indexes. These indexes allow you to expire and remove data from normal collections based on the value of a date-typed field and a TTL value for the index. TTL indexes are not compatible with capped collections.