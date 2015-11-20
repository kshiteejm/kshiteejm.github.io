---
layout: post
title: Project Adam&#58; Building an Efficient and Scalable Deep Learning Training System.
description:
tags: paper-summary-big-data-machine-learning
comments: true
---

Takeaways from *Project Adam: Building an Efficient and Scalable Deep Learning Training System, Chilimbi et al, OSDI, 2014.*

### Problem.

Large Scale Deep Learning. Learning a model is essentially calculating a set of parameters (weights w) iteratively (multiple epochs) to reduce error. 
 
Project Adam tackles this by implementing a scalable distributed deep learning training system using commodity servers. The key principles used are a ground-up system design, effective partitioning of data and compute, making everything asynchronous (as the DNNs tolerate inconsistencies), and heavy system optimization.
 
### Architecture.

- Data Serving machines that serve input
- Model Training machines that asynchronously update the shared model (i.e. parameters).
- Global Parameter Server (PS) that store parameters.
	- PS controllers.
	- PS nodes.
 
### Features.

Data Serving.

- Augment pre-transformed training data.
- Pre-cache training data to be served next to the model training machines.
 
Model Training.

- Vertically partition the model across the various model training machines.
- Multi-threading the model updates for different images on each training machine.
- Each thread has an associated NUMA-aware context (weights and activations) and scratch buffer. 
- Local model updates (across threads) are updated in a lock-free asynchronous manner.
- A uniform interface for both local- and remote- data copy. The interface accepts a data pointer which is handed over locally (avoids memory copy) or copied (the data being pointed to) remotely.
- Model partitioning is done so the working set for each partition fits in L3 cache. Also optimized modules are used for column- or row-major operations.
- Need for straggler mitigation is evaded by allowing threads to work on multiple images in parallel and ending an epoch based on the threshold of input images (randomized order) processed.
- Batching of parameter updates from model training machines to parameter server machines is done. Batched weight updates for several machines are sent in case of convolutional layers as the volume of weights is low due to sharing. Batched activations and error gradients are sent in case of fully connected layers so as to reduce network volume. This also results in offloading compute as the weights are calculated at parameter servers.
 
### Global Parameter Server.

- Model parameters are divided as 1MB shards and several shards are bucketed equally among several PS machines for load balancing.
- Parameter updates are opportunistically batched so that sufficient contiguity in updates relieves L3 cache pressure.
- NUMA-aware localization for operations on each shard is done and lock-free data structures and memory allocation mechanism is used.
- Asynchronous write-back of updated parameters is done. This also helps folding several updates into the latest single update.
- Fault tolerance is achieved via replication of each parameter shard to three machines. The PS controller manages assignment of parameter shard replicas and is itself fault tolerant as it is in a Paxos cluster. Heartbeats within and across PS machines and controllers are used for liveness monitoring.