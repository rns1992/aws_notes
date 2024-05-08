## SNS Interview Questions

1. **What is SNS?**
    - SNS is a fully managed pub/sub messaging service provided by AWS. It enables the creation, publication, and subscription to topics, allowing messages to be sent to multiple subscribers.

2. **How does SNS work?**
    - SNS follows a publish-subscribe messaging pattern. Publishers (producers) send messages to topics, and subscribers (consumers) receive messages from these topics.
    - When a message is published to a topic, SNS delivers a copy of the message to each subscriber registered with that topic.

3. **What are the components of SNS?**
    - Topics: Channels for publishing messages.
    - Subscriptions: Endpoints (such as Amazon SQS, HTTP/HTTPS, email, SMS, Lambda) that receive messages published to topics.
    - Messages: Information sent from publishers to topics.

4. **What are the benefits of using SNS?**
    - Scalability: SNS can handle high-throughput messaging and automatically scale based on demand.
    - Flexibility: Supports various subscription protocols and endpoints, including SQS, HTTP, email, SMS, Lambda, etc.
    - Reliability: Messages are delivered reliably to subscribers, with support for retries and error handling.
    - Integration: Easily integrates with other AWS services and third-party systems.

5. **How do you ensure message delivery in SNS?**
    - SNS ensures message delivery by providing redundancy across multiple Availability Zones within a region.
    - SNS retries message delivery to subscribers that fail to acknowledge receipt, with configurable retry policies.
    - Dead-letter queues can be configured to capture messages that cannot be delivered after a specified number of attempts.

6. **What is the difference between SNS and SQS?**
    - SNS is a pub/sub messaging service, while SQS is a message queue service.
    - SNS delivers messages to multiple subscribers (fan-out), while SQS delivers messages to a single consumer (point-to-point).
    - SNS uses topics and subscriptions, whereas SQS uses queues.

7. **How do you secure SNS topics?**
    - Access control policies (IAM policies) can be applied to SNS topics to control who can publish or subscribe to them.
    - SNS supports encryption in transit (HTTPS) and encryption at rest (SSE-S3) for messages.

8. **What is the message size limit in SNS?**
    - The maximum size of a single SNS message is 256 KB.

9. **How do you handle message ordering in SNS?**
    - SNS does not guarantee message ordering. If message ordering is critical, you can use a single topic per message type or consider using a different messaging service like Amazon Kinesis.

10. **How can you monitor SNS?**
    - CloudWatch can be used to monitor SNS topics, including metrics such as number of messages published, delivery latency, etc.
    - You can also enable SNS delivery status logging to log detailed information about message deliveries.

11. **Can you explain how to implement message fanout with AWS SNS?**

    - Message fanout refers to the distribution of a message to multiple endpoints. In AWS SNS, message fanout can be achieved by publishing a message to a topic and having multiple subscribers (endpoints) subscribed to that topic. SNS automatically delivers the message to all subscribed endpoints, enabling efficient message distribution.

12. What are message attributes in AWS SNS, and how are they used?
13. How can you secure communication with AWS SNS?
14. What are the different protocols supported by AWS SNS for message delivery?
15. What is message fanout, and how can you achieve it with AWS SNS?
16. Can you describe how to implement cross-region message delivery with AWS SNS?
17. What are the benefits of using Amazon SNS?
18. Explain how Amazon SNS can be used for email notifications.
19. What are FIFO topics in Amazon SNS, and when should you use them?
20. How does message filtering work in Amazon SNS?
21. How does long polling work in Amazon SNS, and what are its benefits?
22. Can you explain the concept of message deduplication in Amazon SNS?
23. How does Amazon SNS handle message size limitations?
24. How does Amazon SNS integrate with AWS Lambda?
25. How do you handle message timeouts in Amazon SNS?
26. What are the limitations of Amazon SNS?
27. Can you explain how Amazon SNS supports message filtering based on attributes?