# EC2

### What is full form of EC2?
- Elastic Compute Cloud

### What is EC2?
- Its like a VM, only hosted in AWS instead of your own data center.
- Designed to make web-scale cloud computing easier for developers.
- It provides capacity we want when we need it.
- We are in complete control of our own instances.

### What are different type of instances in EC2?
- On Demand
	- Pay by the hour or the second depending on the type of instance you run.
- Reserved
	- Reserved capacity for one or three years. Up to 72% discount on the hourly charge.
	- Reserved instance operate at a regional level. So if we spin up the instance outside the region of our reserved instance then we wont get discount on the new instance that we have initiated in new region 
- Spot instances
	- Purchase unsed capacity at a discount of up to 90%.
	- Prices fluctuate with supply and demand 
- Dedicated
	- A physical EC2 server dedicated for your use.
	- The most expensive option.
	- Its good for application which have software licencing which is tied to physical hardware

### When to use On Demand instances?
- Flexible
	- Low cost and flexibility of Amazon EC2 without any upfront payment or long-term commitment.
- Short-Term
	- Applications with short-term, spiky or unpredictable workloads that cannot be interrupted.
- Testing the Water
	- Application being developed or tested on Amazon EC2 for the first time.

### When to use Reserved instances ?
- Predictable Usage
	- Application with steady state or predictable usage.
- Specific Capacity Requirements
	- Application that require reserved capacity.
- Pay Up-Front
	- You can make up-front payments to reduce their total computing costs even further.
- There are 3 types of reserved instances.
	- Standard RIs
		- Up to 72% off on-demand proces
		- Can not upgrade to higher instance if needed.
	- Convertible RIs
		- Up to 54% off on-demand price. 
		- Has the option to change to a different Reserved Instance type of equal or greater value.
	- Scheduled Ris
		- Launch within the time window we define.
		- Matches our capacity reservation to a predictable recurring schedule that only requires a fraction of a day, week, or month.
		- For example batch job for specific time which are scheduled.

### When to use Spot instances?
- Flexible
	- Applications that have flexible start and end times.
- Cost sensitive
	- Application that are only feasible at very low compute prices.
- Urgent Capacity
	- Users with an urgent need for large amounts of additional computing capacity.

### When to use dedicated hosts?
- Compliance
	- Regulatory requirements that may not support multi-tenant virtulization
- Licensing
	- Great for licencing which does not support multi-tenancy or cloud deployments
- There are 2 types of Dedicated instances
	- On Demand
		- Can be purchased on-demand(hourly)
	- Reserved
		- Can be purchased as a reservation for up tp 70% off the on-demand price. 

### How many different ways are there to connect EC2 instance?
1. By putty through ssh. We need to have .ppk file that is generated during key-pair generation. We can use that file in our putty and connect to an instance.
2. By `Connect` option in web browser. It uses **EC2 Instance Connect** to connect with the instance in web browser.


### What is EC2 Image Builder?
- It allows to create virtual machine images and in AWS its known as AMI (Amazon Machine Images) and container images
- It is simple to use with Graphical interface.
- Once we create a image we can use EC2 to test and validate the image e.g. for security compliance and functionality, using AWS provided tests or our own custom tests.
- It automates the process of creating and maintaining images.
- When software updates are available, Image Builder can automatically create a new image, run validation tests on the new image and make it available it to the AWS region of our choice.
- It also allows to share our AMI's with other AWS accounts that we own.

### How does it works?
- Step 1:
	- Provide a base OS image e.g. Amazon Linux 2 AMI
- Step 2:
	- Define software to install e.g. .NET, Python, Node JS, latest security updates, latest kernel, security settings.
- Step 3:
	- Run tests on the new image. For example, does it boot correctly?
- Step 4:
	- Distribute the image to the regions of our choice 

### What is terminology  for Image Builder?
1) Image Pipeline:
	- Defines the configuration and end-to-end process of building images. Including the image recipe, distribution and test settings.
2) Image Recipe:
	- Image Builder creates a recipe for each image which can be shared version controlled and re-used.
	- Source Image: e.g. Amazon Linux 2 AMI
	- Build Components: e.g. Apache Tomcat
3) Build Components
	- The software components to include in the image.

### Exam Tips for EC2 Image Builder
- EC2 Image Builder automates the process of creating and maintaining AMI and Container images.
- Select base OS image, customize by adding software, test and distribute to your chosen region.
- Image Pipeline: Setting and process
- Image Recipe: Source image and build components
- Build components: The software to include.