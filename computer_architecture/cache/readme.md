---
title: "Cache"
parent: Computer Architecture
permalink: "/computer_architecture/cache"
layout: default
---

### Cache

A place between the CPU and a storage device to store recent accessed data closer to the CPU, being served faster.

#### Architectures
* Fully Associative (Block 12 can go anywhere)  
  Blocks are identified by a "tag" that **has** to correspond to the entire block address.  
  A cache with 1024 blocks of 32 bits can hold 1024 tags.
  
* Direct Mapped (Block 12 can only go into block 4 (12 mod 8))  
  Each block has only one possible position to be placed on cache. Part of the address is used to address the block in cache, the remaining bits are compared with the block "tag" to confirm the identity.
  
* Set Associative (Block 12 can go anywhere in set 0 (12 mod 4))  
  Part of the address is used to address a group of blocks in cache, the identification of the block inside a group is done via a comparison of the remaining bits with the "tag". Each block has a determined number of positions (number of ways or associativity) allowed on the cache.
  
Independently of architecture, a cache memory can be described by: 
* Associativity (K)
* Number of sets (NSets)
* Block dimension (BS)

If K=1, it's a Direct Mapped Memory.  
If NSets=1, it's a Fully Associative Memory.  
If NSets>1 and K>1, it can be identified as a K-way Set Associative Cache.  

The maximum capacity of the memory cache can be determined with:
> Mc = K * NSets * BS

Block dimension (BS)
> BS = AddrUnit * 2^BO
BO is the number of necessary bits to address one adressing unit inside a block. 
>  BO = log2(BS/AddrUnit)

#### Read Policies

If the wished block is in cache, it can be considered a **hit**, being transfered to the processor, not being required the intervention of the RAM and the operation is completed in the response time of the cache.  
In case of a **miss**, it becomes necessary to consult the RAM, and there can be implemented one of two procediments:
* Read-Through / Forward: The block is read directly from the RAM to the processor and cache. (Should be used when memory bus coincides with block dimension)
* No Read-Through: The block is read from RAM to cache. Then the data is transfered from cache to the processor. (Can be used independently of differences between memory and cache)
* Concorrency: The search is made concorrently between RAM and cache. In case of a miss (not in cache) it is faster than other implementations. However, it ocupies more time the memory bus, and it's more complex to implement.

##### Non-blocking Caches
Usually, cache can only handle one request at once. So, in case of a miss the cache would be inaccessible to other requests.  
The non-blocking cache was introduced in L2 cache of the Pentium Pro and Pentium II and it depends on the use of two independent buses.

#### Write Policies

* Write-through: Write simultaneously into memory and cache. (No advantages of having cache)
* Write-back: The write is only done to cache. Copying to RAM is only done when necessary. (Needs protocols and controllers to keep consistency between them).

In case of a miss:
* Write-Allocate: Allocates a block in cache. Can be necessary to read block from RAM.
* No-Write-Allocate: Write operations are done in RAM.

#### Substition Policies
When a new data group is decided to go into a full cache memory (normal behavior):

* Random: Block is chosen at random, easy to implement but can replace highly searched blocks, reducing cache efficiency.
* LRU (Least Recently Used): The block which last use was the longest time ago. It requires additional space to keep the state of use of each block.
* pLRU (Pseudo Least Recently Used)
* FIFO (First In First Out): It uses a sequencial selection of the position of a new block.


#### Metrics and Misses
To evaluate performance of a memory system is used the (AMAT - average memory access time).

* Compulsory Misses: When data is asked for the first time, not existing in cache.
* Capacity Misses: Limitations of the dimension of the cache.
* Conflit Misses: Dependent on the architecture of the cache.

#### Other Auxiliary Caches

* Write Buffer
* Miss-Cache
* Victim-Cache
