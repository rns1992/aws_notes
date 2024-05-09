# CloudWatch

## What is CloudWatch?

- Amazon CloudWatch is a monitoring service to monitor the health and performance of your AWS resources, as well as the applciations that you run on AWS and in your own datacenter.

## What can CloudWatch Monitor?

- **Compute**
  - EC2 instances
  - Auto Scaling groups
  - Elastic Load Balancers
  - Route53 health checks
  - Lambda
- **Storage & Content Delivery**
  - EBS volumes
  - Storage Gateway
  - CloudFront
- **Database & Analytics**
  - DynamoDB tables
  - ElasticCache modes
  - RDS instances
  - Redshifts
  - Elastic Map Reduce
- **Other**
  - SNS topics
  - SQS queues
  - API Gateway
  - Estimated AWS charges

## What is CloudWatch Agent?

- It allows to define our own metrics.

## What is CloudWatch Logs?

- It allows us to maintain application and operating system logs.
- It can monitor and troubleshoot our applications using existing system and application log files.
- We can monitor logs in near-real time for specific phrases, values or patterns but it requires CloudWatch Agent as the frequency is customized.
- We can track number of errors that occur in our application log and send yourself a notification whenever the rate of errors exceeds a thresold we specify.

## How Operating System metrics is collected in EC2?

- By default EC2 does not send operating system level metrics to CloudWatch.
- By installing **CloudWatch Agent** on your EC2 instances, you can collect operating system metrics and send them to CloudWatch.
- Data such as Memory Usage, processes running on your instances, amount of disk space, CPU ideal time etc can be collected.

## How frequently does EC2 Send Metrics to CloudWatch?

- By default, EC2 sends metric data to CloudWatch in 5 minutes intervals.
- For an additional charge you can enable detailed monitoring that sends metrics at 1-minute interval.
- For custom metrics, the default is 1-minute intervals, and you can configure high resolution metrics that are sent at 1 second intervals.

## What is CloudWatch Alarm?

- We can create an alarm to monitor any Amazon CloudWatch metric in your account.
- Alarms
  - This can include EC2 CPU utilization, Elastic Load Balancer latency, or even the charges on our AWS bill.
- Thresholds
  - We can set appropriate thresolds to trigger the alarm and actions to be taken if an alarm state is reached.
- Use Cases
  - We can set an alarm that sends us a notification or executes an Auto Scaling policy if CPU utilization exceeds 90% on your EC2 instance for more than 5 minutes.
- CloudWatch can send us email notification using an **SNS Topic**.


## What are CloudWatch Dashboards?

- CloudWatch Dashboards are customizable collections of graphs and widgets that allow users to visualize and monitor various metrics and resources within their AWS environment in real-time.
- These dashboards can display metrics such as CPU utilization, network traffic, database performance, and more, allowing users to gain insights into the health and performance of their AWS infrastructure.
- Widget can be created based on CloudWatch Metrics or CLoudWatch Logs.
- Dashboards supports multi-region. We can change the region and add the widget we want.

## What are CloudWatch Metrics?

- A metric is simply a variable that we want to monitor using CloudWatch.
- A CloudWatch metric consist of Time ordered **sequence** of values or data-points, which are published to CloudWatch.
- Each data-point in a metric has a **timestamp**, and optionally, a unit of measurement.
- Example: The CPU usage of an EC2 instance.
- Metrics are uniquely defined by a **name**, a **namespace**, and zero or more **dimensions**.

## What is CloudWatch Namespaces?

- A namespace is a container for CloudWatch metrics. (e.g. EC2 uses the AWS/EC2 namespace). Create our own namespace to publish custom metric data.
- We must **specify** a namespace for each data point or value that we publish to CloudWatch.
- We must specify the namespace name when we create a **metric**.
- Metrics in **different** namespaces are **isolated** from each other.
- Metrics from different applications are **not aggregated** into the same statsics.
- **Note**: Custom metrics appear under Custom Namespaces, while the default AWS metrics appear under the AWS Namespaces. We can send custom metrics from different applications to different namespaces, allowing us to segregate metrics collected from different applications.

## What are CloudWatch Dimensions?

- A dimension is like a filter.
- It is a name-value pair that can be used to **filter** CloudWatch data.
- We can use **InstanceId** dimension to search for metrics relating to a specific EC2 instance.
- CloudWatch can aggregate data across dimensions for some services (e.g. EC2).

## What is CloudTrail?

- It records user account activity in our AWS account.
- It records events related to creation, modification or deletion of resources (such as IAM users, S3 buckets and EC2 instances)
- By default we can view the last 90 days of account activity.

## What is difference between CLoudWatch and CloudTrail?

- Refer to image attached in folder.

## What is CloudWatch Actions?

- It allows us to publish, monitor and alert on a variety of metrics.
- **PutMetricData**
  - It publishes metric data points to CloudWatch.
- **PutMetricAlarm**
  - It creates an alarm associated with a metric to alert you if a threshold has been reached.

## What is CloudWatch Log Insights?

- With the help of CloudWatch Log Insights we can execute query and analyze data stored in CloudWatch Logs.
- Wd can query the Logs directly and generate visualizations e.g. bar graph, line graph, pie chart etc.
- Example:
  - Display 25 mostrecently added log events.
  - Find the most expensive Lambda request