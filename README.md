# 功能修改
## 1. topic命名扩展至instance.schema.table，搜索 put2MapMessage
- connector/core/src/main/java/com/alibaba/otter/canal/connector/core/producer/MQMessageUtils.java
## 2. topic命名去除以下划线代替点的替换，搜索 entry.getKey().replace
-  connector/kafka-connector/src/main/java/com/alibaba/otter/canal/connector/kafka/producer/CanalKafkaProducer.java
-  connector/pulsarmq-connector/src/main/java/com/alibaba/otter/canal/connector/pulsarmq/producer/CanalPulsarMQProducer.java
-  connector/rabbitmq-connector/src/main/java/com/alibaba/otter/canal/connector/rabbitmq/producer/CanalRabbitMQProducer.java
-  connector/rocketmq-connector/src/main/java/com/alibaba/otter/canal/connector/rocketmq/producer/CanalRocketMQProducer.java
## 3. topic消息中增加file、pos元数据，搜索 public class FlatMessage
-  protocol/src/main/java/com/alibaba/otter/canal/protocol/FlatMessage.java