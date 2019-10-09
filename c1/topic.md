# 1.3：topic

### 1: 创建topic

```
./kafka-topics --create \ 
             --zookeeper zkAddress \ 
             --replication-factor 2 \ 
             --partitions 2 --topic mytopic
```





### 2: 修改topic

- 修改过期时间

  ```
  //1 修改过期时间
  ./kafka-topics --zookeeper zkAddress --alter --topic mytopic --config   retention.ms=86400000
  ```

- 修改分区数

  ```
  ./kafka-topics  --zookeeper zkAddress --alter --topic mytopic --partitions 3
  ```

  

- 修改最大可用字节数

  ```
  ./kafka-configs --zookeeper zdAddress --entity-type topics --entity-name mytopic --alter --add-config max.message.bytes=3145728
  
  ./kafka-configs --zookeeper zkAddress --entity-type topics --entity-name mytopic --alter --add-config max.partition.fetch.bytes=3145728
  ```



### 3:  查看topic

```
1. ./kafka-topics --list --zookeeper zkAddress

2. ./kafka-topics --describe --zookeeper  zkAddress --topic mytopic    
       
3. ./kafka-console-consumer --bootstrap-server kafkaBroker --topic mytopic --from-beginning    
```

