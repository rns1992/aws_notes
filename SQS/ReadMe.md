# AWS SQS

### What is AWS SQS?

- It's a message queue service.
- It enables web service application to quickly and reliably queue messages that one component in the applciation generates for another component to consume.
- A queue is a temporary repository for meesages awaiting processing.

### What are SQS features?

- Decouple Application Components
  - Decouple the components of an application so they run independently, easing message management between components.

- Store Messages
  - Any component of a distributed applciation can store messages in the queue. Messages can contain upto 256 KB of text in any format.

- Retrieve Messages
  - Any componebt can later retrieve the messages programmatically using the Amazon SQS API.

### What is visiblilty timeout in SQS?

- Visibility timeout is the amount of time that the message is invisible in the SQS queue after a reader picks up that message.
- If the job is not processed within that time, the message will become visible again and another reader will process it.
- Default visibility time out is 30 seconds and max is 12 hours.

### What are Key features of SQS?

1. It **Pull** Based and not Push Based.
2. Max message size if **256 KB** in size.
3. It supports **Text data** including **XML, JSON and unformatted text**.
4. It gurantees that message will be processed **at least once**.
5. Message can be kept in the queue from **one minute to 14 Days**.
6. The **default** retention period is **4 days**.

### What are different queue types in SQS?

1. **Standard Queues** are the default which provide best effor ordering.
2. **FIFO (First-in-first-out)**

### What are features of Standard Queue?

- Unlimited Transactions
  - Nearly- unlimited transactions per second.
- Gurantee
  - Gurantees that a message is delivered at least once.
- Best-Effort Ordering
  - Standard queues provide best-effort ordering which ensures that messages are generally delivered in the same order as they are sent.
  - Occasionally (because of the high-distributed architecture that allows high throughput), more than one copy of a message might be delivered out of order.

### What are features of FIFO Queue?

- First-In-First-Out Delivery
  - The order in which messages are sent and received is strictly preserved.
- Exactly-Once Processing
  - A message is delivered once and remains available until a consumer processes and deletes it. Duplicates are not introduced.
- 300 TPS Limit
  - FIFO queues are limited to 300 transactions per second (TPS), but have all the capabilities of standard queues.

### What is difference between Standard and FIFO queue?

- Refer to diagram

### What is difference between Short Polling and Long Polling?

- **Short Polling**
  - Returns a response immediately even if the message queue being polled is empty.
  - This can result in lot of empty responses if nothing is in the queue.
  - We still need to pay fot these responses.
- **Long Polling**
  - Periodically pools the queue.
  - Doesn't return a response unil a message arrives in the message queue or the long poll times out.
  - Can save money.
  - Long polling is generally preferable to short polling.

### What are SQS Delay Queues?

- SQS Delay Queue postpones delivery of new messages.
- For Standard queues, changing the setting doesn't affect the delay of messages already in the queue, only new messages will be affected.
- For FIFO queues, this affects the delay of messages already in the queue.

### When we should use Delay Queue?

- There is Large Distributed applications which may need to introduce a delay in processing.
- We need to apply a delay to an entire queue of messages.
- For example, adding a delay of a few seconds, to allow for updates for our sales and stock control databases before sending a notification to a customer confirming an online transaction.

### How to manage large SQS Messages?

- For large SQS message - 256 KB to 2 GB in size we need to use S3 to store the messages.
- We need to use Amazon SQS Extended Client Library for Java to manage them.
- We also need to use AWS SDK for Java which provides an API for S3 bucket and object operations.
- In order to store large message in SQS we will need
  - AWS SDK for Java
  - SQS Extended Client Library for Java
  - An S3 bucket
- Things that wont help to store large message
  - AWS CLI
  - AWS Management Console / SQS Console
  - SQS API
  - Any other AWS SDK