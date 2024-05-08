# CloudFront


### What is CloudFront?
- Its a Content Deliver Network service provided by Amazon.
- Its a system of distributed servers which deliver webpages and other web content.
- Its easy and cost effective way to distribute content with low latency and high data transfer speeds.
- It is much more efficient and performant way for geographically users to access the content.

### What is Edge Location?
- This is the location where content is cached. It is separated to an AWS Region/AZ.

### What is CloudFront Origin?
- This is the region of all the files that the distribution will server.
- It can be an S3 Bucket, an EC2 Instance and Elastic Load Balancer or Route 53.
- This is basically the origin server where all the files are present and will be pulled first time.

### What is CloudFront Distribution?
- This is the name given to the Origin and configuration settings for the content we wish to distribute using CloudFront(CDN). 

### Notes about CloudFront
1) Its optimized to work with other AWS Web Services.
2) Its integrated with AWS Services like S3, EC2, ELB and Route53.
3) It also works seamlessly with any non-AWS origin server, which stores the original, definitive versions of your files.

### What is TTL(Time to Live)?
- In CloudFront Objects are cached for a period of time which is their Time To Live.
- The default TTL is 1 day and when the TTL is over, the object is automatically cleared from the cache.
- We can clear the object from the cache ourself before the TTL is over, but we would be charged.
- So for example if we have updated one file in the origin and we want to delete the old file from CloudFront and replace with new file, then we would be charged for it.

### What is S3 Transfer Acceleration?
- S3 Transfer Acceleration enables fast, easy and secure transfer of files over long distance between you, end users and an S3 bucket. 
- As the data arrives at an edge location, it is routed to Amazon S3, over an optimized network path.
- So for example if a user is located in Asia and the origin S3 bucket in which the file needs to be uploaded is in Europe, then by S3 Transfer Acceleration, when the user uploads the File it will be uploaded to near edge location and from there it will be uploaded to origin S3 bucket.

### What is Origin Access Identity (OAI)?
- An OAI is a **special CloudFront user** that can access the files in our bucket and serves them to users.
- OAI allows us to **Restrict access** to the contents of our bucket, so that all users **must use the CloudFront URL** instead of a direct S3 URL.

### What are HTTP AllowedMethods in CloudFront?
- We have 3 options to choose from methods which are allowed in CloudFront.
	1) GET, HEAD
	2) GET, HEAD, OPTIONS
	3) GET, HEAD, OPTIONS, PUT, POST, PATCH, DELETE
- In order to select any of the above options we need to consider what users need to do on our website.
- For websites that are interactive, it allows users to do anything more than read (e.g. complete forms, upload data, write data, create shopping carts etc.) then we need to enable third option.
- 