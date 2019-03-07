---
title: kafka 详解
---

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
>[Linux 内核的文件 Cache 管理机制介绍](https://www.ibm.com/developerworks/cn/linux/l-cache/index.html)
>
>[Page Cache](https://en.wikipedia.org/wiki/Page_cache)
>
>[Linux系统中的Page cache和Buffer cache](https://zhuanlan.zhihu.com/p/35277219)