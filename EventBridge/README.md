# EventBridge

## What is EventBridge?

- EventBridge is all about event-driven architecture. An event is a change in state.
- Amazon EventBridge is a serverless **event bus** service provided by Amazon Web Services (AWS) that makes it easy to connect different AWS services, SaaS applications, and your own applications using event-driven architecture.
- EventBridge enables you to capture events from different sources such as AWS services, custom applications, and third-party SaaS applications, and route these events to one or more targets such as AWS Lambda functions, Amazon SQS queues, Amazon SNS topics, AWS Step Functions, and more.
- EventBridge is using same underlying technology as **CloudWatch Events**.

## What are Scheduled Events?

- EventBridge rules can also run on a schedule.
- Example: Once an hour or day, using a cron expression, we can set a rule to run at the same time on a specified day, week or month.

## Exam Tips:

- EventBridge receives events relating to state changes in AWS e.g. an EC2 instance changes state like stopped, running, pending etc or a CloudWatch alarm changes state.
- We can use EventBridge to create rules that take actions based on the events it receives e.g. send an SNS notification.
- EventBridge and CloudWatch Events are using the same underlying technology.
