# 1.2：install

### 1: 安装版本

```
confluent 4.0.0
sudo nohup wget http://packages.confluent.io/archive/4.0/confluent-oss-4.0.0-2.11.zip &
```



### 2: 修改配置文件

```
1. advertised.listener
2. zookeeper
3. log.dir
```





### 3: 启停命令

```
sh zkServer.sh start
```



```
1: kafka start:  
 ./kafka-server-start -daemon ../etc/kafka/server.properties

2: kafka stop :  
 ./kafka-server-stop 
```

