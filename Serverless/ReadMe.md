# Serverless


### What is Serverless?
- Serverless allows you to run your application code in the cloud without having to worry about managing any servers.
- AWS handles the infrastructure management task so that you can focus on writing code.

### Which services in AWS is serverless?
- AWS Lambda
- SQS (Simple Queue Service)
- SNS (Simple Notification Service)
- API Gateway
- Dynamo DB
- S3 Bucket
- Step Function
- AWS Fargate.

### Exam Tips
- Serverless enables you to build scalable applications quickly without managing any servers
- Its low cost, as serverless applications are event-driven and you are only charged when your code is executed.
- AWS Handles the heavy Lifting and we can focus on writing code and building our application instead of configuring servers.

### What are characteristics of Event-Driven Architecture?
1) **Asynchronous**
	- Events and asynchronous communication used to loosely couple application components. An event or message might trigger an action, but no response is expected or required.
2) **Loosely Coupled**
	- Services and components operate and scale independently of each other.
3) **Single-Purpose Functions**
	- Stateless functions performing a short lived task.