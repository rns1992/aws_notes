# CloudFormation

## What is AWS CloudFormation?

- It helps to manage, configure and provision our AWS infrastructure as a code.
- Resources are defined using a CloudFormation template.
- CloudFormation interprets the template and makes the appropriate API calls to create the resources ywe have defined.
- It supports YAML or JSON.

### What are benifits of CloudFormation Template?

- **Consistent**
  - It allows to provision our infrastructure consistently, with fewer mistakes. It will be same every single time.
- **Quick and Efficient**
  - It takes less time and effort than configuring things manually.
- **Version Control**
  - We can version control and peer review our template
- **Free to Use**
  - It is free to use but we are charged for the AWS resources we create using CloudFormation
- **Manage Updates**
  - It can be used to manage updates for different resources and also we can manage depedencies so that resources are created in correct order.
- **Rolling Back**
  - We can roll back to a previous state and delete the entire stack as well.

## Explain the process of CloudFormation.

1. **YAML or JSON Template**
    - YAML or JSON template used to describe the end state of the infrastructure we are either provisioning or changing.

2. **S3**
    - After creating the template, you upload it to CloudFormation using S3.

3. **API Calls**
    - CloudFormation reads the template and makes the API calls on your behalf.

4. **CloudFormation Stack**
    - The resulting set of resources that CloudFormation builds from your template is called a "stack".
