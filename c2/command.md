# 2.1：command

### 1 ： 启动命令:

```
1: schema start: 
 ./schema-registry-start -daemon ../etc/schema-registry/schema-registry.properties
```



### 2: 基本操作命令

- 获得所有的schema主体信息

  ```
  curl http://localhost:8081/subjects
  ```

- 手动创建schema信息

  ```
  curl -X POST -H "Content-Type: application/json" \
      --data '{"schema": "{\"type\": \"string\"}"}' \
      http://localhost:8081/subjects/console_test/versions
  ```

- 查看schema主体版本信息

  ```
  curl http://localhost:8081/subjects/console_test/versions
  ```

- 查看schema各版本详情

  ```
  curl http://localhost:8081/subjects/console_test/versions/1
  ```

- 删除schema信息

  ```
  curl -X DELETE -H "Content-Type:application/json" http://localhost:8081/subjects/my-avro-demo-value/
  ```

- 以ids查看版本信息

  ```
  curl -X GET http://localhost:8081/schemas/ids/167
  ```

