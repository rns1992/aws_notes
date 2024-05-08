## SQS Interview Questions

1. **SQS vs Kafka**
    1. **Model**
        - Kafka follows pub-sub model where producer will produce the message and all the consumers which subscribed to the topic will receive at least once published message.
        - SQS follows Message Queue Model. The publishing service will typically put a message on a queue or exchange and a **single consumer** service will consume this message and perform an action based on this. So at a time only one consumer would be able to consume and process the message from the queue.
    2. **Cost/Infrastructure**
        - Kafka can be run on-premises or in the cloud, and the cost will depend on the hardware and infrastructure required to run the system.
        - SQS is a fully managed service provided by Amazon Web Services (AWS), and the cost will depend on the number of requests made and the amount of data transferred.
    3. **Message Processing**
        - Kafka is designed for high-throughput, real-time **data** **streaming** and **batch processing**. It supports parallel processing of messages using partitions.
        - SQS is designed for **simple, asynchronous messaging** between applications, with a focus on ease of use and scalability. It provides a reliable and highly available message queue service, but it does not support real-time data streaming or parallel processing.
    4. **Durability**
        - Kafka provides a high level of durability for messages by storing them on disk and replicating them across multiple nodes in a cluster.
        - SQS provides a high level of durability for messages by automatically storing them redundantly across multiple Availability Zones in the same region
    5. **Scalability**
        - Kafka is highly scalable and can handle high volumes of messages. It can be horizontally scaled by adding more nodes to the cluster.
        - SQS is a fully managed service that is highly scalable, and it can automatically scale to handle the number of messages being sent and received.
    6. **Complexity**
        - Kafka can be complex to set up and manage, especially at scale.
        - SQS is a fully managed service, so it requires no setup or management, making it the simplest of the three systems to use.

2. **Visibility timeout in SQS**
    - In AWS Simple Queue Service (SQS), the visibility timeout is a crucial feature that prevents multiple consumers from processing the same message simultaneously. When a consumer retrieves a message from an SQS queue, the message becomes invisible to other consumers for the duration of the visibility timeout.
    - *How it works*?
        1. **Consumer receives a message**: When a consumer pulls a message from the queue, the message is considered "in flight," and it becomes invisible to other consumers.
        2. **Visibility timeout starts**: At this point, the visibility timeout countdown begins. The default visibility timeout is 30 seconds, but you can set a custom timeout (up to 12 hours) when you create the queue or update its settings.
        3. **Message processing**: The consumer processes the message received from the queue. If the consumer successfully processes the message within the visibility timeout period, it deletes the message from the queue.  
        4. **Message deletion**: If the consumer fails to delete the message within the visibility timeout period (due to a system failure or any other reason), the message becomes visible in the queue again after the timeout expires. This ensures that another consumer can attempt to process it.

3. **What if using SQS and there is an exception in your code.**

    1. Catch and log the exception
    2. Retry logic
    3. Dead Letter Queue
    4. Ensure that the visibility timeout for messages is set appropriately to allow sufficient time for processing. If the processing time exceeds the visibility timeout, the message may become visible again in the queue, potentially causing duplicate processing.
    5. Set up monitoring and alerting mechanisms to detect SQS-related errors or failures proactively. This allows you to respond quickly to any issues and minimize downtime.

4) **How does SQS trigger Lambda?**
	- Already mentioned in Lambda Interview Questions.

5) **What are the limitations of SQS?**
	1.  **Message size**: The maximum size of a single message in SQS is 256 KB for both Standard and FIFO queues. If you need to send larger messages, you'll need to use S3 to store the message payload and send a reference to the S3 object in the SQS message.
	2. **Message retention**: Messages in SQS queues are retained for a maximum of 14 days. After this period, messages are automatically deleted from the queue, even if they haven't been processed.
	3. **Throughput limitations**: While SQS is designed to handle high throughput, there are some throughput limitations that you should be aware of.
	4. **Visibility timeout**: The maximum visibility timeout for a message in SQS is 12 hours. If a message isn't processed within this time frame, it becomes visible in the queue again, potentially leading to duplicate processing.
	5. **Regional constraints**: SQS queues are tied to a specific AWS region, meaning they can't be accessed directly from outside that region. If you need to access a queue from multiple regions, you'll need to replicate the data or use cross-region communication mechanisms.
	6. **Inflight Messages**: Inflight messages are messages in SQS that have been received by a consumer but not yet deleted. Each SQS queue is limited to 120,000 inflight messages, or 20,000 if it is a FIFO queue. When sending a message to a queue with too many inflight messages, SQS returns the "OverLimit" error message.
6) **What are the key features of SQS?**

7) **What are the different types of queues in SQS?**
	1) *Standard Queue* - Order not maintained
	2) *FIFO* - Order maintained in FIFO order. FIFO queues can only support 300 send, receive,  _or_  delete operations per second. When using message batching at 10 messages, this effectively is increased to 3,000 operations per second
	
8) **How does message delivery work in SQS?**
	1. Producer sends a message to a queue.
	2. Message is stored in the queue
	3. Consumers retrieve messages from the queue. When a consumer requests messages from the queue, SQS returns one or more messages up to the maximum configured batch size
	4. Message becomes "in flight". During this time, the message is not visible to other consumers polling the queue. SQS manages message visibility through a mechanism called the visibility timeout.
	5. Message processing. If the processing is successful, the consumer deletes the message from the queue to indicate that it has been successfully processed.
	6. Message deletion. After processing, the consumer deletes the message from the queue using its handle or receipt handle.
9) **What is long polling in SQS, and how does it differ from short polling?**
	- In AWS SQS, long polling and short polling are two different methods used by consumers to retrieve messages from a queue. These methods differ in how they handle the polling process and how they impact the efficiency and cost of message retrieval.
	1.  **Short polling**:
	    -   In short polling, the consumer sends a request to the SQS queue to retrieve messages.
	    -   If there are messages available in the queue at the time of the request, SQS immediately sends them back to the consumer.
	    -   If the queue is empty at the time of the request, SQS returns an empty response without waiting.
	    -   Short polling is the default behavior for message retrieval in SQS.
	2. **Long polling**:
	    -   In long polling, the consumer sends a request to the SQS queue to retrieve messages, but it specifies a wait time (between 1 and 20 seconds).
	    -   If there are messages available in the queue at the time of the request, SQS immediately sends them back to the consumer, just like short polling.
	    -   If the queue is empty at the time of the request, SQS waits for the specified period (up to the specified wait time) for messages to arrive before responding.
	    -   If messages arrive in the queue during the wait time, SQS sends them back immediately.
	    -   Long polling reduces the number of empty responses and helps avoid the overhead and cost associated with frequent polling in scenarios with low message traffic.
    - In summary, while short polling is suitable for scenarios where immediate message retrieval is essential, long polling is more efficient and cost-effective for scenarios with lower message traffic or when latency is less critical. It's generally recommended to use long polling whenever possible to optimize message retrieval in SQS queues.
10) **Explain the message retention period in SQS.**
	- The message retention period in AWS SQS refers to the duration for which messages are retained in a queue after being sent to it.
	- By default, messages in an SQS queue are retained for a maximum of 14 days. This means that once a message is sent to the queue, it will remain there for up to 14 days, regardless of whether it has been retrieved by consumers or not. After this period, messages are automatically deleted from the queue by SQS.
	- The message retention period can also impact the cost of using SQS. Longer retention periods may result in increased storage costs if the queue accumulates a large number of messages over time. Additionally, if messages are not processed promptly, it may lead to higher data transfer costs if messages are retrieved from the queue across regions.
11) **What is Dead Letter Queue (DLQ) in SQS, and how is it used?**
	- A Dead Letter Queue (DLQ) in AWS SQS is a special type of queue that is used to capture messages that could not be processed successfully after a certain number of attempts
	- When creating or configuring an SQS queue, you can specify a DLQ to which messages will be moved if they exceed the maximum number of processing attempts. You set up the DLQ as an attribute of the main queue.
	- You can define the maximum number of times a message can be received (i.e., retrieved by a consumer) and not successfully processed before it is considered problematic. Once a message exceeds this threshold, it is automatically sent to the DLQ.
	- Once the issues causing message processing failures are resolved, messages in the DLQ can be reprocessed and sent back to the main queue for normal processing.
	- By using a Dead Letter Queue in SQS, you can implement robust error handling and fault tolerance mechanisms in your messaging system, ensuring that problematic messages are captured, analyzed, and resolved effectively without disrupting the overall message processing flow.
12) **How do you manage access to SQS queues in AWS?**

13) **How can you scale SQS to handle high throughput or large numbers of messages?**
	1. Use **batched Amazon SQS** actions to send, receive, or delete up to 10 messages at a time. Batching can improve throughput and reduce costs.
	2. Enable **long polling** by setting the WaitTimeSeconds parameter to minimize empty responses and reduce unnecessary network traffic.
	3. Adjust the **visibility timeout** to ensure that messages are processed completely before they become visible to other consumers again.
	4. For **FIFO queues**, increase the number of message groups you use to support a higher number of requests per API, per second.
	5. Use **AWS Lambda functions** triggered by SQS messages to process data in batches. You can store these messages temporarily in a scalable storage service like Amazon DynamoDB or Amazon Elastic Cache.
14) **What is the maximum message size in SQS, and how can you handle larger messages?**
	- Max message size is 256 KB for both types of queues.
	- If you need to handle messages larger than 256 KB, then below are the options:
		1. **Store Message Payload in Amazon S3**: Instead of including the entire message payload directly in the SQS message body, you can store the payload in Amazon S3 and include a reference (e.g., S3 object URL) in the SQS message. This approach allows you to handle larger payloads efficiently while still leveraging SQS for message queuing.
		2.  **Use Message Compression**: Compress the message payload before sending it to SQS to reduce its size. SQS supports various compression algorithms (e.g., **gzip, deflate**), which can help reduce the message size and stay within the 256 KB limit.
		3.  **Split Messages into Smaller Parts**: If the message payload exceeds the size limit, consider splitting it into smaller parts and sending multiple messages. This approach requires logic on the producer and consumer sides to handle message fragmentation and reassembly, but it allows you to work within the size constraints of SQS.
		4.  **Message Chunking**: Chunk the message payload into smaller segments and send each segment as a separate message. Include metadata in each message to identify its position in the sequence and reconstruct the original payload on the consumer side. This approach is similar to splitting messages but involves a more structured approach to handle message segmentation and reconstruction.
		5.  **Custom Solutions**: Implement custom solutions or use other AWS services (e.g., Amazon Kinesis, Amazon Simple Notification Service) for handling larger messages or streaming data scenarios where message size exceeds the SQS limit. Evaluate your specific requirements and choose the approach that best fits your use case.

15) **What are some best practices for using SQS efficiently and securely in AWS architectures?**
	1. **Enable Server-Side Encryption (SSE)**
		- Enable SSE for SQS queues to encrypt message data at rest using AWS Key Management Service (KMS) keys.
		- Use AWS managed keys (AWS managed CMKs) or customer-managed keys (customer-managed CMKs) for fine-grained control over encryption keys and access.
	2. **Implement Least Privilege Access**
		- Use IAM policies to restrict access to SQS queues based on the principle of least privilege.
		- Grant only the necessary permissions to users, roles, or applications to send, receive, or manage messages in SQS queues.

16) **How does SQS ensure message durability and availability?**
	1.  **Replication and Redundancy**:
	    -   SQS automatically replicates messages across multiple availability zones (AZs) within the same AWS region. This redundancy ensures that messages are stored in multiple data centers, increasing durability and fault tolerance.
	    -   By storing messages in multiple AZs, SQS can withstand failures of individual servers, network components, or entire data centers without losing messages.
	2.  **Data Persistence**
	    -   Messages stored in SQS queues are durably persisted, meaning they are retained even in the event of server failures or restarts.
	    -   SQS queues have a default retention period of up to 14 days, during which messages remain in the queue unless explicitly deleted or moved to a Dead Letter Queue (DLQ) due to processing failures.
	3.  **High Availability**:
	    
	    -   SQS is designed for high availability, with service level agreements (SLAs) guaranteeing availability percentages (e.g., 99.9% or higher).
	    -   The distributed nature of SQS across multiple AZs ensures that queues remain available even if individual components or AZs experience disruptions.
	4.  **Atomic Operations**:
	    
	    -   SQS performs atomic operations on messages, ensuring that messages are either processed successfully and deleted from the queue or remain in the queue for further processing.
	    -   Message deletion is an atomic operation, meaning that once a message is deleted from the queue, it cannot be retrieved again.
	5.  **Message Replication and Delivery**:
	    
	    -   When a message is sent to an SQS queue, SQS replicates the message across multiple servers and stores it durably in its data stores.
	    -   Messages are delivered to consumers at least once, ensuring that messages are not lost during transmission. However, duplicate delivery may occur in some scenarios, so consumers must be idempotent.
	6.  **Monitoring and Maintenance**:
	    
	    -   AWS continuously monitors the health and performance of SQS infrastructure and performs maintenance tasks, such as hardware upgrades and software patches, without impacting message availability.
	    -   Amazon CloudWatch provides metrics and alarms for monitoring SQS queue health, allowing users to detect and respond to issues proactively.

17) **Explain the concept of message deduplication in SQS.**
	- Message deduplication in AWS SQS is a feature designed to prevent the processing of duplicate messages within a queue. It ensures that each message is processed only once, even if it's received multiple times due to network retries, system failures, or other factors. Here's how message deduplication works in SQS:
		1.  **Message Deduplication ID**:
		    
		    -   When a message is sent to an SQS queue, the sender can optionally provide a Message Deduplication ID (MD5 digest) for the message. This ID is a unique identifier associated with the message payload.
		2.  **Deduplication Window**:
		    
		    -   SQS maintains a deduplication window, which is a period during which SQS remembers the Message Deduplication IDs of messages that have been successfully processed. The default deduplication window is 5 minutes, but you can configure it to be up to 15 minutes.
		3.  **Duplicate Detection**:
		    
		    -   When a message is received by SQS, it checks the Message Deduplication ID against the IDs of messages processed within the deduplication window.
		    -   If the Message Deduplication ID matches a previously processed message ID within the deduplication window, SQS treats the message as a duplicate and does not deliver it to consumers.
		4.  **Handling of Duplicate Messages**:
		    
		    -   When SQS detects a duplicate message, it does not delete the message from the queue. Instead, it discards the duplicate message and does not deliver it to consumers for processing.
		    -   The original (non-duplicate) message remains in the queue and is processed as usual.
		5.  **Ensuring Message Uniqueness**:
		    
		    -   To ensure message uniqueness, the sender must provide a unique Message Deduplication ID for each message sent to the queue. This ID could be generated based on message attributes or content, such as a hash of the message payload.
		6.  **Benefits**:
		    
		    -   Message deduplication helps prevent unintended duplicate processing of messages, which can occur due to network glitches, retries, or failures.
		    -   By eliminating duplicate processing, message deduplication improves the reliability and consistency of message processing in distributed systems.
		7.  **Considerations**:
		    
		    -   Message deduplication is an optional feature in SQS and must be enabled when creating the queue or updating its settings.
		    -   Enabling message deduplication incurs a slight increase in message processing overhead, as SQS needs to maintain a deduplication cache to track processed message IDs.

18) **How do you monitor SQS queues and their performance in AWS?**
	1.  **Amazon CloudWatch Metrics**:
	    
	    -   CloudWatch provides several metrics for monitoring SQS queue health and performance, including:
	        -   ApproximateNumberOfMessages: Number of messages in the queue, including those not yet processed.
	        -   ApproximateNumberOfMessagesDelayed: Number of messages that are in the queue and are delayed.
	        -   NumberOfMessagesSent: Number of messages sent to the queue during a specified time period.
	        -   NumberOfMessagesReceived: Number of messages received from the queue during a specified time period.
	    -   Use CloudWatch dashboards to create custom visualizations of SQS metrics and set up alarms for key metrics to receive notifications when certain thresholds are exceeded.
	2.  **Amazon CloudWatch Logs**:
	    
	    -   Enable CloudWatch logging for SQS queues to capture detailed information about queue activity, including message send, receive, and delete operations.
	    -   Analyze SQS logs using CloudWatch Logs Insights to gain insights into queue performance, identify trends, and troubleshoot issues.
	3.  **AWS CloudTrail**:
	    
	    -   Enable CloudTrail logging for SQS API calls to track and audit actions performed on SQS queues by users, roles, or AWS services.
	    -   Use CloudTrail logs to monitor queue access, detect unauthorized activity, and investigate security incidents.
	4.  **AWS X-Ray**:
	    
	    -   Use AWS X-Ray to trace and analyze message flows between SQS queues and other AWS services in distributed applications.
	    -   Gain visibility into message processing latency, error rates, and dependencies to identify bottlenecks and optimize performance.

19) **What are the cost considerations when using SQS, and how can you optimize costs?**

20) **Can you integrate SQS with other AWS services? If so, how?**

21) **SQS vs RabbitMQ**
	1.  RabbitMQ is FIFO by default. Amazon SQS queues can optionally be set to FIFO.
	2.  You can setup your own server with RabbitMQ but not in the case of Amazon SQS so the cost gets involved here.
	3.  Setting up your own server will require good knowledge of the subject so that you do not leave any corner untouched. This is not the case with Amazon SQS as it is pretty quick to get started with.	    
	4.  Your own RabbitMQ server means maintenance cost down the line which is not the case with Amazon SQS.
	5.  SQS is a managed service. So you don't have to worry about operational aspects of running a messaging system including administration, security, monitoring etc. Amazon will do this for you and will provide support if something were to go wrong.
	6.  SQS is Elastic and can scale to very large rate/volumes (unlimited according to AWS ;))
	7. Availability of SQS has a lot of 9's in it and is backed by Amazon, which is one less thing to worry about in your application.

22) **How to implement fan-out pattern in SQS?**
	 - https://aws.amazon.com/blogs/aws/queues-and-notifications-now-best-friends/