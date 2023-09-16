# ADR-10: Message Broker and Event System Strategy

## Status

Adopted

## Context

Our application needs a robust system to handle a vast number of messages, events, and updates that originate from different parts of the system, particularly with travel-related updates. The choices under consideration are:

1. **[Apache Kafka](https://kafka.apache.org/)**:
    - Distributed streaming platform that can handle high volumes of data.
    - Designed for durability, with data written to disk and replicated to prevent data loss.
    - Scalable, can handle millions of messages per second.
    - Provides a real-time analytics capability.
    - Kafka Streams allow for stream processing.
    - Complexity is higher and might require specialized knowledge for setup and maintenance.

2. **[RabbitMQ](https://www.rabbitmq.com/)**:
    - Messaging broker that focuses on offering a variety of messaging patterns.
    - Provides a simpler setup compared to Kafka.
    - Not inherently designed for data durability as Kafka is.
    - Best suited for scenarios where different types of messaging patterns are more critical than high throughput or stream processing.

3. **[AWS SNS/SQS](https://aws.amazon.com/sns/)**:
    - Amazon Simple Notification Service (SNS) is a managed pub/sub messaging service.
    - Amazon Simple Queue Service (SQS) is a managed message queuing service.
    - Fully managed, ensuring high availability without administrative overhead.
    - Might cause vendor lock-in, tying our application to the AWS ecosystem.
    - Not as performant as Kafka for very high throughput scenarios.

Given the scale of our platform, the anticipated volume of messages, and the need for real-time analytics and processing, we required a solution that is both performant and scalable.

## Decision

We have chosen to employ **Apache Kafka** for the following reasons:

1. **High Throughput**: Kafka can handle millions of messages per second, fitting our platform's scale.
2. **Durability and Reliability**: Messages in Kafka are persisted on disk and replicated, ensuring data safety.
3. **Scalability**: Kafka clusters can be expanded easily to accommodate growing data.
4. **Real-time Stream Processing**: Using Kafka Streams, we can process our data in real-time, which is crucial for timely updates.
5. **Avoid Vendor Lock-in**: Kafka being an open-source project ensures we aren't tied to a specific cloud provider's ecosystem.

## Consequences

**Pros**:

- **Performance and Scale**: Kafka's architecture allows for handling very high volumes of data efficiently.
- **Flexibility**: Ability to leverage Kafka's ecosystem for stream processing, connectors, and more.
- **Reliability**: With data replication and durability guarantees, data loss risks are minimized.

**Cons**:

- **Complexity**: Kafka's setup, tuning, and maintenance might require more specialized knowledge.
- **Operational Overhead**: While highly performant, Kafka might introduce more operational overhead than a simpler queuing system.
- **Resource Intensive**: Kafka is designed for high performance, which can also mean it's resource-hungry.
