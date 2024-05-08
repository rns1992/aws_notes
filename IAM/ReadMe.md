# IAM

### What does IAM stands for?
- It means Identity and Access Management
- It is a global service.

### What is root user?
- A user which wich AWS main account is created. Its creds shoukd not be shared with anyone.

### What are users?
- User are people with in your organization and can be grouped.

### What is Group?
- It contains users according to the purpose of group.
- It does not contain other groups.
- There are some users with does not belong to any groups.
- There can be user which are part of multiple groups.

### Why do we create users and groups?
- Because we want to allow users to use AWS account based on permissions that are allocated to particular group.

### What are IAM Permissions (IAM Policies)?
- Users or Groups can be assigned JSON documents called policies.
- This policies define the permissions of the user.
- In AWS we need to apply the least privilage principle: don't give more permissions that a user needs.

### What is difference bewteen policies and permissions in AWS?
- Set of policies define permission.

### Can we attach a policy to a user who does not belongs to any group?
- Yes we can create an inline policy and attach it.

### Can user have multiple policies attached?
- Yes a user can have multiple policies attached.

### Explain IAM policy structure?
- Consist of
	- `Version` - policy language version, always include "20120-10-17"
	- `Id` - an identifier fr the policy (optional)
	- `Statement` - one or more individual statements (required)
- Statement consist of
	- `Sid`: an identifier for the statement (optional)
	- `Effect`: weather the statement allows or denies access (Allow, Deny)
	- `Principal`: account/user/role to which this policy applied to 
	- `Action`: list of actions this policy allows or denies
	- `Resource`: list of resource to which the actions applied to

			{
				"Version": "2012-10-17",
				"Ïd": "S3-Account-Permissions",
				"Statement": [
					{
						"Sid": "1",
						"Effect": "Allow",
						"Principal": {
							"AWS": ["arn:aws:iam::1234567:root"]
						},
						"Action": [
							"s3:GetObject",
							"s3:PutObject"
						],
						"Resource": ["arn:aws:s3:::mybucket/*"]
					}
				] 
			}

### What are IAM Roles?
- Some AWS services will need to perform actions on our behalf in our account.
- It is just like some AWS user's need some permission to perform some actions on AWS services, just like that instead on users our services need some permission in order to perform action on other services. To do so, we will assign permissions to AWS services with IAM Roles.
- So this IAM Roles are just like users but are not intended to be used by physical people but instead they are used by AWS services.
- For example I have an EC2 instance and I want to perform some action on AWS, in order to do so I need to have one IAM Role that will help to get me information from AWS services by using that IAM Role.
- Common Roles:
	- EC2 instance Roles
	- Lambda Function Roles
	- Roles for CLoud Formation

### What are IAM security Tools?
- IAM Credentials Report (account-level)
	- Its a report that lists all your account's users and the status of their various credentials.
- IAM Access Advisor (user-level)
	- Access advisor shows the service permissions granted to a user and when those services were last accessed.
	- It helps to foloow principal of least privilage for a user.
	- We can use that information and revise our policies.

### What is IAM Password policy?
- Strong passwords =  higher security for your account
- In AWS, you can setup a password policy:
	- Set a minimum password length
	- Require specific character types:
		- including uppercase letters
		- lowercase letters
		- numbers
		- non-alphanumeric characters
	- Allow all IAM users to change their own passwords
	- Require users to change their own passwords
	- Require user to change their passwords after sometime (password expiration)
	- Prevent password reuse

###	What is MFA in AWS?
- Combination of password and security device we own.
- MFA device options in AWS
	- Virtual MFA Devices
		- Google Authenticator (phone only)
		- Authy 
	- UTF (Universal 2nd Factor Security Key)
		- YubiKey by Yubico. Its like pendrive
	- Hardware key Foob MFA Device
		- Provided by Gemalto
	- Hardware Key Fob MFA Device for AWS GovCloud (US)
		- Provided by SurePassId