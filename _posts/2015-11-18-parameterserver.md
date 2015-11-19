---
layout: post
title: Scaling Distributed Machine Learning with the Parameter Server.
description:
tags: paper-summary-big-data-machine-learning
comments: true
---

Takeaways from *Scaling Distributed Machine Learning with the Parameter Server, Li et al, OSDI, 2014.*

This paper proposes an optimized system - Parameter Server - for solving large-scale generic machine learning problems. The typical machine learning problem consists of iteratively finding parameters (or weights) that minimize the objective function (that captures the loss and the complexity of the learned model). The learning may be unsupervised or supervised based on presence of traning / labeled data.
 
This paper improves prior systems on one or more of the following fronts:

- Efficient Communication. Reduced network traffic and overhead.
- Flexible consistency. Offers a way to balance algorithmic convergence and system efficiency.
- Elastic scalability. New nodes can be added during runtime.
- Fault tolerance. Replication of parameters with well-defined behavior using vector clocks.
- Ease of use. Linear algebra data types - sparse vector representation of key, value pairs.
 
### Architecture.

The system proposed - Parameter Server - consists of a single server group and several worker groups.

- Server Group.
	- Server Nodes. Maintains a partition of globally shared parameters.
	- Server Manager. Maintains a consistent view of the servers with regards to node liveness and assignment of parameter partitions.
- Worker Groups. Each runs an application.
	- Worker Nodes. Stores a portion of training data and computes local statistics.
	- Task Scheduler. Assigns tasks and monitors task progress for each worker node in the group.
 
### Key Features.

- Parameters are treated as linear algebra objects. Key, Value pairs are maintained as key-sorted sparse vectors. This improves the programming efficiency and is a network efficient representation.
- Parameters and local data structures are communicated across nodes using key-range-based push and pull. This improves computational and network bandwidth efficiency.
- Server-nodes can execute UDFs on the partition-set of their parameters. This is a form of parallelization and improves compute efficiency. 
- Support for asynchronous tasks and specifying dependencies. Tasks are issued via RPCs. Tasks are by-default asynchronously executed. Caller continues its own workflow immediately after issuing a task and a callee executes tasks in parallel. However caller can serialize tasks by placing an execute-after-finished dependency across tasks.
- The system offers Flexible Consistency. The supported consistency models are: 
	- Sequential. Equivalent to a single-thread implementation as is the case in BSP.
	- Eventual. No dependency and hence no consistency guarantees.
	- Bounded Delay. A weak consistency wherein a task is blocked until tasks that started a fixed time (tau) before complete.
- Support for User-defined Filters, wherein only parameters that significantly alter the working model are propagated to the server nodes.
- Support for Range-based Vector Clocks that are efficient in terms of memory and network. Vector clocks are used for providing exactly-once semantics so as to discard duplicated messages.
- Key-list caching and value-compression. Key-list caching ensures all the keys belonging to a key-list need not be repetitively shared across nodes, instead can be identified via a single hash value. Many values can be null, value compression further reduces the on-network size of the payload between nodes.
- The system does Consistent Hashing. The servers manage well-defined key partitions. Partitioning is done using hash rings and associated direct mapped DHTs.
- Fault tolerance is ensured through synchronous replication of parameter partitions. Each server node stores replica of k counter-clockwise (in the hash ring) neighbor key-ranges. Replication is made efficient in terms of network usage via aggregation at the cost of delayed task reply.
- Elastic scalability is ensured via a well-defined protocol to add server- and worker-nodes at runtime and also handle node failures. The key partition is repartitioned or reassigned to handle the respective cases.