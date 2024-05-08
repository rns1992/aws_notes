## AWS Lambda Interview Questions

1. **What are the limitations of aws lambda?**
 - **Execution Time Limit**: It can run max up to 15 mins.
 - **Stateless Execution**: As it is stateless we can not store anything inside it. We need to use S3, Dynamo Db or EFS.
 - **Deployment Package Size**: The compressed deployment package (ZIP file) must be less than 50 MB, and the uncompressed package must be less than 250 MB. If your function requires larger dependencies or resources, you may need to consider alternative deployment strategies.
 - **Memory Limit**: Lambda functions have memory limits ranging from 128 MB to 10 GB. The amount of memory allocated to a function also determines the CPU power available to it. If your function requires more memory or CPU power, you may need to optimize your code or consider a different compute option.
 - **Temporary Storage**: Lambda functions are allocated temporary storage space in the `/tmp` directory, with a limit of 512 MB. If your function requires more temporary storage, you may need to use other AWS services like S3 or DynamoDB for storage needs.
 - **Cold Start Performance**: When a Lambda function is invoked infrequently or after a period of inactivity, there may be a delay known as a "cold start" as the execution environment is initialized. This can impact the latency of your application, especially for time-sensitive workloads.
 - **Limited Runtimes**: While Lambda supports multiple programming languages (such as Node.js, Python, Java, etc.), the available runtime environments may not support every programming language or version.
 - **Concurrency Limits**: Lambda functions are subject to concurrency limits, which define the maximum number of function instances that can run simultaneously. By default, this limit is 1,000 concurrent executions per region. If your application requires more concurrency, you may need to request a limit increase or implement concurrency controls in your code.

2. **How do you make versioning of lambda code?**
 1.  Open the Functions page of the Lambda console.
 2.  Choose a function and then choose Versions.
 3.  On the versions configuration page, choose Publish new version.
 4.  (Optional) Enter a version description.
 5.  Choose Publish.

3. **How do you code, deploy and debug the lambda functions on aws?**
 1. By Uploading Zip File to Lambda Console and publishing it
 2. By Jenkins. In Jenkins we need to install plugin for AWS Lambda and configure git repository configurations. So the pipeline which we have defined will be responsible for fetching from repository, building and deploying code in Lambda with new version. Also we can have another way of uploading Zip file in S3 and then deploying.
4. **How lambda functions were been configured?**
 1. **General Configurations**
    - Memory
    - Ephemeral Storage
    - Function timeout
 2. **Triggers**
    - The service or resource that is able to invoke your function
 3. **Permissions**
    - The function's execution role determines the permissions that the function will have.
 4. **Function URL**
    - An HTTPs endpoint used to access your function using a browser.
 5. **Tags**
    - User defined key-value pairs that help organize functions
 6. **VPC**
    - Allow your function to access resource that are in a custom VPC (e.g. a private VPC)
 7. **Monitoring and Operations Tools**
    - CloudWatch, CloudWatch Logs, X-Ray (performance issues)
 8. **Concurrency**
    - Reserved concurrency ensures that a critical function can always run and restrict other concurrent requests.
    - Provisioned concurrency lets your function scale consistently without any fluctuations in latency
 9. **File System**
    - EFS file system that your function needs to connect to
    - Your function must be connected to the same VPC as the file system.
  - **Note:** The Lambda configuration tab lets us define general configuration settings like memory and ephemeral storage, triggers, permission, VPC access, tags, function URLs, monitoring, concurrency and EFS file system access.
	
**5) Best practices for lambda configurations?**
		1) **Memory and Timeout Settings**
			- Configure memory and timeout settings appropriately based on your function's requirements
		2) **Concurrent Execution Limits**
			-  Consider the concurrency limits for your Lambda functions, especially if your application experiences sudden spikes in traffic.
			- Use Amazon CloudWatch alarms to monitor concurrency usage and adjust limits accordingly.
		3) **Environment Variables**
			- Use environment variables to pass configuration values to your Lambda functions. This allows you to change settings without modifying code.
		4) **Logging and Monitoring**
			-   Enable detailed logging in your Lambda functions to capture useful information for troubleshooting and performance analysis.
			-   Use AWS CloudWatch Logs for centralized log management and set up log retention policies to manage storage costs.
			-   Implement custom metrics and alarms using CloudWatch Metrics to monitor function performance and resource utilization.
		5) **Error Handling**
			-   Implement robust error handling and retry mechanisms in your Lambda functions to handle transient failures and recover gracefully.
			-   Use dead-letter queues (DLQs) to capture and process failed invocations for further analysis.
		6) **Cold Start Optimization**
			-   Minimize cold start times by optimizing your Lambda function's code, reducing dependencies, and using languages with faster startup times (e.g., Node.js, Python).
		7) **Dependency Management**
			-   Package only necessary dependencies to minimize deployment package size and reduce cold start times.
			-   Use Lambda Layers to share common libraries across multiple functions and reduce duplication.

6) How basically lambda function in aws deploying multiple infrastructure?
7) Packaging deployment
8) How can we create deployment package?
9) We have a use case script execution run for taking 25 mins would u prefer in lambda or other ?
	- It is not possible to run Lambda function more than 15 minutes.
10) Write a sample AWS Lambda function.
11) What are event and context parameters in Lambda?
  
	- In AWS Lambda, when a function is invoked, it receives two parameters: the event and the context. These parameters provide information about the invocation and the execution environment to the Lambda function. Here's an overview of each:

	1.  **Event**:
	    
	    -   The event parameter contains the data that triggers the Lambda function's invocation. It can vary depending on the event source that triggers the function.
	    -   For example, if the Lambda function is triggered by an HTTP request through API Gateway, the event object will contain information such as the HTTP method, headers, query parameters, and request body.
	    -   If the function is triggered by changes in an Amazon S3 bucket, the event object will include details about the S3 object that triggered the invocation, such as the bucket name, object key, and event type.
	    -   The structure of the event object is specific to the event source that triggers the function. You can access the event data within your Lambda function's code to process the incoming event.
	    - https://docs.aws.amazon.com/lambda/latest/dg/lambda-services.html
	2.  **Context**:
	    
	    -   The context parameter provides runtime information about the Lambda function invocation and execution environment.
	    -   It includes properties such as the AWS request ID, function name, function version, memory limit, deadline (timeout), and remaining execution time.
	    -   The context object also provides methods for interacting with the AWS Lambda service, such as logging messages, retrieving credentials, and retrieving information about the execution environment.
	    -   The context parameter is particularly useful for monitoring and logging, as it allows you to access metadata about the function's execution at runtime.
	    -   Additionally, the context object can be used to control function behavior, such as modifying the function's response or handling errors.
	    - https://docs.aws.amazon.com/lambda/latest/dg/nodejs-context.html
	    - 
12) When a database has a 100-connection limit, how do you handle 1000 Lambda requests to the database?
	- May be we can use RDS Proxy if the database is RDS.
	- Other options are 
		1) **Connection Pooling**:
			- Implement connection pooling in your Lambda function to reuse existing database connections rather than creating new ones for each request.
			- Connection pooling maintains a pool of established database connections that can be reused by multiple Lambda invocations.
			- By managing the pool size and reusing connections, you can reduce the number of connections to the database and stay within the connection limit.
		2) **Adjusting Lambda Concurrency**
			- Adjust the concurrency settings of your Lambda function to control the number of simultaneous invocations.
			- By limiting the concurrency, you can prevent a surge of requests from overwhelming the database connection limit.
		3) **Rate Limiting and Throttling**:
			-   Implement rate limiting and request throttling mechanisms to control the rate of incoming requests to the Lambda function.
			-   By enforcing limits on the number of requests processed per unit of time, you can prevent spikes in traffic that could exceed the database connection limit.
			-   Use services like Amazon API Gateway or AWS Lambda throttling settings to enforce rate limits on incoming requests.
			- 
**13) How can you create/share common DB connection code among Lambdas?**
		- By RDS Proxy

14) Compare Lambda vs. EC2.
	1) **Compute Model**
		- *Lambda*: It is serverless where we just need to upload our code and AWS manages the infrastructure, automatically scaling it to handle incoming requests. We don't need to manage servers.
		- *EC2*: It is a virtual server services which allows us to provision and manage virtual machines(instances) in the cloud.
	2) **Event-Driven vs. Always-On**
		- *Lambda*: Lambda is event-driven and ideal for executing short-lived, stateless functions in response to events such as HTTP requests, file uploads, database changes, or scheduled events. It's well-suited for microservices, event-driven architectures, and serverless applications.
		- *EC2*: EC2 instances are always-on virtual machines that run continuously until stopped or terminated. They are suitable for applications that require long-running processes, persistent storage, or specific configurations not supported by serverless platforms.
	3)  **Scalability**
		- *Lambda*: Lambda scales automatically to handle incoming requests, from a few requests per second to thousands or more, without requiring manual intervention.
		- *EC2*: With EC2, you must manually scale the number and type of instances based on your application's requirements. You can use auto-scaling groups to automatically adjust the number of instances based on metrics such as CPU utilization or incoming traffic.
	4) **Maintenance and Management**
		- *Lambda*: AWS manages the infrastructure, including server provisioning, patching, and maintenance, allowing you to focus on developing and deploying code. You don't need to worry about managing operating systems or scaling infrastructure.
		- *EC2*: With EC2, you're responsible for managing and maintaining the virtual machines, including operating system updates, security patches, and scaling. You have full control over the configuration and management of the instances.
	5) **Cold Start and Warm-up**
		- *Lambda*: Lambda functions may experience a cold start latency when invoked for the first time or after a period of inactivity, as the execution environment is initialized.
		- *EC2*: EC2 instances are always running, so there's no cold start latency associated with them.

**15) How many ways can a Lambda be triggered?**
		1.  Synchronous Invocation
		    -   Lambda runs the function and waits for a response and then return the response.
		    -   The service which is calling the function will know if the function is completed successfully or not.
		    -   Example:
		        -   API Gateway invoking a function and returning an error code to the called.
		2.  Asynchronous Invocation
		    -   No Acknowledgement to let us know that the function has processed successfully.
		    -   The service calling the function is not notified if the function failed to complete successfully.
		    -   Example
		        -   S3 invoking a function when an object is created.
16) How do you deploy EC2 instances, API Gateway, and Lambda?
17) How do you invoke a Lambda to generate a PDF report on a daily basis?
	- We can use Event Bridge Scheduler to do that.
	- We can also use CloudWatch Events, where we can specify minutes, hours or even cron expression.
18) What is the Lambda max upload size?
	- The compressed deployment package (ZIP file) must be less than 50 MB, and the uncompressed package must be less than 250 MB
19) What are Lambda layers, and where do you create them?
	- Using the Lambda Layer we can store all the dependencies that are referenced by our Lambda function.
	- Once created a layer can be used by multiple functions that have the same dependencies. So **multiple function** can reference the same layer.
	- It reduces the size of your deployment package enabling our function to initialize faster.
20) How does SQS trigger Lambda?
	1.  Open the Amazon SQS console at  [https://console.aws.amazon.com/sqs/](https://console.aws.amazon.com/sqs/).
	2.  In the navigation pane, choose  **Queues**.
	3.  On the  **Queues**  page, choose the queue to configure.
	4.  On the queue's page, choose the  **Lambda triggers**  tab.
	5.  On the  **Lambda triggers**  page, choose a Lambda trigger.
	    If the list doesn't include the Lambda trigger that you need, choose  **Configure Lambda function trigger**. Enter the Amazon Resource Name (ARN) of the Lambda function or choose an existing resource. Then choose  **Save**.
	    
	6.  Choose  **Save**. The console saves the configuration and displays the  **Details**  page for the queue.
	    
	    On the  **Details**  page, the  **Lambda triggers**  tab displays the Lambda function and its status. It takes approximately 1 minute for the Lambda function to become associated with your queue.
	    
	7.  To verify the results of the configuration,  [send a message to your queue](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/creating-sqs-standard-queues.html#sqs-send-messages)  and then view the triggered Lambda function in the Lambda console.