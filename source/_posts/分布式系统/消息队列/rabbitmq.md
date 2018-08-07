---
title: RabbitMQ 详解
---

# channel 参数详解

# basicReject

channel.basicReject(delivery.getEnvelope().getDeliveryTag(), false);

deliveryTag:该消息的index
requeue：被拒绝的是否重新入队列

channel.basicNack 与 channel.basicReject 的区别在于basicNack可以拒绝多条消息，而basicReject一次只能拒绝一条消息