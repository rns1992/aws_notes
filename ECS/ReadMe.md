# ECS (Elastic Container Service)

### How does ECS works in EC2 Launch Type?
- When we launch ECS container in AWS we are launching **ECS Tasks** on ECS Clusters.
- ECS Clusters are made of **EC2 instances**.
- When we use ECS Cluster with EC2 Launch type we must need to **provision and maintain the infrastructure** i.e. the EC2 instances.
- Which means that our Amazon ECS Cluster is going to be composed of multiple EC2 instances. This instances are little bit special because each EC2 instances must run the ECS Agent and then this ECS Agent is going to register each EC2 instance into specified ECS service and ECS Cluster. 
- When we start ECS tasks then AWS is going to starting and stopping the containers, which means that when we have new docker container then it is going to be placed accordingly on each EC2 instance
- Docker container are placed in EC2 instance that we provisioned in advance.
- Refer to diagram in folder.

### How does ECS works in Fargate Launch Type?
- It also launches Docker container on AWS but in this case we don't need to provision the infrastructure (no EC2 instance to manage)
- Its all **serverless**.
- In fargate type if we have an ECS cluster then we just create task definitions to define our **ECS tasks** and then AWS will run ECS Tasks for us based on the **CPU/RAM** we need.
- So in order to scale we just need to increase the number of tasks, we don't need to manage any EC2 instances.
- **More questions on Fargate in Exam**

### What is EC2 Instance Profile (IAM)?
- It is only applicable to EC2 Launch Type in ECS.
- It is used by *ECS agent*.
- With the help of EC2 Instance Profile ECS Agent can make API calls to ECS Service.
- It helps to send container logs to CloudWatch Logs
- Can pull Docker image from ECR
- It can reference sensitive data in Secret Manager or SSM Parameter Store.

### What is ECS Task Role?
- It helps to allow each task to have a specific role.
- We can use different roles for the different ECS Services we run.
- Task Role is defined in task definition.  

### Explain Load Balancers Integration with ECS?
1) **Application Load Balancer**
	- It is supported and works for most of the use case.
2) **Network Load Balancer**
	- It is recommended only for high throughput/high performance use cases or to pair it with AWS Private Link.
3) **Classic Load Balancer**
	-It is supported but not recommended (No advance features - **no Fargate supported**)

### Which Data Volumes can be used with ECS?
- We can use EFS (Elastic File Storage) with ECS.
- We can mount EFS file systems onto ECS tasks.
- It works for both EC2 and Fargate launch Types.
- Tasks running in any AZ will share the same data in the EFS file system.
- **Fargate + EFS = Serverless**
- Use cases: Persistent multi-AZ shared storage for your containers.
- **Note:**  Amazon S3 cannot be mounted as a file system.

###  Explain ECS Service Auto Scaling
- We can automatically increase/decrease the desired number of ECS tasks.
- Amazon ECS Auto Scaling uses AWS Application Auto Scaling based on below parameters
	- ECS Service Average CPU Utilization
	- ECS Service Average Memory Utilization - Scale on RAM
	- ALB Request Count Per Target - metric coming from ALB
- *Target Tracking*
	- Scale based on target value for a specific CloudWatch metric where above 3 parameters would be eligible
	- Target tracking scaling is a type of autoscaling that adjusts the number of tasks or services based on a target value for a specific metric.
	- You set a target value for a metric (e.g., CPU utilization) that you want to maintain, and ECS automatically adjusts the number of tasks or services to keep the metric as close to the target value as possible.
	- This type of scaling simplifies autoscaling configuration by automatically adjusting capacity in response to changes in workload, maintaining a consistent performance level.
- *Step Scaling*
	- Scale based on a specified CloudWatch Alarm
- *Scheduled Scaling*
	- Scale based on a specified date/time (predictable changes)
	- Scheduled scaling allows you to define scaling actions based on a schedule rather than on dynamic metrics.
	- You can specify scheduled scaling actions to add or remove tasks or services at specific times or dates, based on anticipated changes in workload patterns.
	- Scheduled scaling is useful for applications with predictable or recurring workload fluctuations, such as daily, weekly, or monthly peaks.
- ECS Service Auto Scaling (task level) != EC2 Auto Scaling (EC2 instance level)
- Fargate Auto Scaling is much easier to setup (because serverless) 

### How Auto Scaling EC2 Instances in EC2 Launch Type works?
- We can accommodate ECS Service Scaling by adding underlying EC2 instances.
- *Auto Scaling Group Scaling*
	- Scale your ASG based on CPU utilization.
	- Add EC2 instances over time.
- *ECS Cluster Capacity Provider*
	- Used to automatically provision and scale the infrastructure for your ECS Tasks
	- Capacity Provider paired with an Auto Scaling Group
	- Add EC2 Instances when you're missing capacity (CPU, RAM..)

### ECS Rolling Updates
- When updating from v1 to v2, we can control how many tasks can be started and stopped and in which order.
- So in case of ECS update screen we have 2 parameters
	1. Minimum healthy percent: 100
	2. Maximum percent: 200
- What both the parameters means is lets say I have 10 tasks running in my cluster. So my total health is 100%. In case if I want to do update then I need to start 10 more task with new updates which makes my health capacity to 200%. Once all are up then old 10 tasks will be deleted. So again my health is 100%
- Same way my minimum health is 100% and max is 150%. Then at a time only 5 new task will be added to 10 old tasks, making it 15. Once all 5 new tasks are up it will delete 5 old tasks and create 5 new task making total 15 tasks again. Once the rest 5 new tasks are up it will delete 5 old tasks as well. 

### What is AWS ECS Task definition parameters?
- Task definations are metadata in JSON form to tell ECS how to run a docker container.
- It contains crucial information such as
	- Image Name
	- Port Binding for Container and Host
	- Memory and CPU required
	- Environment variables
	- Network information
	- IAM Role
	- Logging configuration   (ex CloudWatch)
- Can define up to 10 containers in a Task Definition