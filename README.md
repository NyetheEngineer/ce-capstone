## About The Project

This proposal outlines the development and deployment of a web application on AWS that will allow users to register, store their data, send email notifications, and provide a real-time monitoring dashboard. The application will leverage React.JS for the frontend and DynamoDB for the database.

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
   - API Gateway: Create an API endpoint for handling user registration requests. Ensure that you enable CORS (Cross-Origin Resource Sharing) to allow cross-origin requests.

3. Lambda Functions: Develop a Lambda function triggered by API Gateway to:

  - Validate User Data: Ensure data integrity.
  - Store User Data: Save user data using the AWS SDK in your Lambda function for DynamoDB interaction.
  - Send Email Notification: Send a welcome email using Amazon Simple Email Service (SES) upon successful registration.

4. Amazon CloudWatch
   - Integrate CloudWatch to log user activity, API calls, and errors for monitoring and troubleshooting.

5.	Amazon SNS (optional): Consider setting up a topic in Amazon SNS to publish real-time user login events.
   - The frontend can then subscribe to this topic to receive updates and display them on the dashboard.

## Front-end UI
   - Select a framework like React, Vue.js, or plain JavaScript to build the user interface. For the purposes of this project, we will use React to build the frontend user interface.

1.	Clone or create a new React application on your local machine.
2. Create a form component in the React application to collect user data. Include fields for full name, age, occupation, nationality, marital status, and email address.
3.	Install the required dependencies, including Axios, which will be used to make HTTP requests to the API Gateway.
4.	User Authentication: The web app will be integrated with Amazon Cognito for secure user registration and login.

## Dashboard
Dashboard Feature
The dashboard feature offers real-time visualization of application usage metrics, including:
 - Active user count
 - Total user count
 - User login timestamps
 - Nationality distribution

1. DynamoDB Table Setup:
   - Create a DynamoDB table to store user data, including attributes for logged-in status, timestamps, and nationality.

2. Lambda Function Development:
   - Develop a Lambda function to query the DynamoDB table for real-time data. Process the retrieved data for display on the dashboard.

3. API Gateway Integration:
   -	Set up an API Gateway endpoint to serve as the interface for the dashboard data.
   -	Configure routes and security measures to ensure secure communication between the frontend and Lambda function.
     
4. Frontend Implementation:
   -	Utilize a frontend framework  (React) to create the dashboard component.
   -	Fetch real-time data from the API Gateway endpoint and render it on the dashboard.

5. User Authentication:
   -	Employ AWS Cognito for user authentication and registration.
   -	Retrieve the number of registered users from Cognito using its SDK or API.

6. Dashboard Integration:
   -	Incorporate the retrieved user count into the dashboard component to display the total number of registered users.

7. Lambda Trigger:
   -	Configure the Lambda function to be triggered by DynamoDB table updates, ensuring real-time data reflection on the dashboard.

## Total Estimated Budget

1. AWS Services
   - AWS Amplify: $0.005 per request (estimate: 100,000 requests/month) = $500/month
   - AWS DynamoDB: [Estimate based on your expected data storage and throughput requirements]
   - AWS S3: [Estimate based on your expected storage usage]
   - AWS Cognito: [Estimate based on your expected user base]
   - AWS Lambda: [Estimate based on the number of Lambda invocations]
   - AWS SES: [Estimate based on the number of emails sent]

2. Development and Deployment
   - ADeveloper time: [Estimate based on the complexity of the project and developer rates]
   - AInfrastructure setup: [Estimate based on the time required to set up AWS resources]
   - ATesting and quality assurance: [Estimate based on the project's complexity and testing requirements]
   - ADeployment and maintenance: [Estimate based on the frequency of updates and maintenance tasks]

3. Tools and Services
   - Git and GitHub: $0 (free for public repositories)
   - React: $0 (open-source)
   - AWS CLI: $0 (included with AWS account)
   - Docker and DockerHub: [Estimate based on your usage of Docker and DockerHub]
   - Axios: $0 (open-source)

