# 3.2 :  管理 connector

### 1: 获取当前所有的connectors

```
curl http://localhost:8083/connectors
```



### 2: 查看具体的connector

- 查看具体的connector

  ```
  curl http://localhost:8083/connectors/jdbc-source
  ```

- 查看具体的connector配置

  ```
  curl http://localhost:8083/connectors/jdbc-source/config
  ```

- 查看具体的connector状态

  ```
  curl http://localhost:8083/connectors/jdbc-source/status 
  ```

### 3： 过程操控

  <font color red>topic为 topic.prefix+表名称</font>

- 创建 

  ```
  curl -X POST http://localhost:8083/connectors -H 'Content-Type: application/json' --data '{  
       "name": "mysql-whitelist-timestamp-source", 
       "config":{
          "connector.class": "io.confluent.connect.jdbc.JdbcSourceConnector",
          "connection.url":"jdbc:mysql://xxx:3306/bingo?user=xx&password=xx",
          "tasks.max": "10",
          "batch.max.rows": "1000",
          "table.whitelist": "event_log",
          "mode": "incrementing",
          "incrementing.column.name": "seq",
          "topic.prefix": "databus.event",
          "key.converter": "org.apache.kafka.connect.storage.StringConverter",
          "value.converter": "io.confluent.connect.avro.AvroConverter",
          "key.converter.schema.registry.url": "http://localhost:8081",
          "value.converter.schema.registry.url": "http://localhost:8081",
          "transforms": "setSchema",
          "transforms.setSchema.type": "org.apache.kafka.connect.transforms.SetSchemaMetadata$Value",
          "transforms.setSchema.schema.name": "com.wosai.schema.demo.MyUserEventLog"
     }
   }'
  ```

- 修改

  ```
    curl -X PUT http://localhost:8083/connectors/mysql-whitelist-timestamp-source/config  -H 'Content-Type: application/json' --data '{  
          "connector.class": "io.confluent.connect.jdbc.JdbcSourceConnector",
          "connection.url":"jdbc:mysql://xxx:3306/bingo?user=xx&password=xx",
          "tasks.max": "10",
          "batch.max.rows": "1000",
          "table.whitelist": "user_event_log",
          "mode": "incrementing",
          "incrementing.column.name": "seq",
          "topic.prefix": "zzzd_",
          "key.converter": "org.apache.kafka.connect.storage.StringConverter",
          "value.converter": "io.confluent.connect.avro.AvroConverter",
          "key.converter.schema.registry.url": "http://localhost:8081",
          "value.converter.schema.registry.url": "http://localhost:8081",
          "transforms": "setSchema",
          "transforms.setSchema.type": "org.apache.kafka.connect.transforms.SetSchemaMetadata$Value",
          "transforms.setSchema.schema.name": "com.wosai.schema.demo.MyUserEventLog"
  
   }'
   
  ```

- 重启

  ```
  curl -X POST http://localhost:8083/connectors/jdbc-source/restart
  ```

- 暂停

  ```
  curl -X PUT http://localhost:8083/connectors/jdbc-source/pause
  ```

- 恢复

  ```
  curl -X PUT http://localhost:8083/connectors/jdbc-source/resume
  ```

- 删除

  ```
  curl -X DELETE http://localhost:8083/connectors/jdbc-source/
  ```

- 

  ```
  验证:
  sudo ./kafka-avro-console-consumer --bootstrap-server localhost:9092 --topic zdqzdquser_event_log --from-beginning
  ```

  

  



