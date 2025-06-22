---
title: "Understanding Database Indexes"
date: 2024-06-01
draft: false
tags: ["Database"]
---

## What is an Index

A data structure that stores the index values and the disk addresses or raw data of the index entries.

## Common Data Structure: B+ Tree

### Why Not Other Data Structures

- **Binary Tree**  
  A one-way linked list is formed for incrementing indexes.

- **Binary Balanced Tree (Red-Black Tree)**  
  Each node stores the index and address. It balances the height of the left and right branches and was used by early MySQL. It is not fast enough because there are few data entries per level, and the tree is too tall.

- **B Tree**  
  It is multi-way. Each node stores the index and data. The index values increment from left to right without duplicate indexes.

- **B+ Tree**  
  Used by MySQL. All data is stored in leaf nodes. Non-leaf nodes only store redundant header indexes (like alphabetical indexes in a dictionary). Leaf nodes are linked by pointers to improve the performance of range searches.

### Characteristics

- B+ Tree is a binary tree
- Each node has multiple data entries. In MySQL, each node is 16KB in size
- The tree is short because a single node stores many data entries, usually having 3 levels

---

## Storage Engines: MyISAM and InnoDB

### Differences

- **MyISAM**  
  Each database is stored in the data directory. In each database table file, MyISAM has three types of files:  
  - `.frm` stores the table structure  
  - `.MYD` (D for data) stores raw data  
  - `.MYI` (I for index) stores table indexes, or the B+ tree structure  
  It uses non-clustered indexes where data and indexes aren't stored together, but separately in two files. Indexes just fetch the address.

- **InnoDB**  
  The table file only has two types:  
  - `.frm` stores the table structure  
  - `.idb` stores data and indexes  
  The corresponding row data is all hung on the leaf nodes, saving the I/O operation of fetching data by the address. InnoDB uses clustered indexes (Clustered Index), which have better performance.

### Connection

Internally, both use B+ Trees. After fetching the child nodes, they are loaded into memory for internal binary search.

---

## Considerations

### Why Does InnoDB Recommend Creating a Primary Key Index and Using an Auto-Increment Integer as the Primary Key?

- **Why have a primary key**  
  MySQL must first build a B+ tree to organize data, so an index is required. If it is a non-primary key index, the data stored at the leaf node is the value of the corresponding row's primary key, then another primary key index search is carried out. If there is not even a non-primary key index, MySQL will choose a unique column from the existing columns to build an index. If there is no such column, it will create a hidden column for indexing.

- **Why use integers**  
  Integer comparison is fast. When using a string index, the system must look up the encoding table (ASCII or UTF-8, etc.) bit by bit and then compare them. That's why the use of random string UUIDs isn't recommended.

- **Why auto-increment**  
  (No reason provided in the original text. Add as needed.)

---

## Index Types

Each column's index can be set. The default is B+ Tree, but it can be switched to Hash.

### Hash

- MySQL has its own hash implementation.
- In essence, it's an array + linked list. The hash value is calculated and used as the array key, with the data as the array value. If a hash collision occurs, the array value stores a pointer to the next node in the linked list, continuing until the end of the list points to the data.
- Although hash search speed can be faster than B+ Tree in general, since it cannot perform range searches, it is not widely adopted. However, for scenarios that do not require range searches, using a hash index can be considered.