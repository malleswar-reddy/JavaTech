
```
$ brew cask install java
$ brew install kafka
```



Now start Zookeeper and Kafka:

Start Zookeeper:
```
$ zookeeper-server-start /usr/local/etc/kafka/zookeeper.properties
```

Start Kafka server:
```command 
$ kafka-server-start /usr/local/etc/kafka/server.properties
```

WARNING:

During server start, you might be facing connection broken issue.
```logs
[2018-08-28 16:24:41,166] WARN [Controller id=0, targetBrokerId=0] Connection to node 0 could not be established. Broker may not be available. (org.apache.kafka.clients.NetworkClient)
[2018-08-28 16:24:41,268] WARN [Controller id=0, targetBrokerId=0] Connection to node 0 could not be established. Broker may not be available. (org.apache.kafka.clients.NetworkClient)
```
To fix this issue, we need to change the server.properties file.

```
$ vim /usr/local/etc/kafka/server.properties

listeners=PLAINTEXT://:9092

```

Create Kafka Topic:

```
$ kafka-topics --create --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 --topic test
```
Here we have created a topic name test


```
$ kafka-console-producer --broker-list localhost:9092 --topic test
```

send first message<br>
send second message</br>
wow it is working

```
$ kafka-console-consumer --bootstrap-server localhost:9092 --topic test --from-beginning
```
send first message </br>
send second message</br>
wow it is working


