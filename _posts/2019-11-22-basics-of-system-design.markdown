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
