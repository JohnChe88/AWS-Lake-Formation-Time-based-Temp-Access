<h1><p><u>AWS-Lake-Formation-Time-based-Temp-Access</u></p></h1>

### Disclaimer 
This project is not affiliated with, endorsed by, or directly related to Amazon Web Services (AWS). The methods and practices described herein may not align with AWS's standard recommendations. Users are advised to thoroughly review and test the code before deploying it in any production environment to ensure it meets their security and operational requirements.

### Introduction
This repository contains a Python-based workflow that automates time-based access control for AWS Lake Formation resources using AWS Lambda and Amazon EventBridge. This solution grants temporary access to AWS Lake Formation tables and automatically revokes it after a specified duration, enhancing security and compliance by ensuring that access is only available when necessary.

### Why Is It Useful?
In environments where data security and compliance are paramount, limiting access duration to sensitive data can significantly reduce risk. This workflow automates the process of granting and revoking access, eliminating human error and ensuring that permissions are only available for the time they are needed. It's particularly useful for scenarios involving temporary workers, short-term projects, or time-bound data analysis tasks.

### Example Use Case
A data analytics firm needs to grant a contractor temporary access to a specific dataset stored in Lake Formation for a period of 48 hours. Using this workflow, the firm can automate the process, ensuring the contractor only has access for the specified time, after which access is automatically revoked, thus maintaining data security and compliance.

### Prerequisites
Before you can use this workflow, you need to have the following:

* An AWS account with permissions to manage AWS Lambda, AWS Lake Formation, and AWS EventBridge.
* The AWS CLI installed and configured.
* Python 3.8 or higher.
* Basic familiarity with AWS services, particularly Lambda, Lake Formation, and EventBridge.
* Ensure the AWS Lambda for revokeLFAccess has Resource-based policy(under permission) statements has event.amazonaws.com and lambda:InvokeFunction

### Getting Started
Setting Up Your Environment
Clone the repository:

Copy code
```
git clone https://github.com/johnche88/AWS-Lake-Formation-Time-based-Temp-Access.git
```
```
cd AWS-Lake-Formation-Time-based-Temp-Access
```

### Install required dependencies:

Ensure you have Python 3.8+ installed. You can install required Python packages using pip:

#### Configuring AWS Resources
* Create IAM roles for AWS Lambda functions with permissions to access AWS Lake Formation(add as a data admin) and AWS EventBridge.

* Set up Lake Formation: Ensure your data lake is configured, and you have tables created in AWS Lake Formation to test the access control.

* Deploy Lambda functions: Upload the Python scripts to AWS Lambda. Ensure the IAM roles assigned have the necessary permissions.

* Configure EventBridge rules: Follow the instructions in the deployment section to create EventBridge rules that trigger your Lambda functions.



#### Usage
To initiate the workflow using API Gateway or UI backed with API gateway. Invoke the LF-access-grant AWS Lambda function with the necessary parameters (principal, table details, and access, duration). The function will grant access and schedule the revocation using AWS EventBridge based on the specified duration.
<b>Note</b> : You can use a UI and make this more dynamic for inputs like principal, table details, and access, duration

### AWS SAM Template Overview
This AWS SAM template provisions two AWS Lambda functions with specific roles and permissions designed for managing AWS Lake Formation access. It leverages IAM roles with predefined policies to allow the Lambda functions to perform operations such as granting and revoking Lake Formation permissions, alongside creating and managing CloudWatch Logs and EventBridge rules.

#### Deployment Steps
* Prepare Your Environment: Ensure you have AWS CLI and AWS SAM CLI installed and configured with your AWS account.
* Build the SAM Application: Navigate to the project directory and execute sam build. This command prepares your application for deployment.
* Deploy the SAM Application: Run sam deploy --guided to deploy your application. Follow the prompts to specify the stack name, AWS region, and other configurations. This process will create or update resources defined in the SAM template in your AWS account.
Confirmation: During deployment, you'll be asked to confirm resource changes and IAM role creation. Respond according to your preferences to proceed with the deployment.
* Execution Prompts Explanation
* Stack Name: Unique identifier for your stack.
* AWS Region: AWS region where your resources will be deployed.
* Confirm changes before deploy: Opt to review changes before they are executed.
* Allow SAM CLI IAM role creation: Permissions for SAM to create IAM roles needed for your Lambda functions.
* Disable rollback: Choose whether to preserve or rollback resources if the deployment fails.
* Save arguments to configuration file: Opt to save your deployment settings for future use.


### Contributing
Contributions are welcome! Please follow the guidelines in the CONTRIBUTING.md file for details on how to submit pull requests, report issues, or suggest enhancements.

### License
This project is licensed under the MIT License - see the LICENSE file for details.
