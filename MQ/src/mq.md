
### RocketMQ如何保证消息有序性？
- 全局有序？ 不支持，除非只有一个队列
- 局部有序？ 也就是组内有序（单个队列有序）
  - 消息发送有序 ：RocketMQ 顺序消息的原理是在 Producer 端把一批需要保证顺序的消息发送到同一个 MessageQueue
  - 消息存储有序：MQ自己保证
  - 消息消费有序：Consumer 端则通过加锁的机制来保证消息消费的顺序性，Broker 端通过对 MessageQueue 进行加锁，保证同一个 MessageQueue 只能被同一个 Consumer 进行消费。
- 可能的问题？
  - 有顺序性的消息需要发送到同一个 MessageQueue，可能导致单个 MessageQueue 消息量很大，而 Consumer 端消费的时候只能单线程消费，很可能导致当前 MessageQueue 消息积压；
  - 如果顺序消息 MessageQueue 所在的 broker 挂了，这时 Producer 只能把消息发送到其他 Broker 的 MessageQueue 上，而如果新的 MessageQueue 被其他 Consumer 消费，这样两个 Consumer 消费的消息就不能保证顺序性了。
如下图：![img.png](img.png)

