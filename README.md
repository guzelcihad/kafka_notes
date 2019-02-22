# kafka_notes
Includes Apache Kafka Notes

* Installed on ```/usr/local``` directory.
* ```/kafka/libs``` contains all of the dependencies kafka has to run. 
* ```/kafka/config``` contains all of the config files to configure Apache Kafka.
<br/> ```server.properties``` file is a configuration file about Kafka broker.
* ```kafka/bin``` folder , contains all of the programs get Kafka up and running in a variety of capacities.
* ```kafka/bin/windows``` includes batch files. 

# Message Retention Policy
Apacke Kafka retains all published messages regardless of consumption
* Retention period is configurable
<br/> Default is 168 hours or seven days. 
<br/> Retention period is defined on a per-topic basis.

# Starting Kafka
To be able to use Kafka, first start the main components of the cluster. Those are Zookeper instance and at least one broker.
<br/> To starting Zookeper, there is a shell program provided by Kafka. 
* Start Zookeper
<br/>Go to ```/usr/local/kafka/``` and run ```bin/zookeeper-server-start.sh config/zookeeper.properties```
<br/>To check Zookeper is running succesfully, open another terminal and type command ```telnet localhost 2181``` 
and then ```stat```. This will give us the status of Zookeper.
* Start Kafka. Type command ```bin/kafka-server-start.sh config/server.properties```.
<br/>```

### Create Topic
* Now it is time to create a topic. For this ``` bin/kafka-topics.sh --create --topic my_topic --zookeeper localhost:2181 
--replication-factor 1 --partitions 1```. We specified a spesific zookeper to run. It can be multiple zookeeper on cluster.
<br/>First, Zookeper scanned its registry of brokers, and made a decision to assign a broker as the leader for the topic, my_topic.
<br/>Second, on the broker, there is a logs directory, and in there there is a new directory was created called my_topic-0.
<br/>Within this directory, there are two files, an index file and the log file.
<br/>Directory is in the path ```/tmp/kafka-logs/my_topic-0```.
* List topics in broker, type command : ```bin/kafka-topics.sh --list --zookeeper localhost:2181```

### Produce Messages
* First thing is to instantiate a producer, type command ```bin/kafka-console-producer.sh --broker-list localhost:9092 --topic my_topix```
<br/> Now it is ready for publish messages in terminal, enter some message and then press enter.

### Consume Messages
* Open another terminal window and type command ```bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic my_topic --from-beginning```

