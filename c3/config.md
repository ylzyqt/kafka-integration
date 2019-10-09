# 3.2：config

### 1:配置预览

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

### 2: 配置详情

- **connection.url**

  ```
  connection.url=jdbc:mysql://xxx:3306/bingo?user=xxx&password=xxx
  ```

- **table.whitelist**

  ```
  控制jdbc-connector的读取白名单
  ```

- **connection.attempts**

  ```
  当接收到合法的connection.url后的尝试最大次数
  ```

- **table.blacklist**

  ```
  读取黑名单表，与table.whitelist表是互斥行为
  ```

- **mode**

  ```
  读取策略
  bulk 整块
  incrementing 自增字段
  timestamp 时间戳
  timestamp+incrementing 时间戳+字段
  ```

- **incrementing.column.name**

  ```
  自增长字段
  ```

- **timestamp.column.name**

  ```
  时间戳字段
  ```

- **poll.interval.ms**

  ```
  读取的时间间隔，默认是5000 ，即5秒
  ```

- **batch.max.rows**

  ```
  单次读取的最大行，默认100
  ```

- **table.poll.interval.ms**

  ```
  表结构的变更的检测间隔时间,默认60000 毫秒
  ```

- **topic.prefix**

  ```
  产生topic的前缀 + 表名 成为最后的topic
  ```

- **timestamp.delay.interval.ms**

  ```
  读取的时候的延迟数
  ```

- 