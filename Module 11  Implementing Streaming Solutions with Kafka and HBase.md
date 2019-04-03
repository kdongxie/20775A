# Module 11 : Implementing Streaming Solutions with Kafka and HBase
## Module Overview

- Building and deploying a Kafka cluster
- Publishing, consuming, and processing data using the Kafka APIs
- Using <u>HBase</u> to store and query data

### Kafka cluster environment (pic)

![image](https://user-images.githubusercontent.com/46669551/55211195-56381500-522e-11e9-827d-da7752cb4be1.png)

## Lesson 1: Building and deploying a Kafka cluster
- What is a Kafka cluster?
- How Kafka publishes data
- Creating a Kafka cluster
- Configuring mirroring
- Managing and monitoring Kafka
- Demonstration: Creating, configuring, and mirroring a Kafka cluster on
  HDInsight

### What is a Kafka cluster? (pic)

![image](https://user-images.githubusercontent.com/46669551/55210695-15d79780-522c-11e9-8946-fd1fa4d3b4e7.png)

### How Kafka publishes data (pic)

![image](https://user-images.githubusercontent.com/46669551/55210716-2be55800-522c-11e9-9178-4a5a2054c58e.png)

### Creating a Kafka cluster

- Create HDInsight Storm cluster
  - Kafka preinstalled
  - Configure using Ambari
  - Remove Storm service if not required 

- A Kafka broker is installed on each supervisor node, by default

- To add or remove brokers, use Ambari console to stop and uninstall the Kafka service

### Configuring mirroring (pic)

![image](https://user-images.githubusercontent.com/46669551/55210751-4b7c8080-522c-11e9-98cc-f17c9eede70c.png)

### Managing and monitoring Kafka

Ambari console:

- Summary dashboard:
  - FQDNs for the Kafka broker nodes
  - By default one broker node for each Storm Supervisor node
  - Broker node names <node>xxxxx.internal.cloudapp.net

- Configs pane
- Service Actions
  - Maintenance mode

- Actions

## Demonstration: Creating, configuring, and mirroring a Kafka cluster on HDInsight
In this demonstration, you will see how to:

- Create an HDInsight cluster that includes Kafka
- Configure a Kafka cluster using Ambari
- Use MirrorMaker to mirror a cluster
- Monitor mirroring activity

## Lesson 2: Publishing, consuming, and processing data using the Kafka APIs
- Sending events to Kafka
- Demonstration: Configuring remote access to a Kafka cluster
- Consuming Kafka events
- Performing stream processing
- Visualizing stream processing results
- Limitations of Kafka
- Connecting to a Kafka cluster from a remote client
- Demonstration: Visualizing data with Kafka clusters and Power BI

### Sending events to Kafka

- Kafka events are key/value pairs
- All sending is asynchronous
  - The producer can perform limited internal buffering to optimize network utilization

- Basic Kafka producers

  - KafkaProducer object
    - Properties

  - ProducerRecord
  - Send method
  - RecordMetadata
  - Close method

## Demonstration: Configuring remote access to a Kafka cluster
- In this demonstration, you will see how to start the process of configuring remote access to a Kafka cluster

### Consuming Kafka events

- Kafka events consumed by subscribing to a topic and reading event data 

- Basic Kafka consumers

  - KafkaConsumer
    - Properties

  - KafkaConsumer.subscribe method 
  - KafkaConsumer.poll method
  - KafkaConsumer.commitSync method
  - KafkaConsumer.close method

### Performing stream processing (pic)

![image](https://user-images.githubusercontent.com/46669551/55210859-c776c880-522c-11e9-892b-de6d427e341d.png)

### Visualizing stream processing results
- Power BI online service can provide visualizations of stream processing results
- Use the following steps:
  1. In the Power BI service, define a streaming dataset, specifying API as the source rather than PubNub
  2. Configure the streaming dataset by specifying the values to use; define one value for each item to visualize 
  3. Note the Push URL that Power BI creates for app configuration 
  4. Create Power BI dashboards to visualize the data values defined in the dataset

### Limitations of Kafka

- Partition size
- Message order
- Performance spikes
- Scalability
- Mirroring

### Connecting to a Kafka cluster from a remote client

1. Create a user-specified virtual network
2. Create a Public IP address
3. Create a virtual network gateway
4. Create the HDInsight cluster in the vnet
5. Create a trusted root certificate
6. Create a client certificate that references the self-signed root certificate
7. Configure the VPN gateway to add an address pool and upload root certificate data
8. Download and install the VPN client configuration package
9. Open the VPN connection to Azure
10. Configure Kafka for IP advertising
11. Obtain the IP addresses of worker nodes in the cluster
12. Specify these IP addresses as the bootstrap servers for the producer and consumer configurations in Kafka applications 

## Demonstration: Visualizing data with Kafka clusters and Power BI
In this demonstration, you will:

- Complete the process of configuring remote access to a Kafka cluster
- Send event data to a Kafka cluster
- Perform stream processing
- Visualize event data

## Lesson 3: Using HBase to store and query data
- Why use HBase?
- Installing and configuring HBase on HDInsight
- Using HBase Shell
- Storing and retrieving data in an HBase database
- Monitoring an HBase database

### Why use HBase?

- Applications with a variable schema where each row is slightly different
- Data stored in collections
- Key-based access to data required when storing or retrieving
- Applications that need to add large numbers of columns, with low latency, especially with majority of Null columns
- Applications that do NOT require SQL, an optimizer, cross-record transactions or joins

### Installing and configuring HBase on HDInsight
1. In the Azure Portal, open the source HBase cluster
2. From the cluster menu, click **Script** **Actions**
3. Click **Submit New** from the top of the blade
4. Enter the following information:
   - **Name**
   - **Bash Script URL**
   - **Head**
   - **Parameters**

### Using HBase Shell

- Create
- List
- Put
- Scan
- Get 

### Storing and retrieving data in an HBase database
- HBaseConfiguration object
- Connection object
- Admin object
- HTableDescriptor object
- Table object
- Put object
- Get object

### Monitoring an HBase database

- Region servers
- Backup masters
- Tables
- Tasks
- Software attributes

## Lab: Implementing streaming solutions with Kafka and HBase
- Exercise 1: Prepare the lab environment
- Exercise 2: Create a virtual network and gateway
- Exercise 3: Create a Storm cluster for Kafka
- Exercise 4: Create an HBase cluster
- Exercise 5: Create a Kafka producer
- Exercise 6: Create a Power BI dashboard
- Exercise 7: Create a streaming processor client topology

### Lab Scenario

> You have access to a stream of data generated by the meters in a fleet of taxis in New York. The data includes information about each trip, including the time and location of each pickup, the time and location of each drop-off, and the price, tax, and tips paid. You want to create a streaming application in HDInsight that receives events from this data stream, calculates summary statistics, and displays information in Power BI. 
>
> You want to calculate the following summary statistics based on the live data stream:
>
> •The number of trips currently running
>
> •The average number of passengers
>
> •The average distance for a trip
>
> •The average fare for a trip
>  
>
> You have been asked to build this application as a Kafka streaming application. 

### Lab Review

- How might you use HBase clusters within your organization?
- What uses might you have for displaying and manipulating real-time data in your organization?

### Module Review and Takeaways

In this module, you learned how to:

- Build and deploy a Kafka cluster
- Publish data to a Kafka cluster, consume data from a Kafka cluster, and perform stream processing using the Kafka APIs
- Save streamed data to HBase, and perform queries using the HBase API