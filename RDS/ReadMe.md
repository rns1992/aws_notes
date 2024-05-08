# RDS

### When would you use RDS?
- RDS is generally used for Online Transaction Processing (OLTP) workloads.

### What is OLTP?
- It processes data from transactions in real-time e.g customer orders, banking transactions, payments and booking systems.
- OLTP is all about data processing and completing large numbers of small transactions in real-time.

### What is OLAP?
- Processes complex queries to analyze historical data, e.g. analyzing net profit figures from the past 3 years and sales forecasting.
- OLAP is all about data analysis usgin large amount of data and complex queries that take long time to complete.

### Exam Tips
- RDS Database Types
	- SQLServer
	- Oracle
	- MySQL
	- PostgreSQL
	- MariaDB
	- Amazon Aurora
- RDS is OLTP workloads
	- Great for processing lots of small transactions, like customer orders, banking transactions, payments and booking systems
- Not Suitable for OLAP
	- Use RedShift for data warehousing and OLAP tasks, like analyzing large amounts of data, reporting and sales forecasting.

### Which RDS Types can be configured as Multi-AZ?
- SQL Server
- My-SQL
- MariaDB
- Oracle
- PostgreSQL

### What is purpose of Multi-AZ?
- Multi-AZ is for Disaster-Recovery, not for improving performance. 
- So you cannot connect to the standby when the primary DB is active.

###  What is Read Replica?
- It is a read-only copy of your primary application.
- It is used to improve the read performance of the application.
- For e.g running any analytics or preports on the copy of the database.
- It is for read heavy work loads.
- The read replica can be in the same AZ, or different AZ or completely in different region.
- Each read replica has different DNS name.
- *The read replica can be promoted to completely own database in which we can do read and write as well, but then it will break the rule of replication.*


### What are key facts for Read Replicas?
- Scaling Read Performance
	- It is primarily used for scaling and not for DR (Disaster Recovery)
- Requires Automatic Backup
	- Automatic backups must be enabled in order to deploy a read replica.
- Multiple Read Replicas are Supported
	- *MySQL, MariaDB, PostgreSQL, Oracle and SQL Server allow you to add upto 5 read replicas to each DB instance*.

### Difference between Multi-AZ and Read Replicas?
- Multi AZ
	- An exact copy of your production database in another Availability Zone.
	- Used for DR.
	- In the event of a failure, RDS will automatically failover to the standby instance.
- Read Replica
	- A read only copy of your primary database in the same AZ, cross AZ or cross-region
	- Used to increase or scale read performance.
	- Great for read-heavy workloads and takes the load off your primary database for read-only workloads,
	- eg. Business Intelligence reporting jobs.

### How many ways are there to BackUp data in RDS?
1) Database Snapshots
	- Manual, ad-hoc and user-initiated.
	- It provides a snapshot or a point in time copy of the storage volume attached to DB instance.
2) Automated Backup
	- Enabled by default
	- It creates a daily backups or snapshots that run during a backup window that you define.
	- Transaction logs are used to replay transactions.

### What are Automated Backups?
- Automated backups are done in three steps
	1) **Point-In-Time Recovery**
		- Recover your database to any point in time within a "retention period" of 1-35 days.
	2) Full Daily Backup
		- RDS takes a full daily backup or snapshot and also stores transaction logs that has hapened throughout the day.
	3) The Recovery Process
		- When you do a recovery, AWS will first choose the most recent daily backup and then apply transaction logs relevant to that day, up to the recovery point.
- Automated backups and snapshots are stored in S3 bucket with transaction logs.
- *Free Storage:* You get free storage spaceequal to the size of your database. So if you have an RDS instance of 10GB, then we will get 10GB worth of storage.
- *Define Backup Window:* During the backup window, storage I/O may be suspended for a few seconds while the backup process initializes and you may experience increased latency at this time.

### What are Database Snapshots?
1) Not Automated
	- DB Snapshots are done manually (i.e they are user initiated)
2) No Retention Period
	- Manual snapshots are not deleted even after you delete the original RDS instance, including any automated backups.
3) Backups to a Known State
- Back up your DB instance in a known state as frequently as you wish and the restore to that specific state ay any time. 

### Will the DB that is restored will be the same DB with same DNS endpoint?
- No, the restored version of the database will always be a new RDS instance with a new DNS endpoint for both types of backups.

### Does RDS Backups and snapshots supports encryption?
- It supports Encryption at Rest.
- We need to enable encryption at creation time by selecting the encryption option in the console.
- It is integrated with KMS. Encryption is done using the AWS Key Managment Service (KMS). AES-256 encryption.
- It includes all the underlying storage automated backups, snapshots, logs and read replicas.
- **We can not enable encryption on an unencrypted RDS instance.**

### How to create encrypted DB from Unencrypted DB?
- We can create snapshot of unencrypted snapshot. 
- Then we can create another snapshot which is encrypted from previous Snapshot.
- Then from encrypted snapshot we can create Encrypted DB. 


### Exam Tips
1) **Automated Backups**
	- Automated, enabled by default, you define the backup window.
	- Point-in-time snapshot plus transactional logs.
	- Retention period of 1-35 days.
	- Can be used to recover your database to any point in time down to the second with the retention period.
2) **Database Snapshots/Manual Snaphots**
	- It is initiated by user, ad-hoc.
	- Point-in-time snapshot only.
	- No retention period and stored indefinately.
	- Used to back up your DB instance to a known state and restore to that specific state at any time. e.g before making change to the production database. 


### What is RDS Proxy?
- RDS Proxy is a fully-managed, highly available, and easy-to-use database proxy feature of Amazon RDS that enables your applications to: 
	1) improve scalability by pooling and sharing database connections
	2) improve availability by reducing database failover times by up to 66% and preserving application connections during failovers
	3) improve security by optionally enforcing AWS IAM authentication to databases and securely storing credentials in AWS Secrets Manager.

### What are advantages of RDS Proxy?
1) Its serverless and scales automatically to your workload through pooling and sharing database connections.
2) Preserves application connections during failover.
3) Detects failover and routes request to standby quickly
4) Deployable over Multi-AZ protection from infrastructure failure
5) Up to 66% faster failover times.