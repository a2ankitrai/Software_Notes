# Java implementations of producer and consumer

- Simple Producer Demo

- Producer with Callback

- Producer with keys

- Simple Consumer Demo

- Consumer Groups

- Consumer Threaded implementation

- Consumer Assign and Seek (consuming specific partition with specific offset)

[Github link for source code](https://github.com/simplesteph/kafka-beginners-course/tree/master/kafka-basics/src/main/java/kafka/tutorial1)

---

# Client Bi-Directional Compatibility

![bidirectional-compatibility.png](./images/bidirectional-compatibility.png)

---

# Streaming twitter data via Kafka producer

[Github source code for twitter producer](https://github.com/simplesteph/kafka-beginners-course/tree/master/kafka-producer-twitter/src/main/java/kafka/tutorial2)

---

# Producer configurations

## Producer acks (acknowledgment)

- `acks = 0`(no acks)

![producer_acks.png](./images/producer_acks.png)

- `acks = 1`(leader acks)

![producer_acks_1.png](./images/producer_acks_1.png)

- `acks = all`(replicas acks)

![producer_acks_all.png](./images/producer_acks_all.png)

**In-Sync replicas configurations**

![acks_all_min_insync.png](./images/acks_all_min_insync.png)

**Failure scenario**

![acks_all_min_insync_fail_scenario.png](./images/acks_all_min_insync_fail_scenario.png)


















---
