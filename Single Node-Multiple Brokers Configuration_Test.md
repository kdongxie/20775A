# Single Node-Multiple Brokers Configuration_Test

## Multiple Kafka Brocker

config/server-one.properties
broker.id=1
port=9093
log.dirs=/tmp/kafka-logs-1

config/server-two.properties
broker.id=2
port=9094
log.dirs=/tmp/kafka-logs-2

* Start Multiple Brocker
  Broker1
  bin/kafka-server-start.sh config/server.properties
  Broker2
  bin/kafka-server-start.sh config/server-one.properties
  Broker3
  bin/kafka-server-start.sh config/server-two.properties

* Creating a Topic
  bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 3 
  -partitions 1 --topic Multibrokerapplication

bin/kafka-topics.sh --describe --zookeeper localhost:2181 -> describe command = checking
--topic Multibrokerapplication

* Start Producer to Send Messages
  bin/kafka-console-producer.sh --broker-list localhost:9092 --topic Multibrokerapplication

* Start Consumer to Receive Messages
  bin/kafka-console-consumer.sh --zookeeper localhost:2181 --topic Multibrokerapplication --from-beginning

* Modifying a Topic
  bin/kafka-topics.sh --zookeeper localhost:2181 --alter --topic Hello-kafka --partitions 2
* Deleting a Topic
  bin/kafka-topics.sh --zookeeper localhost:2181 --delete --topic Hello-kafka