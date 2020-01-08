# ElasticSearch Consumer & Consumer configurations

**ElasticSearch on Demand**

https://bonsai.io

---

Twitter data producer:

[Github source code for twitter producer](https://github.com/simplesteph/kafka-beginners-course/blob/master/kafka-producer-twitter/src/main/java/kafka/tutorial2/TwitterProducer.java)

ElasticSearch Consumer:

[ElasticSearch consumer code](https://github.com/simplesteph/kafka-beginners-course/blob/master/kafka-consumer-elasticsearch/src/main/java/com.github.simplesteph.kafka/tutorial3/ElasticSearchConsumer.java)

----

# Delivery Semantics

## At Most Once

![deilvery_semantic_at_most_once.png](./images/deilvery_semantic_at_most_once.png)

![delivery_semantics_1.gif](./images/delivery_semantics_1.gif)

## At Least Once

![deilvery_semantic_at_least_once.png](./images/deilvery_semantic_at_least_once.png)

## Summary

![delivery_semantics_summary.png](./images/delivery_semantics_summary.png)

----

# Idempotence

To achieve Idempotence in Kafka, we can use the following to generate the same id for the same message when it is processed again. This is Kafka generic id. Similarly other methods can be used so that even if process the message more than once we don't create duplicates.

```java
// kafka generic ID
String id = record.topic() + "_" + record.partition() + "_" + record.offset();
  ```

---

# Consumer Offset Commits Strategies

![offset_commit_strategy_1.png](./images/offset_commit_strategy_1.png)

---

## `enable.auto.commit = true`

![offset_commit_strategy_2.png](./images/offset_commit_strategy_2.png)

---

## `enable.auto.commit = false`

![offset_commit_strategy_2.png](./images/offset_commit_strategy_3.png)


---


# Consumer Offset Reset Behaviour

![consumer-offset-reset-behaviour-1.png](./images/consumer-offset-reset-behaviour-1.png)

![consumer-offset-reset-behaviour-2.png](./images/consumer-offset-reset-behaviour-2.png)

---

# Replaying data for consumers

![replay-data-for-consumer.png](./images/replay-data-for-consumer.png)

![offset_reset.png](./images/offset_reset.png)

---

# Controlling Consumer Liveliness

![consumer-liveliness.png](./images/consumer-liveliness.png)

## Consumer Heartbeat Thread

![Consumer-Heartbeat-Thread.png](./images/Consumer-Heartbeat-Thread.png)
