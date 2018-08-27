---
title: RabbitMQ 详解
---

# channel 参数详解

## basicPublish 方法

~~~java
/**
     * Publish a message.
     *
     * Publishing to a non-existent exchange will result in a channel-level
     * protocol exception, which closes the channel.
     *
     * Invocations of <code>Channel#basicPublish</code> will eventually block if a
     * <a href="http://www.rabbitmq.com/alarms.html">resource-driven alarm</a> is in effect.
     *
     * @see com.rabbitmq.client.AMQP.Basic.Publish
     * @see <a href="http://www.rabbitmq.com/alarms.html">Resource-driven alarms</a>.
     * @param exchange the exchange to publish the message to
     * @param routingKey the routing key
     * @param mandatory true if the 'mandatory' flag is to be set
     * @param immediate true if the 'immediate' flag is to be
     * set. Note that the RabbitMQ server does not support this flag.
     * @param props other properties for the message - routing headers etc
     * @param body the message body
     * @throws java.io.IOException if an error is encountered
     */
    void basicPublish(String exchange, String routingKey, boolean mandatory, boolean immediate, BasicProperties props, byte[] body)
            throws IOException;
~~~

## basicAck

deliveryTag: 该消息的index
multiple：是否批量.
true: 将一次性 ack 所有小于 deliveryTag 的消息。

## basicNack

channel.basicNack(delivery.getEnvelope().getDeliveryTag(), false, true);

deliveryTag: 该消息的 index
multiple：是否批量.
true: 将一次性拒绝所有小于 deliveryTag 的消息。
requeue：被拒绝的是否重新入队列

## basicReject

channel.basicReject(delivery.getEnvelope().getDeliveryTag(), false);

deliveryTag: 该消息的 index
requeue：被拒绝的是否重新入队列

channel.basicNack 与 channel.basicReject 的区别：
> basicNack可以拒绝多条消息，而basicReject一次只能拒绝一条消息