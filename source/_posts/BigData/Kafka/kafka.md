---
title: kafka 详解
---

# kafka 基本知识

Kafka的架构和涉及到的名词：

1. Topic ：用于划分 Message 的逻辑概念，一个 Topic 可以分布在多个 Broker 上。
2. Partition：是 Kafka 中横向扩展和一切并行化的基础，每个T opic 都至少被切分为 1 个 Partition。
3. Offset：消息在 Partition 中的编号，编号顺序不跨 Partition。
4. Consumer：用于从 Broker 中取出/消费 Message。
5. Producer：用于往 Broker 中发送/生产 Message。
6. Replication：Kafka 支持以 Partition 为单位对 Message 进行冗余备份，每个 Partition 都可以配置至少 1 个 Replication (当仅 1 个 Replication 时即仅该 Partition 本身)。
7. Leader：每个 Replication 集合中的 Partition 都会选出一个唯一的 Leader，所有的读写请求都由 Leader 处理。其他 Replicas 从 Leader 处把数据更新同步到本地，过程类似大家熟悉的 MySQL 中的 Binlog 同步。
8. Broker：Kafka 中使用 Broker 来接受 Producer 和 Consumer 的请求，并把 Message 持久化到本地磁盘。每个 Cluster 当中会选举出一个 Broker 来担任 Controller ，负责处理 Partition 的 Leader 选举，协调 Partition 迁移等工作。
9. ISR(In-Sync Replica)：是 Replicas 的一个子集，表示目前 Alive 且与 Leader 能够 “Catch-up” 的 Replicas 集合。由于读写都是首先落到 Leader 上，所以一般来说通过同步机制从Leader 上拉取数据的 Replica 都会和 Leader 有一些延迟(包括了延迟时间和延迟条数两个维度)，任意一个超过阈值都会把该 Replica 踢出 ISR。每个 Partition 都有它自己独立的 ISR。

# kafka 应用场景

kafka 作为时下最流行的开源消息系统，被广泛地应用在数据缓冲、异步通信、汇集日志、系统解耦等方面

# kafka 如何实现每秒几十万的高并发写入

Kafka 是高吞吐低延迟的高并发、高性能的消息中间件，在大数据领域有极为广泛的运用。配置良好的 Kafka 集群甚至可以做到每秒几十万、上百万的超高并发读取和写入。

## 页面缓存技术

kafka 为了保证数据写入性能，基于操作系统的页缓存（page cache 为了处理块设备和内存交互时高速访问的问题）来实现文件写入。

## 磁盘顺序写



## 零拷贝技术


> 参考资料
>
>[kafka 高吞吐量性能揭秘](https://blog.csdn.net/stark_summer/article/details/50144591 )
>
>[Linux 内核的文件 Cache 管理机制介绍](https://www.ibm.com/developerworks/cn/linux/l-cache/index.html)
>
>[Page Cache](https://en.wikipedia.org/wiki/Page_cache)
>
>[Linux系统中的Page cache和Buffer cache](https://zhuanlan.zhihu.com/p/35277219)