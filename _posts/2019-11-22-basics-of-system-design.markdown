---
layout: post
title: System Design Basics
date: 2019-11-22 13:32:20 +0300
description: Basic of system design # Add post description (optional)
img: icons/neutral_trading.svg #i-rest.jpg # Add image post (optional)
fig-caption: image # Add figcaption (optional)
tags: [Tech]
---


Vertical scaling
Horizontal scaling
Caching
Load balancing
Database replication
Database partitioning


# Trade Offs
## Performance vs Scalability
Performance = How system works for Single user

Scalability = How system works for Large no of users

```
                         +-----+
    X------Performance-->+     |
                         |     |
                         |     |
   XXXXXX                |     |
   XXXXXX+-scalability-->+     |
   XXXXXX                |     |
                         +-----+

```

## Latency vs Throughput
Latency = How much time each requests take

Throughput = How many requests are possible

```
+----------------------------------------+  +
                                            |
  +-------->                                |
           +---------->                     |
                                            Throughput = 3
                      +---------------->    |
                      <--Latency = t--->    |
                                            |
+----------------------------------------+  +

```

## CAP Theorem
CAP: Consistency, Availability, Partition Tolerance
Used to design systems as you can never have a system with All 3 elements of the CAP.

Consistency: is data consistent between nodes
Availability: is every request processed
Partition Tolerance: does system work even if some nodes go down


```
r1-->N1(d1)___________(link l1)__________N2(d2)<--r2

 N1/N2 = nodes, d1/d2 = data at N1/N2, r1/r2 = incoming requests, l1 = partition link

```

CA: normal cloud systems, d1==d2 and r1,r2 always get response
CP: faulty transactions, d1==d2 and l1 down but system working
AP: nosql, d1~=d2, r1/r2 always get response, l1 down but system works


