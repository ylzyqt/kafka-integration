# 3.1：command

### 1: 启动命令

```
export KAFKA_HEAP_OPTS="-Xmx5G -Xms5G"  # 堆内存
export GC_LOG_ENABLED="true"  # 开启GC日志
export GC_LOG_FILE_NAME="connect-gc.log" # GC日志名称
export LOG_DIR="/app/confluent/logs" # 日志目录
export KAFKA_JVM_PERFORMANCE_OPTS="-server -XX:MetaspaceSize=96m -XX:+UseG1GC -XX:MaxGCPauseMillis=20 -XX:InitiatingHeapOccupancyPercent=35 -XX:G1HeapRegionSize=16M -XX:MinMetaspaceFreeRatio=50 -XX:MaxMetaspaceFreeRatio=80" # JVM performance 调优
export KAFKA_JMX_OPTS="-Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.port=9001  -Dcom.sun.management.jmxremote.authenticate=false  -Dcom.sun.management.jmxremote.ssl=false " # JMX 配置

./connect-distributed -daemon ../etc/schema-registry/connect-avro-distributed.properties
```



### 2: 查看当前的connectors

```
./confluent list connectors

输出结果
connect is [DOWN]
Bundled Predefined Connectors (edit configuration under etc/):
  elasticsearch-sink
  file-source
  file-sink
  jdbc-source
  jdbc-sink
  hdfs-sink
  s3-sink
  
这里碰到connect is [DOWN]  的情况比较另类，是因为没有启动，我停掉了所有的组件，使用
confluent start之后，即可。
```



### 3: 加载jdbc-connectors quick start

- 修改source-quickstart-sqlite.properties

  ```
  name=mysql-whitelist-timestamp-source
  connector.class=io.confluent.connect.jdbc.JdbcSourceConnector
  tasks.max=10
  
  connection.url=jdbc:mysql://xxx:3306/bingo?user=xxx&password=xxx
  table.whitelist=user_event_log
  
  mode=timestamp+incrementing
  timestamp.column.name=ts
  incrementing.column.name=id
  
  topic.prefix=mysql-zhudongquan-jdbc-connector
  ```

  

- 启动

  ```
  ./confluent load jdbc-source
  默认的配置是读取source-quickstart-sqlite.properties
  ```

  

- 返回结果

  ```
  {
    "name": "jdbc-source",
    "config": {
      "connector.class": "io.confluent.connect.jdbc.JdbcSourceConnector",
      "tasks.max": "10",
      "connection.url": "jdbc:mysql://xxx:3306/bingouser=xxx&password=xxx",
      "table.whitelist": "user_event_log",
      "mode": "timestamp+incrementing",
      "timestamp.column.name": "ts",
      "incrementing.column.name": "id",
      "topic.prefix": "mysql-zhudongquan-jdbc-connector",
      "name": "jdbc-source"
    },
    "tasks": [],
    "type": null
  }
  ```

  

