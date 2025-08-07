# lab24-serverless-backend-logging
This lab demonstrates how to build a secure, scalable serverless backend using AWS Lambda and API Gateway. It includes API integration, access logging, deployment to a stage, and monitoring using CloudWatch.
Lab 24: Secure Serverless Backend with Lambda & API Gateway + Logging

Author

Dr. Ime BenAWS Account ID: 2853-0598-8025

Overview

This lab focuses on building a secure, serverless backend infrastructure using AWS Lambda and API Gateway. It demonstrates how to:

Set up and integrate an AWS Lambda function with API Gateway.

Secure the backend with proper route control.

Enable access logging for monitoring and diagnostics.

Deploy to a specific API Gateway stage.

Monitor usage via CloudWatch.

Objectives

Deploy a serverless API using AWS Lambda and API Gateway.

Enable and configure CloudWatch logging for all API activity.

Test the deployed endpoint.

Understand the importance of secure, monitored, and observable backend services in a production environment.

Tools Used

AWS Lambda: For running serverless compute logic.

API Gateway (HTTP API): For exposing the Lambda function as an HTTPS endpoint.

Amazon CloudWatch: For monitoring and logging API calls.

IAM: For permissions and role-based access control.

Implementation Procedure

Step 1: Create a Lambda Function

Name: SecureBackendFunction

Runtime: Python or Node.js (custom code omitted here)

Permissions: Attach a basic execution role with permissions for logging (AWSLambdaBasicExecutionRole).

Step 2: Create an HTTP API via API Gateway

Name: SecureBackendAPI

Route: /SecureBackendFunction

Method: ANY

Integration: Lambda proxy integration with SecureBackendFunction

Step 3: Enable Access Logging

Navigate to Logging under Monitor.

Enable access logging.

Define log group: /aws/apigateway/SecureBackendAPI

Use structured JSON log format with key context variables like requestId, sourceIp, user, etc.

Step 4: Deploy to Stage dev

Select Deploy > Choose Stage: dev

Add description: "Initial deployment with logging enabled."

Save and deploy.

Step 5: Retrieve Invoke URL

Format: https://<api-id>.execute-api.<region>.amazonaws.com/dev/SecureBackendFunction

Example from this lab: https://6032xw3nbj.execute-api.eu-west-1.amazonaws.com/dev/SecureBackendFunction

Step 6: Test API

Open browser or Postman.

Send GET request to the above URL.

Verify 200 OK response and backend logic (e.g., Hello World).

Step 7: Check Logs in CloudWatch

Go to CloudWatch > Log Groups > /aws/apigateway/SecureBackendAPI

View entries confirming request context, IP address, etc.

Strategies & Approach

Use modular serverless design.

Separate backend logic (Lambda) from routing logic (API Gateway).

Implement logging as a default practice, not optional.

Use JSON log format for easier parsing and automation.

Deploy in stages (e.g., dev, test, prod) to ensure CI/CD readiness.

Significance and Importance in Real Work Environments

Why It Is Desperately Needed:

Serverless is the future: Reduces infrastructure costs and management.

Security First: Fine-grained control of routes and permissions.

Observability: Every request is logged, monitored, and traceable.

Compliance: Logs help in demonstrating API usage for audits.

Scalability: API Gateway + Lambda supports scale-out without complex infrastructure.

Rapid Deployment: Infrastructure as Code (future enhancement) allows automated rollouts.

Must-Do Best Practices

Enable logging from day one.

Avoid open permissions on Lambda.

Use descriptive names for routes.

Tag all resources for easy cost tracking and auditing.

Clean up unused stages and log groups.

Challenges Encountered

Identifying the correct ARN for logging destination.

Confusion between HTTP API and REST API setup.

Lambda timeouts and integration issues.

Forgetting to deploy after setting up routes (changes won’t go live otherwise).

Limitations

No authentication or API Key protection enabled.

No WAF applied.

No backend database integration (future enhancement).

No throttling or rate limiting yet.

Next Steps

Add CORS policy and test with front-end application.

Secure API with Cognito or IAM Authorizer.

Integrate with DynamoDB or RDS.

Create CI/CD pipeline for automated deployment.

GitHub Repository

https://github.com/ime-cloud-sec-analyst/lab24-serverless-backend-logging

Summary

This lab showcases the real-world need for deploying secured, observable, and scalable serverless APIs. By combining Lambda, API Gateway, and CloudWatch, organizations can deploy fast, secure, and cost-efficient backend services that are production-ready and auditable from the start.
