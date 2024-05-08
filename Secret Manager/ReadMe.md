# Secrets Manager


### What is Secret Manager?
- Secret Managers allows us to protect and Store secrets for AWS Services, IT Resources and Applications.
- It allows to centrally manage secrets that are used to access resources inside and outside AWS.
- We can also automate rotation of secrets without code deployment.
- It also allows to secure secrets with control of fine-grain permissions and encryption with AWS KMS.

### What type of secrets are allowed to store in secret manager?
- Store secrets of RDS database
- RedShift cluster
- DocumentDB Database
- Other Databases
	- My SQL
	- PostgresSQL
	- Oracle
	- MariaDB
	- SQL Server
- API Keys

### What kind of information in stored in Secrets?
- Username and Port
- Server Address
- Database Name and Port

### How secrets are Encrypted using an AWS KMS Key?
- Secrets are encrypted using CMK(Customer Master Key).
- Its a logical representation of a master key, which holds a key material to encrypt up to 4KB of data.

### Can we configure rotation of secrets?
- Yes we can configure rotation for 30, 60, 90 or custom # of days till max 365 days.

### How secret rotation is performed?
- Secret rotation is performed by lambda. we can use new lambda or existing lambda function which triggers and perform rotation.


### What is difference between AWS Secrets Manager and AWS System Manager(Parameter Store)?
1) AWS Secrets Manager
	- Database Credentials
	- API Keys
	- Automatically Rotate keys
	- Provides security compliance related to DB keys.
2) AWS System Manager Parameter Store
	- Wider Use cases
	- Configuration Variables
	- License Keys

