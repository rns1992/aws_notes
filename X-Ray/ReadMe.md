# X- Ray


### What is X-Ray?
- X-Ray is a tool which helps developers analyze and debug distributed applciations.
- It allows to troubleshoot the root cause of performance issues and errors.
- It provides a visualization of our application's underlying components called *X-Ray service map*.
- The X-Ray Service Map consists of information like Latency, HTTP status codes and Errors.

### Which services can be integrated with X-Ray?
1) **AWS Services**
	- We can use X-Ray with EC2, Elastic Container Service, Lambda, Elastic Beanstalk, SNS, SQS, DynamoDB, Elastic Load Balancer and API Gateway.
2) **Integrate With Your Apps**
	- We can use X-Ray with applications written in Java, Node JS, .NET, Go, Ruby, Python
3) **API Calls**
	- The X-Ray SDK automatically captures metadata for API calls made to AWS services using the AWS SDK.

### Explain X-Ray Architecture?
1) **Install The X-Ray Agent**
	- Install the agent on your EC2 instance.
2) **Configure**
	- Instrument your application using the X-Ray SDK.
3) **The X-Ray SDK.**
	- The X-Ray SDK gathers information from request and response headers, the code in your application and metadata about the AWS resources on which it runs and sends this trace data to X-Ray. e.g. incoming HTTP requests, error codes, latency data.

### What things are needed for configuring X-Ray?
1) X-Ray SDK
2) X-Ray daemon (In case of EC2 it need to run in same instance and in case of ECS it needs to run in separate container)
3) Instrument our application using the SDK to send the required data to X-Ray, e.g. data about incoming HTTP requests to your application.