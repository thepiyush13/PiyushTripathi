---
layout: post
title: System Design Basics
date: 2020-11-22 13:32:20 +0300
description: Basic Of System Design # Add Post Description (Optional)
img: icons/services.svg #I-Rest.Jpg # Add Image Post (Optional)
fig-Caption: Image # Add Figcaption (Optional)
tags: [Tech]
---


Vertical Scaling
Horizontal Scaling
Caching
Load Balancing
Database Replication
Database Partitioning


# Trade Offs
## Performance Vs Scalability
Performance = How System Works For Single User

Scalability = How System Works For a Large No Of Users

```
                         
    X------Performance-->+


   Xxxxxx                
   Xxxxxx+-Scalability-->+ 
   Xxxxxx               


```

## Latency Vs Throughput
Latency = How Much Time Each Requests Take

Throughput = How Many Requests Are Possible

```
+----------------------------------------+  +

                                            |
  +-------->                                |
           +---------->                     |
                                            Throughput = 3

                      +---------------->    |
                      <--Latency = T--->    |
                                            |

+----------------------------------------+  +

```

## Cap Theorem
Cap: Consistency, Availability, Partition Tolerance

Used To Design Systems As You Can Never Have A System With All 3 Elements Of The Cap.

1. Consistency: Is Data Consistent Between Nodes
2. Availability: Is Every Request Processed
3. Partition Tolerance: Does System Work Even If Some Nodes Go Down



```
R1-->N1(D1)___________(Link L1)__________n2(D2)<--R2

 N1/N2 = Nodes, 
 
 D1/D2 = Data At N1/N2, 
 
 R1/R2 = Incoming Requests, 
 
 L1 = Partition Link

```

Ca: Normal Cloud Systems, D1==D2 And R1,R2 Always Get Response


Cp: Faulty Transactions, D1==D2 And L1 Down But System Working


Ap: Nosql, D1~=D2, R1/R2 Always Get Response, L1 Down But System Works


Eventually Consistent (Weak Consistent, A, P): 
Update N1 Or N2, Background Process Updates Other Nodes, Time Delay For Consistency, Dynamodb In Multi Region


## Cap Patterns In Various Systems 

### A[P] (Weakly Consistent) 
Highly Available But Weekly Consistent. Every Request Gets A Response But No Guarantee That Data Would Be Consistent. 


Example: Most Realtime Systems, Voip Systems, Memcahced 

### A[P] (Eventually Consistent) 
Highly Available But Consistent After Some Time Delay. Every Request Gets A Response But Takes Few Ms For Data To Replicate Across. 


Example: Most Nosql Systems,Dynamodb

### C (Strongly Consistent) 
May Not Be Highly Available But Very Consistent. Data Integrity Is Guaranteed. 


Example: Most Rdbms Systems, Transactions, Mysql

### Availability
We Can Maintain Availibity In Case Of Issues By:

#### Replication: Always Keep Data Copied
Master Slave: Master Processes Traffic & Replicates To Slave. Master Goes Down, Slave Becomes Master

#### Fail Over: Replace A New Server When Need
Active Server Processes Traffic & Send Heartbeat To Passive. Active Goes Down, Passive Becomes Active

## Dns Server

Type Google.Com In Browser -> 

Browser Only Have Name, No Ip -> 

Asks For Ip From Dns Host -> 

Dns Host Returns Ip Back ->

Browser Uses Returned Ip To Connect To Actual Server

```

 
           Browser+--------------> Google (192.168.10.23)

           +------+ 

             |   ^
             |   |
  Google.Com |   | 192.168.10.23
             |   |
             |   |
             V   |

           +-------+

           Dns Server


```


What: Resolve Ip From Domain Name

Why: Cache, User Friendly Names

Why Not: Latency, Ddos Attacks, 

How: Has Ns (Name Server, Record Of Dns Server), Mx (Mail Xchange, Mail Server Record), A (Ip Record), Cname (Canonical, Alias For Other Host). Route 53 Is A Dns Server.

## Reverse Proxy, 
What:Web Server Before Actual Servers

Why: Hide Backend Servers, Security, Ssl Termination, Compression, Caching 

Why Not: Single Point Of Failure, Increased Complexity

How: Varnish With Nginx, Haproxy

## Users 1 To 10 Million Progression

Basic Request Flow In The System

	User (U)——>Server(S)——>Db

Application Layer Progression

	S > Dns > Reverse Proxy > Cache > Elb > Cdn > Read/Write Server > Async Endpoints (Que>Worker)

Database Layer Progression

	Db > Sql > Nosql + S3 > Cache > Replication (Master,Slave) > Sharding (Pk,Sk) > Compression (Shortcode)

## Cache
### What: 
Memoize Execution Results

### Why: 
Improve Lookup Times

### How:

#### Types:

    Client Cache > Cdn Cache > Web Server Cache > Application Cache (Memcached/Redis) > Datbase Cache (Query, Object) 
Write Methods:

**Cache-Aside**

  * Client->Cache, Found(√) ->Client | Not_found(X) ->Db->Update Cache -> Client)

  * Good: Lazy Loaded, Only Needed Data Is Cached

  * Bad: Cache Miss = 3 Trips = Delay, Cache Update Depends On Client Request(Ttl Fixes It)

**Write Through**

* Client->Cache->Db->Client

* Good: No Cache Miss, Always Updated Cache

* Bad: Delay On Write, Too Much Data In Cache


**Write Behind**

* Client->Cache->Client....>Async Update To Db

* Good: Faster Writes, Always Updated Cache

* Bad: Data Loss If Async Failed, Too Much Data In Cache


**Refresh Ahead** 

* Client->Cache->Client....>Async Update From Db

* Good: Predictive Cache, Only Hot Items Cached

* Bad: Hard To Predict Hot Items Accurately 

### Why Not:

1. Maintain Consistency Between Cache And Storage, Extra Work
2. Single Point Of Failure Unless Distributed(Memcached)
3. Cache Invalidation Is A Hard Problem (Lru,Lfu)



## Load Balancer (ELB)

```


Requests      +-----+   +----->Server1
+-----------> |     |   |
              |     |   |
+-----------> |ELB  +--------->Server2
              |     |   |
+-----------> |     |   |
              |     |   +----->Server3
              +-----+
    Modes: active-active, active-passive

    Server Selection:
    Roundrobin/least_busy/random/sticky_session


```

### Why:
1. Distribute load to multiple servers
2. Prevent overloading single server
3. Prevent requests to unhealthy servers

### Why not:
1. Single point of failure unless setup in active-active,active-passive mode
2. Performance bottleneck
3. Increases complexity for maintaining sticky sessions etc


### How:
### ELB: Elastic Load Balancer:
ELB stands for Elastic load balancer. It is used in places where we want to distribute the incoming request load to several servers as opposed to a single server. It operates on layer 4 (network) and relatively less compute intensive.

### ALB: Elastic Load Balancer:
It is used to distribute application load to different internal servers. It operates on layer 7 (application) and offer more flexibility but needs more computing/resources.

## ASYNC operations

```

                      Queue
Publisher       +--------------------+  Subscriber
--------------> |  ||  ||  ||  || || | ---------->
  job           ++-------------------+
                 | |               |
  <--------------+ |               v
     jobID         |            if QueSize > Memory
                   v             Maintain BackPressure
                 queue_item         +
         (itemid,jobid,data)        |
                                    |
                                    v
                                  Send response:
                                  HTTP 503
                                  server busy
                                     | ^
                                     | |
                                     | |
                                     | |
                                     v +
                                  User retries
                                  exponential backoff


```

### Why:
1. Improves App Responsiveness By Pushing Compute Intensive Operations In The Background 
2. Good For Large File Uploads, High Volume Of Data, Concurrent Requests
3. Can Help Doing Some Compute In-Advance (Timeline Generation Etc)

### Why Not:
1. Not Suitable For Real-Time Or Time Critical (Near Instant) Operations
2. Queue Size Can Exceed Memory: This Could Lead To Slow Performance, Cache Miss Etc. Solution Is To Use Maintain Back Pressure. Back Pressure Works By Sending A User Http 503 (Server Busy) If The Queue Is Filled Up. User Can Then Retry Normally Or Use Exponential Backoff (Time B/W Each Retry Increases Exponentially)

### How:
### Message Queue:
It Gets The Message From A Publisher, Holds It And Then Delivers It To Subscribers. No Processing Is Done In The Queue Itself. Example Is:
1. Redis: Simple But Could Loose Messages
2. Rabbitmq: Popular But Needs Amqp Protocol Use
3. Amazon Sqs: Managed Queue But High Latency And Message Sometimes Delivered Twice


### Task Queue:
This Takes Task Definition And Data, Processes It And Delivers The Results.

