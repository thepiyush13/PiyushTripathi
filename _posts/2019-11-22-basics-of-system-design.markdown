---
layout: post
title: System Design Basics
date: 2019-11-22 13:32:20 +0300
description: Basic of system design # Add post description (optional)
img: icons/ #i-rest.jpg # Add image post (optional)
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
                         
    X------Performance-->+


   XXXXXX                
   XXXXXX+-scalability-->+ 
   XXXXXX               


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
                      <--Latency = t--->   |
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

 N1/N2 = nodes, 
 
 d1/d2 = data at N1/N2, 
 
 r1/r2 = incoming requests, 
 
 l1 = partition link

```

CA: normal cloud systems, d1==d2 and r1,r2 always get response


CP: faulty transactions, d1==d2 and l1 down but system working


AP: nosql, d1~=d2, r1/r2 always get response, l1 down but system works


Eventually consistent (weak consistent, A, P): 
update N1 or N2, background process updates other nodes, time delay for consistency, dynamodb in multi region


## CAP Patterns in Various Systems 

### A[P] (weakly consistent) 
highly available but weekly consistent. Every request gets a response but no guarantee that data would be consistent. 


Example: Most realtime systems, VOIP systems, memcahced 

### A[P] (Eventually consistent) 
highly available but consistent after some time delay. Every request gets a response but takes few ms for data to replicate across. 


Example: Most NOSql systems,dynamodb

### C (Strongly consistent) 
may not be highly available but very consistent. Data integrity is guaranteed. 


Example: Most RDBMS systems, Transactions, mySql

### Availability
We can maintain availibity in case of issues by:

#### Replication: always keep data copied
Master Slave: master processes traffic & replicates to slave. Master goes down, slave becomes master

#### Fail Over: replace a new server when need
active server processes traffic & send heartbeat to passive. Active goes down, passive becomes active

## DNS server

type google.com in browser -> 

browser only have name, no ip -> 

asks for ip from DNS host -> 

DNS host returns ip back ->

browser uses returned IP to connect to actual server

```

 
           BROWSER+--------------> GOOGLE (192.168.10.23)

           +------+ 

             |   ^
             |   |
  google.com |   | 192.168.10.23
             |   |
             |   |
             v   |

           +-------+

           DNS SERVER


```


what: resolve ip from domain name

why: cache, user friendly names

why not: latency, ddos attacks, 

how: has NS (name server, record of dns server), MX (mail xchange, mail server record), A (ip record), CNAME (canonical, alias for other host). route 53 is a dns server.

# Reverse prxoy, 
what:web server before actual servers

why: hide backend servers, security, SSL termination, compression, caching 

why not: single point of failure, increased complexity

how: varnish with nginx, HAproxy
