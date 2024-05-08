# Lambda

### What is AWS Lambda?
- It is serverless compute where we can run our code in AWS without provisioning any servers.
- Lambda takes care of everything required to run your code, including the runtime environment.
- It supports Java, Go, PowerShell, Node JS, C#, Python and Ruby.
- We can upload our code to lambda and we are good to go.
- It offers enterprise features of Auto-scaling and high availability are already integrated in to Lambda service.

### Explain Lambda Pricing?
1) *Requests*
	- The first 1 million requests per month are free.
	- $0.20 per month per 1 million requests.
2) *Duration*
	- You are charged in 1 millisecond increments
	- The price dependents on the amount of memory you allocate to your lambda function.
3) Price per GB-second.
	- $0.00001667 per GB second.
	- A function that uses 512 MB and runs for 100ms.
	- So it would be 0.5 GB X 0.1s = 0.05 GB-seconds.
	- Which costs $0.00000000083
	- Also the first 400,000 GB-seconds per month are free.

### Use cases of Lambda in event driven.
1) **Event Driven**
	- Lambda functions can be automatically triggered by other AWS services or called directly from any web or mobile app.
2) **Triggered by Events**
	- These events could be changes made to data in an S3 bucket, or DynamoDB table. 
3) **Triggered by User Requests**
	- You can use API Gateway to configure an HTTP endpoint allowing you to trigger your function at any time using an HTTP request.

### Which AWS services can trigger Lambda?
- DynamoDB
- Kinesis
- SQS
- Application Load Balancer
- API Gateway
- Alexa
- CloudFront
- S3
- SNS
- SES
- CloudFormation
- CloudWatch
- CodeCommit
- CodePipeline

### How versions are maintained in Lambda?
- When you create a Lambda function there is only one version: $LATEST
- But when we upload a new version of the code to Lambda that new version will become $LATEST

### How to manage multiple versions?
- We can create multiple versions of our function code and use aliases to reference the version we want to use.
- For example in development environment, we might want to maintain a few versions of the same function.
- With the help of alias we can point to specific version of the function code and use it. 

### What is weighted alias?
- Suppose we have new versions which we want to test in production but we don't want 100% of traffic to flow in that version. Then we can opt for this option in **Create Alias** and select % of traffic that we want to redirect to that new version and rest of traffic to old version.

### Notes on Lambda Concurrent Execution Limit.
- Bu default we can execute **1000 concurrent** lambda function per second.
- If we are running serverless website which experience heavy load, then might we can hit the limit at some point.
- In case if we hit the limit then we will start seeing invocations being rejected - **429 HTTP status code**.
- The remedy is to get the limit raised by AWS support.
- **Reserved concurrency** guarantees a set number of concurrent executions are always available to a critical function.

### Notes on Lambda and VPC access.
- It is possible to enable Lambda to access resources that are inside a private VPC.
- In order to do that we need do configuration for VPC ID, private subnet ID and security group ID.
- Lambda is going to create Elastic Network Interfaces (ENI) using IPs from the private subnets. We need to add addition role in IAM policy to do that. The security group allows our function to access the resources in the VPC.


### What is Ephemeral state and Persistent Data Storage Patterns?
- Functions are stateless in lambda, meaning that you can't permanently store any data in the function (e.g. session data, customer data etc.)
- **Ephemeral** - (something is short-lived or passing quickly)
	- Lambda is not used for applications that need to run for longer than 15 minutes (e.g. a database application or a web server that needs to stay up and running)
- **Persisting Data**
	- In order to persist the data, the function must interact with data store (e.g. save it to S3, EFS or Dynamo DB)

### What are different Storage Options available in lambda?
- Native within Lambda
	- */tmp*
	- *Lambda layers*
- External storage options: *S3, EFS, DynamoDB* etc.

### What is */tmp* storage in Lambda?
- It is temporary storage in the **execution environment** of the Lambda function. By default, 512 MB is provided and can be configurable to 10 GB.
- It is like a cached File System where Data can be accessed by multiple invocations of your function sharing the execution environment in order to **optimize performance**. 
- Data is not persistent, so it is available only during the **lifetime of the execution** environment and once the execution is completed it will be not available. 
- It is not the place to store permanent data.


### What is the best way to use libraries in Lambda function?
1) **Adding Libraries in Zip File**
	- Additional libraries needed by the function can be included in your Lambda Deployment package (the ZIP file containing your code)
	- By this methods our package size will be increased as well as deployment time will be increased. So every new deployment can take time and also we are likely to encounter issues of Cold Start.
2) **Including Libraries in Lambda Layer** (Best Practice)
- We can add libraries and SDKs as a layer that can be accessed by multiple functions.
- If we have large dependencies for instance we can import image manipulation libs, graphics libs or any AWS version SDKs.
- We will then get better performance because our deployment will be faster as the ZIP file contains code which is smaller.
- **Note**: Using the Lambda layer is not going to be dynamic means we can't update it dynamically. We need to create a new layer and reference that.

### What are persistence storage options that are available outside of Lambda?
1) S3: Object Storage Only
	-	It allows to store and retrieve objects only. Its not a file system.
	-	So we cannot directly open and write data to objects stored in S3.
	-	Instead we can upload new data with new version.
2) **Elastic File System**
	- It is a **Shared File System** which acts like a file system where data is persistent and can be updated dynamically (e.g. we can open a file and write to it)
	- It is **mounted** by the function when execution environment is created and it can be shared across multiple invocations.
	- In order to use EFS our Lambda function must be in the Same VPC as our EFS file system.


### What are environment Variables?
- With the help of Lambda Environment variables we can adjust our function's behavior, **without changing** our code.
- We can pass different environment variables to configure our function to **behave differently** in our development environment that it does in production.
- It is pair of strings, a key and value pair (e.g. *key*: environment, *value*: development, *key*: databasename, *value*: mydevdb)
- **Note:** It needs to be defined before your version is published and it is locked when the version is published. So we need to make the changes like adding to env variables before the version is published or after making changes we need to republish the version.

### What are the things that we can configure in Lambda?
1) General Configurations
	- Memory
	- Ephemeral Storage
	- Function timeout
2) Triggers
	- The service or resource that is able to invoke your function
3) Permissions
	- The function's execution role determines the permissions that the function will have.
4) Function URL
	- An HTTPs endpoint used to access your function using a browser.
5) Tags
	- User defined key-value pairs that help organize functions
6) VPC
	- Allow your function to access resource that are in a custom VPC (e.g. a private VPC)
7) Monitoring and Operations Tools
	- CloudWatch, CloudWatch Logs, X-Ray (performance issues)
8) Concurrency
	- Reserved concurrency ensures that a critical function can always run and restrict other concurrent requests.
	- Provisioned concurrency lets your function scale consistently without any fluctuations in latency
9) File System
	- EFS file system that your function needs to connect to
	- Your function must be connected to the same VPC as the file system.
- **Note:** The Lambda configuration tab lets us define general configuration settings like memory and ephemeral storage, triggers, permission, VPC access, tags, function URLs, monitoring, concurrency and EFS file system access.

### How many ways are there for Lambda Invocation?
1) Synchronous Invocation
	- Lambda runs the function and waits for a response and then return the response.
	- The service which is calling the function will know if the function is completed successfully or not.
	- Example:
		- API Gateway invoking a function and returning an error code to the called.
2) Asynchronous Invocation
	- No Acknowledgement to let us know that the function has processed successfully.
	- The service calling the function is not notified if the function failed to complete successfully.
	- Example
		- S3 invoking a function when an object is created.

### How many ways are there for handling failures in Lambda while performing asynchronous invocation?
1) Lambda Retries
	- If the function returns an error lambda will automatically perform 2 retries.
	- Common failure can be because of something went wrong in the code or function timed out before processing has completed.
	- Lambda waits for one minute before first retry and if that also fails then it will wait 2 minutes before the second retry.
2) Dead Letter Queues (DLQ)
	- It is used to save failed invocations for further processing.
	- It is associated to particular version of a function.
	- It can even be configured to be an event source for another function, allowing us to reprocess events.
	- It is responsible for failures only.

### How many ways DLQs can handle failures in Lambda?
1) *SQS*
	- We can hold the **failed events** in the queue until they are retrieved.
	- For example if the function failed then it will send notification to SQS to persist message.
2) *SNS*
	- It sends notification about failed events to one or **multiple destinations**.
	- For example if Lambda fails then it will send notification to SNS and then SNS can send notification to user email, trigger another lambda and also sends notification an HTTP request.
3) *Lambda Destinations*
	- We can use Lambda Destinations to Optionally configure Lambda to send invocation records to another service.
	- If the invocation is successful we can send the record to one destination and if invocation fails we can send record to another destination.
	- For example we invocation is successful we can send record to SQS and save the successful record and if invocation fails then we can send record to SNS and notify user on email. 

###  How many types of Lambda Destinations are there?
1) SQS
	- Send message containing the error message to an SQS queue for a developer to review.
2) SNS
	- Send notification to the support team using email or SMS
3) Lambda
	- Trigger another Lambda function to start an automatic error-handling process.
4) EventBridge
	- A successful response can be used to trigger an EventBridge event so that successful invocations are tracked.

### How Lambda Deployment Package Works?
1) By Console
	- When creating a function using the console, a .zip file containing the code we have written in the console is automatically created by Lambda in background.
	- That zip file is our deployment package and it contains the application code and all the dependencies that we need need in our code.
2) Deployment Package
	- We can also create a deployment package ourself and upload directly from our local machine which can be up to 50 MB max size.

### What happens when our zip file is greater than 50 MB?
1) **Using S3**
	- In case our zip file is greater than 50 MB then we need to upload it to S3 in same region where our lambda function is there because direct upload from local machine is not supported for file size more than 50 MB.
	- Then we need to specify the S3 Object when we create the region.
	- This is the **limitation** in Lambda.
2) **Using Lambda Layer**
	- Using the Lambda Layer we can store all the dependencies that are referenced by our Lambda function.
	- Once created a layer can be used by multiple functions that have the same dependencies. So **multiple function** can reference the same layer.
	- It reduces the size of your deployment package enabling our function to initialize faster.

### What is the advantage of creating Lambda Layer over S3 for deployment package size greater than 50 MB?
- It reduces the size of deployment package which enables functions to initialize faster.
- Also multiple functions can reference the same layer.

#### Note 
	- We can only increase memory allocation in Lambda but not CPU. However if we increase memory allocation CPU memory will be automatically increased. 
	- By default we get only 128 MB of basic function memory and it is expandable up to 10,240 MB (10 GB). 

### What are different phases for executing a function in Lambda?
- There are 4 phases for execution environment
	1) Download Code
		- First time our function is invoked, Lambda creates the execution environment.
	2) Configure
		- Configuration using memory, runtime (e.g. Node JS), configuration
	3) Static Initialization
		- It runs function static initialization code, import libraries and dependencies.
		- It is the one which **adds latency** to function 
	4) Function Code
		- Runs the function

### What are the factors that contribute to Latency for Static Initialization?
- There are three factors that contribute to Latency
 1) Code:
	 - The amount of code that needs to run during the initialization phase.
 2) Function Package Size
	 - Including imported libraries, dependencies and Lambda layers.
  3) Performance
	  - Libraries and other services that require connections to be setup (e.g. connections to S3 or a database)

### Note: In case of import, don't import entire SDK instead import specific module that we need to use. Refer to screen shot.
