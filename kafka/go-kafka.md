# Golang Kafka 使用
## Kafka 名词解释
1. 消息记录：由一个key，一个value和一个时间戳构成，消息最终存储在主题下的分区中，记录在生产中称为生产者记录，在消费者中称为消费记录。Kafka集群保持了所有发布的消息，直到它们过期，无论消息是否被消费了，在一个可配置的时间段内，Kafka集群保留了所有发布的消息。比如消息的保存策略被设置为2天，那么在一个消息被发布的两天时间内，它都是可以被消费的。Kafka的性能是和数据量无关的常量级的，所以保留太多数据并不是问题
2. 生成者：生产者用于发布消息
3. 消费者：消费者用于订阅消息
4. 消费者组：相同的groupID的消费者将视为同一个消费者组，每个消费者都需要设置一个组id，每条消息只能被consumer group中的一个Consumer消费，但是可以被多个consumer group消费
5. 主题（topic）：消息的一种逻辑分组，用于对消息分门别类，每一类消息称之为一个主题，相同主题的消息放在一个队列中
6. 分区（partition）：消息的一种物理分组，一个主题被拆成多个分区，每一个分区就是一个顺序的，不可变的消息队列，并且可以持续添加，分区中的每个消息都被分配了一个唯一的id，称之为偏移量（offset），在每个分区中偏移量都是唯一的。每个分区对应一个逻辑log，有多个segment组成
7. 偏移量：分区中每个消息都有一个唯一的Id，称之为偏移量，代表已经消费的位置
8. 代理（broker）：一台kafka服务器称之为一个broker
9. 副本（replica）：副本只是一个分区（partition）的备份。副本不读取或写入数据。它们用于防止数据丢失
10. 领导者：leader是负责给定分区的所有读取和写入的节点
11. 追随者：跟随领导者指令的节点被称为Follower。
12. zookeeper：Kafka代理是无状态的，所以它们使用Zookeeper来维护它们的集群状态。Zookeeper用于管理和协调Kafka代理

## Kafka 功能
1. 发布订阅：生产者生产消息（数据流），将消息发送给kafka指定的主题队列中，也可以发送到topic中的指定分区中，消费者从kafka的指定队列中获取消息，然后来处理消息