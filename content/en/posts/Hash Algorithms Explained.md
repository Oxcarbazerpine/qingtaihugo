---
date: 2024-06-01
draft: false
lang: en
tags:
- Algorithsm
title: Hash算法
---

The original data is calculated into a string of fixed-length numbers through a hash function, (such as SHA-256 algorithm which is 256 bits long), the calculated value is called a hash value (or digest). Hash values are irreversible, meaning that original data cannot be deduced from the hash value. Even if the original data changes slightly, the calculated hash value will be completely different from the previous one, making it hard to break violently according to the previous value. In practical applications, it's often used for comparison. For instance, when we input a password, its hash value is calculated first and then transmitted to the server database. The password data stored in the database are all hash values of the original passwords, and a comparison with the hash value transmitted by the user verifies the correctness of the password.

When storing data, a hash table can be created based on the hash function, using the data itself to calculate the hash value as the index of the table. The calculation is as follows:
If the data are numbers, you can use the number itself (or each digit or every certain length such as four digits as a small segment, adding up to get the sum of each part), to mod table length and get the remainder, which is the index of the data in the table. If the data is a string, you can convert it to numbers based on the ASCII table, calculate the sum, and then continue with the previous algorithm.
Collision:
If two pieces of data calculate the same hash value, a collision will occur, the data that arrives later can be handled in several ways:
Open addressing (any data can occupy any position in the table according to the situation)
	1. 
Linear probing - Sequentially finding empty positions
	2. 
Plus 3 rehash - Jumping over three empty spots to find an empty position
	3. 
Other methods

In closed addressing, the way of chain connection is adopted, and new data is linked to the existing data that has occupied a position.