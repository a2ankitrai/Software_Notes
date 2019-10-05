Kafka
---

Kafka is a distributed publish-subscribe messaging system that is designed to be fast, scalable, and durable.

![kafka_use_cases](./images/kafka_usecases.png)

---

![kafka_eco_system](./images/kafka_eco_system.png)

---

![kafka_in_enterprise](./images/kafka_in_enterprise.png)

# Topics, Partitions & Offsets

![topics_n_partitions](./images/topics_n_partitions.png)

## Example

![topic_example.png](./images/topic_example.png)

- **Offset** only have a meaning for a specific partition.

	-	E.g. offset 3 in partition 2 doesn't represent the same data as offset 3 in partition 1.

- Order is guaranteed only within a partition (not across partitions)

- Data is kept only for a limited time. (default is one weeks)

- Once the data is written to a partition, **it can't be changed** (immutability)

- Data is assigned randomly to a partition unless a key is provided.

- You can have as many partitions per topic as you want.

---

# Brokers

- A Kafka cluster is composed of multiple brokers (servers)

- Each broker is identified with its ID (integer)

- Each broker contains certain topic partitions.

- After connecting to any broker (called a bootstrap broker), you will be connected to the entire cluster.

- A good number to get started is 3 brokers, but some big clusters have over 100 brokers


## Brokers and topics

![brokers_n_topics](./images/brokers_n_topics.png)

## Topic replication factor

- Topics should have a replication factor > 1 (usually between 2 and 3)

- This way if a broker is down, another broker can serve the data

- Example: Topic with 2 partitions and replication factor of 2 

![topic_replication_1](./images/topic_replication_1.png)

- Example: we lost Broker 2

- Result: Broker 1 and 3 can still serve the data

![topic_replication_2](./images/topic_replication_2.png)

## Concept of Leader for a partition

- **At any time only 1 broker can be a leader for a given partition**

- **Only that leader can receive and serve data for a partition**

- The other brokers will synchronize the data

- There each partition has: one leader, and multiple ISR (in-sync replica)

- The leader and ISR is determined by Zookeeper.

![topic_replication_3](./images/topic_replication_3.png)


---

# Producers

- Producers write data to topics (which is made of partitions).

- Producers automatically know to which broker and partition to write to

- In case of Broker failures, Producers will automatically recover.

- **They only have to specify the topic name and one broker to connect to, and Kafka will automatically take care of routing the data to the right brokers**.

- Producers can choose to receive acknowledgement of data writes:

	- Acks = 0 : Producer won't wait for acknowledgement (possible data loss)
	- Acks = 1 : Producer will wait for leader acknowledgement (limited data loss)
	- Acks = all : Leader + replicas acknowledgment (no data loss) 


![producers_1](./images/producers_1.png)

## Producers: Message keys

- Producers can choose to send a key with the message (string, number, etc..).

- If key=null, data is sent round robin (broker 101 then 102 then 103...)

- If a key is sent, then the producer has the guarantee that all messages for that key will always go to the same partition. A key is basically sent if you need message ordering for a specific field.

- This enables to guarantee ordering of a specific key.

![producers_2](./images/producers_2.png)


---

# Consumers

- Consumers read data from a topic (identified by name)

- Consumers know which broker to read from

- In case of broker failures, consumers know how to recover.

- **They only have to specify the topic name and one broker to connect to, and Kafka will automatically take care of pulling the data from the right brokers**.

- Data is read in order **for each partitions.**
 
![consumers_1](./images/consumers_1.png)

- Note: *Consumers will automatically use a GroupCoordinator and a ConsumerCoordinator to assign a consumers to a partition*

## Consumer Groups

- Consumers read data in consumer groups

- Each consumer within a group reads from exclusive partitions

- You cannot have more consumers than partitions (otherwise some will be inactive)

![consumers_2](./images/consumers_2.png)

**What if too many consumers?**

- If you have more consumers than partitions, some consumers will be inactive.

![multiple_consumers.png](./images/multiple_consumers.png)

## Consumer Offsets

- Kafka stores the offsets at which a consumer group has been reading

- The offset commit live in a Kafka topic named  `__consumer_offsets`

- When a consumer has processed data received some Kafka, it should be committing the offsets

- If a consumer process dies, it will be able to read back from where it left off thanks to consumer offsets!

![consumers_3](./images/consumers_3.png)

## Delivery semantics for consumers

- Consumers choose when to commit offsets

- There are three delivery semantics:

- **At most once**
	- offsets are committed as soon as the message is received.
	- If the processing goes wrong, the message will be lost(it won't be read again).

- **At least once(usually preferred)**
	- offsets are committed after the message is processed.
	- If the processing goes wrong, the message will be read again.
	- This can result in duplicate processing of messages. Make sure your processing is idempotent(ie. processing again the messages won't impact your systems)

- **Exactly once**
	- Can be achieved for Kafka => Kafka workflows using Kafka Streams API.
	- For Kafka => External system workflows, use an idempotent consumer.	

---

# Kafka Broker Discovery

- Every Kafka broker is also called a "bootstrap server".

- That means that you only need to connect to one broker, and you will be connected to the entire cluster.

- Each broker knows about all brokers, topics and partitions (metadata).

![broker_discovery.png](./images/broker_discovery.png)

---

# Zookeeper

- Zookeeper manages brokers (keeps a list of them)

- Zookeeper helps in performing leader election for partitions

- Zookeeper sends notifications to Kafka in case of changes (e.g. new topic, broker dies, broker comes up, delete topics etc...)

- **Kafka can not work without a Zookeeper**

- Zookeeper ususally operates in an odd quorum (cluster) of servers (3,5,7)

- Zookeeper has a leader(handle writes), the rest of the servers are followers(handle reads)
 
- Zookeeper does not store consumer offsets with Kafka > v0.10)

![zookeeper](./images/zookeeper.png)

---

# Kafka Guarantees

- Messages are appended to a topic-partition in the order they are sent

- Consumer reads messages in the order stored in a topic-partition

- With a replication factor of N, producers and consumers can tolerate up to N-1 brokers being down

- This is why a replication factor of 3 is a good idea:
	
	- Allows for one broker to be taken down for maintenance

	- Allows for another broker to be taken down unexpectedly

- As long as the number of partitions remains constant for a topic (no new partitions), the same key will always go to the same partition

---

# Summary

![theory-summary.png](./images/theory-summary.png)


  






























