# Dynamo DB

### What is Dynamo DB?
- Its cloud native No Sql database service for any scale
- It provides single digit millisecond response time at any scale.
- There are no server to manage, patch or to install software, maintain or operate
- It automatically scales table up and down to adjust capacity and performance.
- It has built in availability and fault tolerance.
- Under hood dynamo DB replicates the data in multiple availability zones.
- It also supports ACID transaction
- It key-value and document database.

### When should one consider Dynamo DB?
 - When we need unlimited throughput and storage.
 - Need to make database scalable.
 - Need always high availability for mission critical application
 - High level of data durability
 - Require consistent response time in single milliseconds at any scale
 - Application going global using global table

### When should one not consider Dynamo DB?
- Ad hoc query with join, subquery etc.
- Online analytical processing (OLAP) data warehousing application
- Require large object (BLOB) storage
- Dynamo item limit is 400 KB

### What are partition key and composite key in Dynamo DB?
- `Partition key` consist of single item/attribute
- `Composite key` consist of two attribute. i.e. partition key + sort key 
- `Partition key` is referred as hash attribute
- `Sort key` is referred as range attribute

### How does DynamoDB achieves multi AZ  high durability and high availability?
- For example we have 3 AZ for a table AZ-1, AZ-2, AZ-3. So when data is added into one AZ for ex. AZ-2 then  it gets replicated to AZ-1 and AZ-3.
- So in case of any failure in any AZ our data would be available in other AZ as a backup.

### How does replication happen in DynamoDB?
- For example we have 3 AZ for a table AZ-1, AZ-2, AZ-3. So any one AZ is selected as primary leader and the data is written in that AZ first.
- Once the data is written in primary leader AZ, after that under the hood it gets replicated to other 2 AZ.
- There can be possibility of latency during reading from other AZ while one a has just written it and yet to replicate it.

### What is Eventually Consistent Reads?
- Response might include stale data after write.
- If repeated read after short time, response returns latest data.
- By default, dynamo DB reads are eventually read consistent.

### What is strongly consistent read?
- It is change that we need to make in code, so that code will wait until the AZ is updated with latest data for read operation.
- Response has most up-to-date data.
- May have higher latency than eventually consistent reads.
- Specify strongly consistent read mode in code during reads.
- It uses more throughtput capacity then eventually capacity,

### What is throughput capacity?
- Dynamo Db throughput is measured in RCU (*Read Capacity Units*) and WCU (*Write Capacity Units*).

### How RCU is measured?
- One RCU = one strong consistent read request/second for item upto 4 KB
- One RCU = two eventually consistent read request/second for item upto 4 KB
- So for example I have an item with size 8 KB
	- 2 RCU's for one strongly consistent read/second
	- 1 RCU's for one eventually consistent read/second

### How is WCU measured?
- One WCU = one write for an item up to 1 KB/second
- So for example if the item size is 2 KB, then we need to spend 2 WCU's for one write request/second.

### A dynamo table is configured with 100 RCU and 40 WCU. How much data can be read and written each second?
- Read
	- 1 RCU = one strong consistent read/sec for 4 KB item
		-  100 RCU = (100 x (4 KB for strong consistent read)) = 400 KB
	- 1 RCU = two eventually consistent reads/sec for 4 KB item
		- 100 RCU = (100 x 2) x 4 KB = 800 KB
- Write
	- one write for 1KB = 40 KB per second write

### How many capacity modes are there in DynamoDB?
- **Provisioned capacity mode**
	- You can specify required RCU and WCU
	- Ability to setup autoscaling
- **On Demand capacity mode**
	- No need to specify read and write capacity requirements
	- Dynamo scales up and down with traffic

### Advantages of Global Table
- Multi-master enables low latency data access
- Multi-region redundance for Disaster recovery and High availability applications
- Replication latency typically under one second
- Go global in minutes - no code change required!

### How does global table works?
- It is a collection of one or more replica tables all owned by single AWS account.
- Each region have one replica table, so when user writes something in one replica table it get propogated automatically to other replica tables of other regions.

### Things about global table and replica table
- Every replica has a same table name and primary key.
- Partial replication or specific data replication is not possible
- Strong consistent reads/writes must be done in same region.
- Dynamo DB does not support strong consistent reads/writes across different regions.
- If the region is isolated or degraded then Dynamo DB keeps the track of un-synched data. Once the region is back to normal it performs synch.
- Monitor *ReplicationLatency* metric to track replication latency.
- On demand scaling or provisioned mode with autoscaling should be used
- All replicas should have same RCUs/WCUs

### What is homogeneous migration?
- Where source and target database are of same type that migration is called homogeneous migration.

### What is heterogeneous migration?
- The source and target DB are 2 different type of databases.
- For ex. moving postgress DB to DynamoDB.

### What is AWS Database Migration Service (DMS)?
- It helps to migrate database to AWS quickly and securely.
- Source database remains operational during the migration.
- Consolidate multiple source database into a single target database.
- It can do one time migration or continuous data replication.
- It is highly available and self healing.

### Why we need to use DMS?
- Because if we do it manually then we need to self manage Backup, Transformation and Restoration for source db.

### What is AWS Schema Conversion Tool (SCT)?
- It automatically converts source database objects to a format compatible with the target database.
- This objects includes schemas, views, stored procedures, functions.
- Any objects that can not be automatically converted are clearly marked so that they can be manually converted to complete migration.
- SCT also scans our application source code for embedded sql statements and convert them as a part of database schema conversion project.
- SCT supports apache cassendra to dynamoDb conversion.

### What are different ways to ingest data in to Dynamo DB?
- *Case 1*
	- Create AWS data pipeline and AWS EMR (Elastic MapReduce).
	- AWS EMR would be responsible for pulling data from S3 buckets and putting in DynamoDB
- *Case 2*
	- In case if the input source is Amazon S3/AWS SQS/ AWS Kinesis then we can use Lambda function.
	- This is not recommended for mass migration.

### Can we do migration faster in SCT?
- Yes we can do it. We need to deploy multiple SCT data extractor agents and run it in parallel for faster migration.

###  What is AWS Glue?
- It is serverless and fully managed extract, transform and load (ETL) service that makes it easy for customer to prepare and load their data for analytics.
- We can simply point AWS Glue to datastore. AWS and AWS Glue discovers your data using crawler and stores associated metadata, table definition and schema in the AWS Glue catalog.
- Once data is in catalog it is immediately, query able, searchable and available for ETL.
- It can be queried from Athena, Redshift and EMR.
- Another advantage of Glue is we just need to select source and target data, Glue automatically generates the ETL code for us. If we want we can do modification and add additional business logic in code.
- Once ETL job is ready we can schedule or invoke based on demand.

### What is the need to use Glue with Dynamo?
- Dynamo DB is not appropriate for big data analytics and ad hoc queries.
- Dynamo data need to be moved to an AWS service, such as S3, to conduct big data analytics.
- Glue can help to crawl Dynamo table and extract data into S3.
- It is exporting data into Dynamo DB not importing into DynamoDB.

### Best practice of using Glue with DynamoDB
- Increate RCU of Dynamo table so it does not impact the current application and Glue can read faster from Dynamo DB as it uses Dynamo DB table RCU.
- Increase Glue ETL job DPU(Data Processing Unit) for faster extraction and load.
- Use Glue with AWS Step Function service for serverless workflows.
- Use pySpark extensions for connecting to DynamoDB.
	- Adjust *dynamodb.throughtput.read.percentage*, default is 0.5

### How many different ways are there for DynamoDB backup?
1) On Demand Backup
2) Point in time Recovery or Continuous Recovery

### What is OnDemand Back-up Restore?
- It creates a full back up of DynamoDB anytime on when needed.
- Backups can be retained until it is deleted.
- We can restore in same or in different AWS region.
- Backup and restore do not affect table performance.
- Backups can be done using
	- AWS Console, AWS CLI
	- AWS Backup
	- Any service that can execute AWS API's
		- Lambda
		- ECT
		- EKS etc.

### What is Point-in-Time Recovery?
- It creates continuous incremental backups of Dynamo table.
- It restores to any point in time from 5 mins before current time to last 35 days.
- It helps to restore in same or different AWS region.
- Backups and restore do NOT affect table performance.
- Restore to a point in time can be done using
	- AWS Console, AWS CLI
	- By using any service that can execute AWS APIs like Lambda, EC2, EKS etc.
	- 
### What are different DynamoDB Error Components?
1) Http status code (e.g. 400)
2) Exception name (e.g. ResourceNotFoundException)
3) Error message (e.g. Requested resource not found: Table: tablename not found)

###  Why Dynamo Infrastructure Logging is required?
- In case if a user creates or deletes a table. 
- It helps for governance, compliance, operational and risk auditing of AWS account.
- Action taken by AWS user, role or AWS service are recorded in this infrastructure logging.
- So anytime any event happens that is undesirable we can take actions on it.
- We can do this by using AWS CloudTrail.
- It keeps record of actions.
- It stores the logs of action in S3 bucket in json format. We can integrate S3 bucket with AWS Lambda to perform actions like send email, SNS or perform any actions on user using it.

### What is DAX (DynamoDB Accelerator)
- It is highly available, in memory cache for DynamoDB.
- No functional code change is required. 
	- DAX supports same APIs as DynamoDB
- Microseconds range response, and no tuning required.
- On DAX for multiple DynamoDB table or multiple DAX for multiple Dynamo tables.

### Types of DAX caches?
1. Item cache
2. Query cache 

### What is Primary Key in DynamoDB?
- Primary key uniquely identifies each item in the table.
- There are 2 types of primary key
	1. Simple Primary Key: Hash is calculated for storing and reading
		1.  Partition Key (Hash Key)
	2. Composite primary key: Hash is calculated as well as we can apply range operators like less than, greater than etc for composite Key
		1. Partition Key (hash key)
		2. Sort Key (Range key) 

### How DynamoDB works internally?
- Data in DynamoDB is spread across multiple DynamoDB partitions.
- A partition is an allocation of storage for a table backed by SSDs (Solid State Drives).
- DynamoDB replicates partitions across 3 different AZ to make DynamoDB durable and highly available.
- *Simple Key Working*
	- When the data comes to write in DynamoDB, DynamoDB calculates hash of primary key (partition Key), then based on hash value of primary key it decides in which partition it need to store data into. Also while read it calculates hash of the partition key and decides which partition it needs to read into.
- *Composite Key Working*
	- For all the items with the same primary key, items are stored in ascending order of the sort key. We can apply range operators on sort key for retrieving, also it resides near to each other in underlying SSD. That is why it is called as range key

### How DynamoDB calculates number of partitions?
- (RCU/3000) + (WCU/1000) = # of partitions (rounded up).
- So for example if we create a table and allocate RCU=1500 and WCU=500, then it will be
	- (1500/3000) + (500/1000) = 0.5 + 0.5 = 1.
	- So DynamoDB will allocate 1 partition. 
- Down the line partition can change. **1 partition can handle only upt0 10GB of data**. If it increase beyond that then DynamoDB will allocate a new partition.
- In case if we decrease RCU and WCU then DynamoDB will reduce the partition accordingly. We don't have  to do explicitly any thing in that.
- In ideal case each partition will equally share RCU and WCU.

### What is hot partition?
- Partition which gets too much traffic and is busy is called hot partition. 

### What is difference between Primary Key and Partition Key?
- The primary key may consist of only the partition key (*simple primary key*) or both the partition key and a sort key (*composite primary key*), defining the *uniqueness and ordering* of items within the table. 
- The partition key is a required attribute of the primary key structure in DynamoDB, determining the physical partition and unique identification of items.

### What are best practice for selecting Primary Key?
- We need to choose the attribute which is uniquely distributed across all the partitions
- If we need range query then we can also select sort query with partition key.

### What is Secondary Indexes?
- In Amazon DynamoDB, a secondary index is a data structure that allows you to query your table using alternate attributes (other than the primary key) with efficient read access. Secondary indexes provide flexibility in querying your data by enabling queries on non-primary key attributes, improving query performance, and supporting various access patterns.
- We can create one or more secondary indexes.
- Unlike Primary Key, Secondary Key does not need to be unique.
- There are 2 types of Secondary Index
	1. **Global Secondary Index**
		- A GSI is an independent data structure with its own partition and sort keys that differ from those of the table's primary key.
		- Sort Key is optional in GSI.
		- A GSI is configured Global because queries on this index can spend all of the data in the base table across all partitions.
		- A Global secondary index is stored in its own partition space away from the base table and scale separately from the base table.
	2. **Local Secondary Index**
		- An LSI is similar to a GSI, but it shares the same partition key as the table's primary key and is stored in the same partition.
		- It must be composite. SO it need to have a partition key and sort key.
		- A local secondary index is local in the sense that every partition of a local secondary index is scoped to a base table partition that has the same partition key value.

### What is projection in DynamoDB?
- In Amazon DynamoDB, a projection is a way to specify which attributes should be included in the result of a query or scan operation. By default, a query or scan operation returns all the attributes of an item, but in many cases, you only need a subset of the attributes.
- Projection settings allow you to control the data that is returned in query results, which can impact query performance and the amount of data transferred over the network.
- There are three types of projection settings in DynamoDB:
	1. **All Attributes**
		- With this projection type, all attributes from the table are copied into the index. When you query the index, DynamoDB returns all attributes associated with the matching items.
		- This projection type ensures that all data is available in the index, allowing you to retrieve any attribute without accessing the table.
	2. **Keys Only**
		- With keys-only projection, only the key attributes (partition key and sort key) from the table are copied into the index.
		- When you query the index, DynamoDB returns only the key attributes associated with the matching items. Other attributes are not included in the query results.
		- This projection type is useful when you only need to retrieve the key attributes and plan to fetch additional attributes from the table using the retrieved keys.
	3. **Include**
		- With include projection, you can specify a list of specific attributes from the table to be copied into the index.
		- This projection type allows you to control which attributes are included in the query results, reducing the amount of data transferred over the network and improving query performance.

### What is difference between LSI and GSI?
- Refer to image attached in folder

### What is Encryption (Data Protection) at Rest?
- It is Server-side encryption with AWS Key Management Service (KMS).
- All DynamoDB tables are encrypted by default. We just need to choose KMS.
- KMS encrypts following
	- Table data
	- Primary key
	- LSI and GSI
	- Streams
	- Global Tables
	- Backups
	- DAX clusters

### What are different type of Encryption at Rest?
1. AWS owned CMK (Default) (CMK - Customer Managed Key)
	1. Key is owned by DynamoDB
	2. No additional charge
2. AWS managed CMK
	1. Managed by AWS KMS
3. Customer managed CMK
	1. Created, owned and managed by us
4. Specify KMS type during table creation
	1. Switch on existing table without any code impact
	2. IAM role needs to have encrypt/decrypt policy for customer managed CMK.


### How data is Protected in Transit?
- All DynamoDB traffic use HTTPS (SSL/TLS)
- Client side encryption provides protection in transit and rest
	- Encrypt data in application code with KMS
	- Encrypt selective attributes
	- Some fields can't be encrypted
	- AWS Encryption SDK available.
  


