# Single Node-Single Broker Configuration_Test

wget https://archive.apache.org/dist/kafka/1.0.1/kafka_2.11-1.0.1.tgz

tar xvfz kafka_2.11-1.0.1.tgz

* Start Kafka
  bin/kafka-server-start.sh config/server.properties
* Stop Kafka
  bin/kafka-server-stop.sh config/server.properties

* single node-single broker
  bin/zookeeper-server-start.sh config/zookeeper.properties
  bin/kafka-server-start.sh config/server.properties

* Create Topic
  bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic Hello-Kafka

* List of Topics
  bin/kafka-topics.sh --list --zookeeper localhost:2181

* Start Producer to Send Messages
  bin/kafka-console-producer.sh --broker-list localhost:9092 --topic Hello-Kafka

* Start Consumer to Receive Messages
  bin/kafka-console-consumer.sh --zookeeper localhost:2181 --topic Hello-Kafka --from-beginning