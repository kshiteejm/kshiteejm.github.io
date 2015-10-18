---
layout: post
title: Major Technical Advancements in Apache Hive
description: 
tags: paper-summary sql-on-hadoop
comments: true
---

Takeaways from *Major technical advancements in Apache Hive, Huai et al, SIGMOD, 2014.*

### Hive and Advancements Therein
Hive is a translation layer that converts its own dialect of SQL to DAG of MR jobs.  
Due to increased adoption, increasing data volume, increasing workloads and demanding use cases (interactive workloads) that Hive is being put to use for, several shortcomings were realized and are being addressed in this paper.  

### Hive Architecture:

- CLI & HiveServer2 receive statements
- Driver generates Abstract Syntax Tree 
- Planner converts Abstract Syntax Tree to an Optimized Operator Tree
- Task Compiler converts the Operator Tree to DAG of MR jobs
- Execution Unit does further optimization and hands over MR jobs to Execution Engine (example: MR in Hadoop)
- (De)Serializer for conversion to or from a Hive-specific file format stored on HDFS for the Execution Engine
 
### Shortcomings and Improvements

File Format and Memory Management

- Shortcoming: Data-type agnostic file formats and one-row-at-a-time serialization leading to storage inefficiency and slow performance
- Improvements: 
	- Improved File Format called Optimized Record Columnar (ORC) File.
	- Table Placement.
		* Larger default stripe size (256 MB) for efficient disk reads.
		* Column decomposition to achieve pinpointed reads.
		* Preventing remote reads by aligning stripe boundaries to HDFS block boundaries.
	- Indexes.
		* Data Statistics. File-level, Stripe-level and Index Group-level data statistic indexes. Avoids wasteful reads and also helps in query optimization.
		* Position Pointers. To efficiently locate indexes of Stripes and Index Groups.
	- Compression. Two-level compression scheme. Data-type aware compression scheme followed by optional general compression scheme.
	- Memory Manager. Stripe size for each writer is minimum of default stripe size or the ratio of memory threshold to number of writers.
 
Query Planning

- Shortcomings: Unnecessary Map phases, data loading and data re-partitioning
- Improvements:
	- Elimination of Unnecessary Map phases. Coalescing consecutive Map phases into one, specifically as observed in the case of Map Joins (when a reduce operation is done via a Map job by sending the smaller table along with each Map task avoiding a shuffle phase)
	- Correlation Optimizer.
		* Avoiding Reduce Sink Operators (RSOps) and the corresponding shuffle by correlating RSOps based on similarity in sort order, partitioning and number of reducers.
		* Introduction of Demux and Mux Operators to handle assignment of output rows from reducers to different major operators (join, groupBy and the likes).
		* Coordination mechanism to signal start and end buffering of incoming rows at a major operator.
 
Query Execution

- Shortcomings: Lazy deserialization and one-row-at-a-time processing model led to slow execution pipeline and inability to exploit parallelism offered by modern CPUs
- Improvements:
	- Vectorized Query Execution. Execution in batches by converting one-row-at-a-time execution model to batched-row-at-a-time execution model. Lookahead deserialization based on filters and projections avoiding unnecessary reads.
	- Vectorized Expression. To complement Vectorized Query Execution and achieve parallelism on modern CPUs, each operation on batched rows is achieved via custom-written expressions. These expressions use tight loops with no conditionals and interdependence across iterations of the loop. Such loops can be parallelized on modern CPUs (superscalar instruction pipelines). Conditionals are indirectly achieved by providing an array that points to the relevant rows of each column that need to be iterated upon.

----- 

[Apache Calcite: Cost-Based Optimizer (CBO)](http://hortonworks.com/blog/hive-0-14-cost-based-optimizer-cbo-technical-overview/)

### Join ordering optimization. 
CBO finds the join order that results in the biggest reduction of intermediary rows as early as possible in the query plan tree. CBO achieves this via joint knowledge of query filters and the Indexes (Data Statistics and Position Pointers) to estimate the amount of reduction for different join orderings.
 
### Bushy Join Support.
CBO preferentially generates bushy query plan trees to enable parallel execution of data operators. Bushy join support in tandem with optimized join ordering improves query performance by a great deal.
 
### Join Simplification.
CBO identifies duplicated joins and pushes down join predicates. This is reminiscent of a bottoms-up approach rather than a top-down approach where a costly cross-product is performed followed by application of the predicates.