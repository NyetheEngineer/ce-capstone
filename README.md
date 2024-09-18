## About The Project

This proposal outlines the development and deployment of a web application on AWS that will allow users to register, store their data, send email notifications, and provide a real-time monitoring dashboard. The application will leverage React.JS for the frontend and DynamoDB for the database.

### Collaborations

I worked on this project with insightful contribution from the Cloud Navigators Team.

1. Dzandu Ransford Selorm - dzandu.selorm@azubiafrica.org
2. Jermin Amarteifio - jermin.amarteifio@azubiafrica.org
3. Alfred Mensah - alfred.mensah@azubiafrica.org
4. Ernest Kwabena Ofori Thompson - ernest.thompson@azubiafrica.org
5. Allan Loyatun - allan.loyatum@azubiafrica.org
6. Jully Achenchi - jully.achenchi@azubiafrica.org
7. Selma Anya - selma.anya@azubiafrica.org
8. Caesar Morris - caesar.morris@azubiafrica.org

## Technologies and tools used

- Git and GitHub
- React
- AWS Dynamo DB
- AWS Amplify
- AWS S3
- AWS Cognito
- AWS Lambda
- Docker and DockHub
- AWS SES
- AWS CLI
- Axios

## Project Overview
1. Build webapp to receive user details
2. Send users confirmation mail upon successful registration
3. Display user details on dashboard
4. Automate the project

## Prerequisites
1. An AWS account with appropriate permissions to create and configure AWS services.
2. Node.js and npm (Node Package Manager) installed on your local machine.
3. Docker installed and running

## Setup the Backend (AWS Services)

1. DynamoDB: Create an AWS DynamoDB table to store the user data. Take note of the table name and its attributes.

2. API Gateway
   API Gateway: Create an API endpoint for handling user registration requests. Ensure that you enable CORS (Cross-Origin Resource Sharing) to allow cross-origin requests.

3. Lambda Functions: Develop a Lambda function triggered by API Gateway to:

  - Validate User Data: Ensure data integrity.
  - Store User Data: Save user data using the AWS SDK in your Lambda function for DynamoDB interaction.
  - Send Email Notification: Send a welcome email using Amazon Simple Email Service (SES) upon successful registration.

4. Amazon CloudWatch
   Integrate CloudWatch to log user activity, API calls, and errors for monitoring and troubleshooting.

5.	Amazon SNS (optional): Consider setting up a topic in Amazon SNS to publish real-time user login events.
    The frontend can then subscribe to this topic to receive updates and display them on the dashboard.

   

## Front-end UI
Select a framework like React, Vue.js, or plain JavaScript to build the user interface. For the purposes of this project, we will use React to build the frontend user interface.
   
1. Configure AWS Credentials
   - Prerequisites: An AWS account with appropriate permissions.
Establish local access to your AWS account by configuring the AWS CLI using the aws configure command.
Refer to the official AWS documentation for detailed instructions: https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-configure.html

2. Create Terraform Project Directory
Create a dedicated directory on your local machine to store your Terraform configuration files for this project.

3. Define the AWS Provider (main.tf)
Create a file named ```text main.tf``` within your Terraform directory. This file will define the AWS provider, specifying the AWS region and credentials Terraform will use.

```
Terraform
# Configure Terraform AWS Provider
provider "aws" {
  region = "us-east-1"
}
```

4. Define DynamoDB Table (main.tf)
Within the same ```text main.tf file```, define the configuration for your DynamoDB table.

```text
Terraform
resource "aws_dynamodb_table" "GuestBook" {
  name           = "GuestBook"
  hash_key       = "Email" # Define your hash key attribute
  read_capacity  = 10
  write_capacity = 10

  attribute {
    name = "Email" # Define hash key attribute details
    type = "S"  # Specify attribute data type (String in this case)
  }

  # ... Define additional attributes and settings as needed...
resource "aws_dynamodb_table_item" "dynamodb_schema_table_item" {
  for_each = local.tf_data
  table_name = aws_dynamodb_table.GuestBook.name
  hash_key   = "Email"
  item = jsonencode(each.value)
} 
```

5. Loading JSON Data into Terraform

   - Create a file named ```text data.json``` within your Terraform directory. Include some data in the format shown:
     
   ```
        {
   	"item1": {
   		"Email": {
   			"S": "nyemitei.odjidja@azubiafrica.org"
   		},
   		"Name": {
   			"S": "Nyemitei Odjidja"
   		},
   		"Gender": {
   			"S": "male"
   		},
   		"Country": {
   			"S": "Ghana"
   		}
   	},
   	"Item2": {
   		"Email": {
   			"S": "jermin.amarteifio@azubiafrica.org"
   		},
   		"Name": {
   			"S": "Jermin Amarteifio"
   		},
   		"Gender": {
   			"S": "male"
   		},
   		"Country": {
   			"S": "Ghana"
   		}
   	}
   }
``
 
   - Create a file named ```locals.tf``` within your Terraform directory. It will read and decode the JSON data saved in ```data.json``` into Terraform data structure.
     
     ```
        locals {
        json_data = file("./data.json")
        tf_data   = jsondecode(local.json_data)
         }
     ```
     
6. Initialise Terraform
   Run the ```terraform init command``` within your Terraform project directory to initialize the working directory and download any required plugins for your configuration.

7. Preview Changes
   Execute the ```terraform plan``` command to preview the changes Terraform will make to your AWS environment based on your configuration files. This step helps you review the planned actions before applying them.

8. Apply Terraform Configuration
   Once you've reviewed the preview and are satisfied with the changes, run the ```terraform apply``` command to create the DynamoDB table in your AWS account as defined by your Terraform configuration.

# Deploying to DockerHub

1. Create a Dockerfile in the app folder. 

2. Build the Docker image using the following command: ```docker build -t your-dockerhub-username/docker-web-app:1.0``` .  

    - This will build a Docker image with the name "your-dockerhub-username/docker-web-app" and the tag "1.0".  

3. Push the Docker image to DockerHub using the following command: ```docker push your-dockerhub-username/docker-web-app:1.0```, 
   
