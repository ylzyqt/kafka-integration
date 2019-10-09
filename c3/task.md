# 3.4 :  管理 tasks

### 1: 查找connectors

```
查找connectors
curl http://localhost:8083/connectors/
```





### 2: 查看具体的tasks

- tasks详情

  ```
  curl http://localhost:8083/connectors/mysql-whitelist-timestamp-source/tasks |jq
  ```

  

- tasks状态

  ```
  curl http://localhost:8083/connectors/mysql-whitelist-timestamp-source/tasks/0/status | jq
  ```

  

- tasks重启

  ```
  curl -X POST http://localhost:8083/connectors/mysql-whitelist-timestamp-source/tasks/0/restart
  ```







