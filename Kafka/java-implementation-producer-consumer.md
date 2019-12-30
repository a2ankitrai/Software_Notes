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

[Github source code for twitter producer](https://github.com/simplesteph/kafka-beginners-course/blob/master/kafka-producer-twitter/src/main/java/kafka/tutorial2/TwitterProducer.java)

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

# Producer Retries

![producer_retries_1.png](./images/producer_retries_1.png)

![producer_retries_2.png](./images/producer_retries_2.png)

---

# Idempotent Producer

![idempotent_producer_1.png](./images/idempotent_producer_1.png)

![idempotent_producer_2.png](./images/idempotent_producer_2.png)

Producer also sends a producer id which is used to identify duplicate messages.

![idempotent_producer_3.png](./images/idempotent_producer_3.png)

---

# Safe Producer Summary

![safe_producer_summary.png](./images/safe_producer_summary.png)

**In Java**

```java
public KafkaProducer<String, String> createKafkaProducer(){
    String bootstrapServers = "127.0.0.1:9092";

    // create Producer properties
    Properties properties = new Properties();
    properties.setProperty(ProducerConfig.BOOTSTRAP_SERVERS_CONFIG, bootstrapServers);
    properties.setProperty(ProducerConfig.KEY_SERIALIZER_CLASS_CONFIG, StringSerializer.class.getName());
    properties.setProperty(ProducerConfig.VALUE_SERIALIZER_CLASS_CONFIG, StringSerializer.class.getName());

    // create safe Producer
    properties.setProperty(ProducerConfig.ENABLE_IDEMPOTENCE_CONFIG, "true");
    properties.setProperty(ProducerConfig.ACKS_CONFIG, "all");
    properties.setProperty(ProducerConfig.RETRIES_CONFIG, Integer.toString(Integer.MAX_VALUE));
    properties.setProperty(ProducerConfig.MAX_IN_FLIGHT_REQUESTS_PER_CONNECTION, "5"); // kafka 2.0 >= 1.1 so we can keep this as 5. Use 1 otherwise.

    // high throughput producer (at the expense of a bit of latency and CPU usage)
    properties.setProperty(ProducerConfig.COMPRESSION_TYPE_CONFIG, "snappy");
    properties.setProperty(ProducerConfig.LINGER_MS_CONFIG, "20");
    properties.setProperty(ProducerConfig.BATCH_SIZE_CONFIG, Integer.toString(32*1024)); // 32 KB batch size

    // create the producer
    KafkaProducer<String, String> producer = new KafkaProducer<String, String>(properties);
    return producer;
}
```

---

# Message Compression

![message_compression.png](./images/message_compression.png)

Benchmarks here: https://blog.cloudflare.com/squeezing-the-firehose/

![message_compression_2.png](./images/message_compression_2.png)

## Advantages and Disadvantages

![message_compression_3.png](./images/message_compression_3.png)

## Recommendations

![message_compression_4.png](./images/message_compression_4.png)

---

# Linger.ms & batch.size

![linger_batch_1.png](./images/linger_batch_1.png)

## Controlling the batching mechanism

**Linger.ms**

![linger_batch_2.png](./images/linger_batch_2.png)

![linger_batch_3.png](./images/linger_batch_3.png)

**Batch size**

![linger_batch_4.png](./images/linger_batch_4.png)











---
