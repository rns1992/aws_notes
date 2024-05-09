# SNS (Simple Notification Service)

## What is SNS?

- It is a Simple Notification Service.
- A web service that makes it easy to set up, operate and send notifications from the Cloud.
- Messages sent from an application can be immediately delivered to subscribers or other application.

## What are common use cases of SNS?

- **Push Notifications**
  - Helps to send push notifications to devices like Apple, Google, Fire OS, Windows and Android.
- **SMS and Email**
  - Send SMS text messages or email
  - Even send to Amazon Simple Queue Service (SQS) or any HTTP endpoint.
- **Lambda**
  - It can help to trigger Lambda sunctions to process the information in the message, publish to another SNS topic or send the message to another service.

## How does SNS works?

- It is a publish subscribe model.
- Application can publish or push the message to the topic and subscribers can subscribe a message from the topic to receive it.
- Notifications are delivered using a push mechanism that eliminates the need to periodically chech or poll for new information and updates.
- SNS delivers appropriately-formatted copies of the message to each sunscriber (e.g IOS, Android, SMS etc).
- All messages published to AWS SNS are stored redundantly across multiple Availability Zones.

## What are Key Benifits of using SNS?

- Instantaneous
  - Instantaneous, push-base delivery (no polling)
- Simple
  - Simple APIs and easy integration with applications
- Flexible
  - Flexible message delivery over multiple transport protocols
- Inexpensive
  - Inexpensive, pay-as-you-go model with no up-front consts.
- Easy To Configure
  - Web-based AWS Management Console offers the simplicity of a point-and-click interface.
- Managed Service
  - With all the high availability and durability features needed for a production enviornment.
  