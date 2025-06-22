---
date: 2024-06-01
draft: false
tags: ["Database"]
title: "Understanding Database Indexes"
---

What is an Index: A data structure that stores the index values and the disk addresses or raw data of the index entries.
Common Data Structure: B+ Tree.
Why not other data structures: 
Binary Tree: A one-way linked list is formed for incrementing indexes
Binary Balanced Tree (Red-Black Tree): Each node stores the index and address. It balances the height of the left and right branches and was used by early MySQL. It is not fast enough because there are few data entries per level, and the tree is too tall.
B Tree: It is multi-way. Each node stores the index and data. The index values increment from left to right without duplicate indexes.
B+ Tree: Used by MySQL. All data is stored in leaf nodes. Non-leaf nodes only store redundant header indexes (like alphabetical indexes in a dictionary). Leaf nodes are linked by pointers to improve the performance of range searches.
Characteristics:
* B+ Tree is a binary tree
* Each node has multiple data entries. In MySQL, each node is 16KB in size
* The tree is short because a single node stores many data entries, usually having 3 levels

Storage Engines MyISAM and InnoDB 
Differences:
MyISAM: Each database stored in the data directory. In each database table file, MyISAM has three types of files. The .frm file stores the table structure. The .MYD (D for data) file stores raw data. The .MYI (I for index) file stores table indexes, or the B+ tree structure. It uses non-clustered indexes where data and indexes aren't stored together, rather stored separately in two files, and indexes just fetch the address.
InnoDB: The library table file only has two types. The .frm file stores the table structure, and the .idb file stores data and indexes. The corresponding row data is all hung on the leaf nodes, saving the I/O operation of fetching data by the address. InnoDB uses clustered indexes (Clustered Index) which have better performance.
Connection:
Internally, both use B+ Trees. After fetching the child nodes, they are loaded into memory for internal binary search.

Reasons behind InnoDB recommending the establishment of primary key index and using integer increments as primary indexes: 
* Why to have a primary key: Because MySql must first build a B+ tree to organize data, it must have an index. If this is a non-primary key index, the data stored at the leaf node is the value of the corresponding row's primary key, then one more primary key index search is carried out. 
* Why to use integers: Integer comparison is fast. When using a string index, the system must look up the encoding table (ASCII or utf8, etc.) bit by bit and then compare them. That's why the use of random string UUIDs isn't recommended.
* Why auto-increment: 

Each column's index can be set, default is B+ Tree, but can be switched to Hash.
Hash: 
* MySQL has its own hash implementation
* In essence, it's an array + linked list. 
* Although under average circumstances hash search speed can be faster than B+ Tree, since it cannot perform range searches it hasn't been adopted. However, for scenarios that do not require a range search, considering a hash index can be a valid option.