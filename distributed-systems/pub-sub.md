# Pub/Sub Pattern

## Scenario 

Given the process for a customer purchasing an item in an Ecommerce application:

1. Customer visits Application
2. Customer purchases Item.
3. Request for Item is sent with Customer details to Payment Service.
4. Payment Service notifies Packaging Service and Reporting Service.
5. Report Service does something.
6. Packaging Service notifies Shipping Service.
7. Shipping Service notifies Notification Service.
8. Notification Service notifies Customer of Order state.

### Problems:
- Its complicated, lots of dependencies.
- If a service fails, there needs to be a retry mechanism to keep the whole system from failing. Adds complexity.
- If a new service is introduced (e.g. monitoring), it needs to interface with all the other services, and making change to all the other services. 
- For testing, as services are dependent on each other, you will need to mock up all the services just to test 1 service.

### Pub/Sub Solution:
- Real time messaging service that allows you to send and receive message independent applications.
- Once and event is successfully published as a message, it becomes the job of the Pub/Sub service to enusre that all the systems that need to react this event will get it.
- The idea behind the asynchronous integrations is to react to events represented as messages. In the example, messages can represent events happening in the real world, e.g. Order received, Package shipped, etc.

### Implementing with Cloud Pub/Sub:
1. Customer visits Application
2. Customer purchases Item.
3. Request for Item is sent with Customer details to Pub/Sub Service.
4. Pub/Sub will push (or services will pull) the message to Payment Service.
5. Payment Service will push message to Pub/Sub.
6. Pub/Sub will push to Reporting, Packaging, etc.

The services do not know which other services are receiving the event.

## Comparison with Observer pattern
- The Subject maintains a list of all the Observers and will notify() each Observer from a given event.
- In Pub/Sub, senders of messagers called Publishers do not program the messages to be sent directly to Subscribers. There is a third component called the message broker or event bus. This component helps the communication between publishers and subscribers.
- Observers are mostly implemented in a **synchronous** way, i.e. the Subject calls the appropriate method of all its Observers when some event occurs.
- Pub/Sub is mostly implemented in an **asynchronous** way using the messaging queue.

## Tools

Summary: 
- ActiveMQ/RabbitMQ (general purpose). 
- Kafka: distributed streaming platform, scales well and due to high throughput is good for real-time data streaming.

Kafka Architecture is different to ActiveMQ.

In Kafka, producer will publish messages to topic, which is a stream of messages of a particular type. Consumer will subscribe to one or more topics of brokers by pulling the data.

### Key differences:
- ActiveMQ Broker had to maintain the delivery state of every message resulting into lower throughput. Kafka producer doesn’t wait for acknowledgements from the broker. Overall throughput will be high if broker can handle the messages as fast as producer.
- Kafka has a more efficient storage format. On average, each message had an overhead of 9 bytes in Kafka, versus 144 bytes in ActiveMQ.
- ActiveMQ is push based messaging system and Kafka is pull based messaging system . In AcitveMQ, Producer push messages to all consumers. Producer has responsibility to ensure that message has been delivered. In Kafka, Consumer will pull messages from broker at its own time. It's the responsibility of consumer to consume the messages it has supposed to consume.
- Slow Consumers in AMQ can cause problems on non-durable topics since they can force the broker to keep old messages in RAM which once it fills up, forces the broker to slow down producers, causing the fast consumers to be slowed down. A slow consumer in Kakfa does not impact other consumers.

    In Kafka - A consumer can rewind back to an old offset and re-consume data. It is useful when you fix some issue and decide to re-play the old messages post issue resolution.

    Performance of Queue and Topics degrades with addition of more consumers in ActiveMQ. But Kafka does not have that dis-advantage with addition of more consumers.

    Kafka is highly scalable due to replication of partitions. It can ensure that messages are delivered in a sequence with in a partition.

    ActiveMQ is traditional messaging system where as Kakfa is meant for distributed processing system with huge amount of data and effective for stream processing

Due to above efficiencies, Kafka throughput is 2x - 4x times more than normal messaging systems like ActiveMQ and RabbitMQ.