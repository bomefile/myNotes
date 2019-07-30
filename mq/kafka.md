# zookeeper 启动配置
运行zkServer.cmd
# kafka 启动配置
 .\bin\windows\kafka-server-start.bat .\config\server.properties

kafka启动配置 
zookeeper-server-start /usr/local/etc/kafka/zookeeper.properties & kafka-server-start /usr/local/etc/kafka/server.properties

nohup ./bin/kafka-server-start.sh ./config/server.properties & ./bin/zookeeper-server-start.sh ./config/zookeeper.properties &

依赖工程：spring-kafka的samples

[win配置参考地址](https://www.cnblogs.com/lnice/p/9668750.html)

## 管理kafka
1. 创建topic
````
kafka-topics --zookeeper localhost:2181 --create --topic "demo-topic-1" \
> --replication-factor 1 --partitions 1
Created topic demo-topic-1.
````

2. 查看topic列表

````
./kafka-topics.sh  --zookeeper localhost:2181 --list
````

3. 删除topics

````
kafka-topics --zookeeper localhost:2181 
--delete --topic demo-topic-1
````
4. 列出消费者群组

````
kafka-consumer-groups --zookeeper localhost:2181 

````
> 注意：上述安装环境为本机
## kafka简介

### 发布订阅

### kafka核心概念


1. producer：
消息生产者，发布消息到 kafka 集群的终端或服务。
2. broker：
kafka 集群中包含的服务器。
3. topic：
每条发布到 kafka 集群的消息属于的类别，即 kafka 是面向 topic 的。
4. partition：
partition 是物理上的概念，每个 topic 包含一个或多个 partition。kafka 分配的单位是 partition。
5. consumer：
从 kafka 集群中消费消息的终端或服务。
6. Consumer group：
high-level consumer API 中，每个 consumer 都属于一个 consumer group，每条消息只能被 consumer group 中的一个 Consumer 消费，但可以被多个 consumer group 消费。
7. replica：
partition 的副本，保障 partition 的高可用。
8. leader：
replica 中的一个角色， producer 和 consumer 只跟 leader 交互。
9. follower：
replica 中的一个角色，从 leader 中复制数据。
10. controller：
kafka 集群中的其中一个服务器，用来进行 leader election 以及 各种 failover。
12. zookeeper：
kafka 通过 zookeeper 来存储集群的 meta 信息。
13. replication-factor
每个partition的副本个数。任意将每一个分区复制到n个broker上。

### KAFKA高性能
- 其一，Kafka 集群可以通过增删 Broker 实集群级的水平扩展。
- 其二，通过对 Topic 进行分区，实现了应用级别的无限平行扩展能。
- 其三，通过优良通讯协议，实现了生产系统直接与后端的 Broker 进行通讯，节省了代理，不仅减少了数据链路长度降低了延迟，而且极大的降低了成本。
- 页缓存 + 磁盘顺序写
- 零拷贝技术
- Broker NIO 异步消息处理，实现IO线程与业务线程分离

https://cloud.tencent.com/developer/article/1032487

https://www.cnblogs.com/davidwang456/articles/7884677.html

## KafkaTemplate 配置 消息生产者配置

````
    @Bean(name = "timelineKafkaTemplate")
    public KafkaTemplate<String, String> timelineKafkaTemplate() {
        Map<String, Object> configProps = new HashMap<>();
        configProps.put(ProducerConfig.BOOTSTRAP_SERVERS_CONFIG, bootstrapServers);
        configProps.put(ProducerConfig.KEY_SERIALIZER_CLASS_CONFIG, StringSerializer.class);
        configProps.put(ProducerConfig.VALUE_SERIALIZER_CLASS_CONFIG, StringSerializer.class);
        configProps.put(ProducerConfig.PARTITIONER_CLASS_CONFIG, "com.sayabc.onlineclassroom.timeline.configuration.TimelinePartitioner");
        return new KafkaTemplate<>(new DefaultKafkaProducerFactory<>(configProps));
    }
````

##  kafka消费者配置

````
    @Bean
    public ConcurrentKafkaListenerContainerFactory<?, ?> kafkaListenerContainerFactory(
            ConcurrentKafkaListenerContainerFactoryConfigurer configurer,
            ConsumerFactory<Object, Object> kafkaConsumerFactory,
            KafkaTemplate<Object, Object> template) {

        ConcurrentKafkaListenerContainerFactory<Object, Object> factory = new ConcurrentKafkaListenerContainerFactory<>();
        configurer.configure(factory, kafkaConsumerFactory);
        factory.setBatchListener(true);
        factory.setMessageConverter(batchConverter());
        return factory;
    }

    @Bean
    public BatchMessagingMessageConverter batchConverter() {
        return new BatchMessagingMessageConverter(converter());
    }

    @Bean
    public RecordMessageConverter converter() {
        return new StringJsonMessageConverter();
    }

````
