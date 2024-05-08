# S3 (Simple Storage Service)


### What is S3?
- It's an object storage that provides secure, durable, highly-scalable object storage.
- It is very easy to use with simple web service interface.
- It is super scalable that allows you to store and retrieve any amount of data from anywhere on the web at very low cost.
- It manages data as objects rather than in file systems or data blocks.
- We can upload any type of file we can think of to S3.
- Examples: photos, videos, code, document, text files.
- It cannot be used to run an operating system or database.
- It provides *unlimited storage so the total volume of data and the objects we can store is unlimited*.
- *S3 Objects can range in size from a minimum of 0 bytes to 5 TB*
- S3 stores file in buckets which is similar to folders but not folders.
- When we upload a file to an S3 bucket we will receive an HTTP *200* code if the upload was successful

### How naming works in S3 for buckets?
- It has *Universal Namespace* means all AWS accounts share the S3 namespace. Each S3 bucket name is globally unique.
- Example of URL:
	- https://*bucket-name*.s3.Region.amazonaws.com/*key-name*
	- https://*fayecloudguru*.s3.us-east-1-amazonaws.com/*Ralphie.jpg*

### What is key, value, version and metadata in S3?
- **Key**: Its the name of object example: Ralphie.jpg
- **Value**: This is the data itself, which is made up of a sequence of bytes.
- **Version ID:** Important for storing multiple versions of same object
- **Metadata**: Data about the data you are storing, e.g. content-type, last-modified

### Explain how S3 maintains High Availability and High Durability?
- **Availability**: It is built from 99.95% to 99.99% service availability based on selected S3 tier.
- **Durability**: It is designed for 99.999999999% (11 9's) durability for stored data which means not even a single object will get corrupted. 

### What are characteristics of S3?
1) Tiered Storage
	- S3 offers a range of storage classes designed for different use cases.
2) Lifecycle Management
	- Define rules to automatically transition objects to a cheaper storage tier or delete objects that are no longer required after a set period of time.
3) Versioning
	- With versioning, all versions of an object are stored and can be retrieved, including deleted objects.


### How security is handled in S3?
1) **Server Side Encryption**
	- You can set default encryption on a bucket to encrypt all new objects when they are stored in the bucket.
2) **Access Control Lists (ACLs)**
	- Define which AWS accounts or groups are granted access and the type of access. You can attach S3 ACLs to individual objects within a bucket.
3) **Bucket Policies**
	- S3 bucket policies specify what actions are allowed or denied (e.g. allow user Alice to PUT but not DELETE objects in the bucket.)

### What is S3 Standard Tier?
1) High Availability And Durability
	- Data is stored redundantly across multiple devices in multiple facilities (>=3 AZs)
		- 99.99% Availability
		- 99.99999999% (11 9's) Durability
2) Designed for Frequent Access
	- Perfect for frequently accessed data.
3) Suitable for Most Workloads
	- The default storage class
	- Use case include websites, content distribution, mobile and gaming applications and big data analytics.


### What is S3 Standard-Infrequent Access (S3-IA)?
- It is designed for Infrequent accessed data.
- Rapid Access
	- Used for data that is accessed less frequently but requires rapid access when needed.
- You Pay To Access Data
	- There is a low per-GB storage price and a per GB retrieval fee.
- Use Cases
	- Great for long term storage, backups and disaster recovery files.
	- Minimum storage duration: 30 days.
- It has 99.9 % availability and 99.999999999 (11 9's) Durability

### What is S3 One Zone Infrequent Access?
- Its same like S3 IA but data is stored redundantly within a single AZ.
	- It costs 20% less than regular S3-IA
	- Great for long-lived, infrequently accessed, non-critical data
	- Minimum storage duration is 30 days.
	- It has same availability and durability.


### What is Glacier and what are different types of options?
- Glacier is very cheap storage option.
- Optimized for data that is very infrequently accessed
- You pay each time you access your data
- You only for archiving data.
- Its availability and durability is same as Standard Tier.
- There are 2 types of Glacier storage option
	1) Glacier
		- Provides long term data archiving with the retrieval times that range from 1 minute to 12 hours. e.g. historical data only accessed a few times per year.
	2) Glacier Deep Archive
		- Archives rarely accessed data with a default retrieval time of 12 hours. e.g. financial records that may be accessed once or twice per year. 180 days minimum.

### What is S3 - Intelligent Tiering?
- It automatically moves our data to the most cost effective tier based on how frequently we access each object.
- It optimize the cost. It added monthly cost fee is of $0.0025 per 1000 objects
- Its availability and durability is same as Standard Tier.
- There are 2 tiers in it. 
	1) Frequent
	2) Infrequent

### How is the Storage cost for all services?
- Standard
	- It has highest storage price compared to all tiers starting from $0.023 per GB to $0.021 per GB
- S3 Intelligent Tier
	- Frequent Access Tier starts from same as standard $0.023 per GB
	- Infrequent Access Tier is of $0.0125 per GB
- S3 Standard - Infrequent Access
	- $0.0125 per GB
- S3 One Zone - Infrequent Access
	- $0.01 per GB
- S3 Glacier
	- $0.004 per GB
- S3 Glacier Deep Archive
	- $0.00099 per GB

### How to Secure S3 Buckets?
- S3 is very private by default
	- It private by default. All newly created buckets are private by default.
	- By default only bucket owner can upload new files, read new files and delete file.
	- By default no public access
- **Bucket Policies**
	- We can setup control of bucket using Bucket policies.
	- It is applied at bucket level. The permissions granted by the policy apply to all of the objects within the bucket.
	- We can not apply bucket policy to individual bucket objects
	- It is useful when we have group of file in same bucket and they really ned to be accessed by same people.

### What is S3 Bucket Access Control Lists (Bucket ACLs)?
- It is applied at a object level. We can apply different permissions for different objects within a bucket.
- We can define which account or group are granted access and also the type of access e.g. read, write or full control.
- It provides fine grain control over objects in buckets. We can grant a different type of access to different objects within the same bucket. e.g. to apply different permissions for different objects, for different users and groups.


### What does S3 Access Logs does?
- It logs all the request made to the S3 Bucket.
- It is not configured by default. We need to configure and enable it.
- For example
	- Every time a user makes a request to upload a file, read a file or delete a file it gets recorded in S3 access Logs.
	- We can also have our logs written to another S3 buckets.

### What are S3 Encryption Options?
1) Encryption in Transit
	- SSL/TLS
	- HTTPS
2) Encryption at Rest: Server-Side Encryption
	- *SSE-S3* : S3-managed keys, using AES-256-bit encryption (**default enabled**)
	- *SSE-KMS* : AWS Key Management Service-managed keys
	- *SSE-C* : Customer-provided keys.
3) Encryption at Rest: Client-Side Encryption
	-	You can encrypt the files yourself before you upload them into S3.

### What is CORS in S3 bucket and how it is useful?
- CORS means Cross-Origin Resource Sharing.
- It can be used to allow resources in one S3 bucket to access resources located in another S3 bucket. 