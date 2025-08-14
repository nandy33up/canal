# 功能修改
## 1.topic命名扩展至instance.schema.table，搜索 put2MapMessage
- connector/core/src/main/java/com/alibaba/otter/canal/connector/core/producer/MQMessageUtils.java
  
## 2.topic命名去除以下划线代替点的替换，搜索 entry.getKey().replace
-  connector/kafka-connector/src/main/java/com/alibaba/otter/canal/connector/kafka/producer/CanalKafkaProducer.java
-  connector/pulsarmq-connector/src/main/java/com/alibaba/otter/canal/connector/pulsarmq/producer/CanalPulsarMQProducer.java
-  connector/rabbitmq-connector/src/main/java/com/alibaba/otter/canal/connector/rabbitmq/producer/CanalRabbitMQProducer.java
-  connector/rocketmq-connector/src/main/java/com/alibaba/otter/canal/connector/rocketmq/producer/CanalRocketMQProducer.java

## 3.topic消息中增加file、pos元数据，搜索 public class FlatMessage
-  protocol/src/main/java/com/alibaba/otter/canal/protocol/FlatMessage.java

# 编译打包
## 1.编译
```shell
mvn clean package -DskipTests
```

## 2.打包
```shell
tar -czvf canal-server-1.1.9.tar.gz -C deployer/target --transform='s/canal/canal-server-1.1.9/' canal
tar -czvf canal-admin-1.1.9.tar.gz -C admin/admin-web/target --transform='s/canal-admin/canal-admin-1.1.9/' canal-admin
```

# 更新升级
## 1.更新配置
```shell
cp canal-admin-1.1.8/conf/application.yml canal-admin-1.1.9/conf/application.yml
cp canal-admin-1.1.8/conf/canal-template.properties canal-admin-1.1.9/conf/canal-template.properties
cp canal-admin-1.1.8/conf/instance-template.properties canal-admin-1.1.9/conf/instance-template.properties

cp canal-server-1.1.8/conf/canal_local.properties canal-server-1.1.9/conf/canal_local.properties

vim canal-server-1.1.8/conf/logback.xml
# 增加instance消费点位日志打印，定位到文件最后一行
# <root level="WARN"> 修改为 <root level="INFO">
```

## 2.服务重启
```shell
sh canal-server-1.1.8/bin/stop.sh
sh canal-admin-1.1.8/bin/stop.sh

sh canal-admin-1.1.9/bin/startup.sh
sh canal-server-1.1.9/bin/startup.sh local
```