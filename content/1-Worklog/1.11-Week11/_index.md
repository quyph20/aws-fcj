---
title: "Week 11 Worklog"

weight: 2
chapter: false
pre: " <b> 1.11. </b> "
---



### Week 11 Objectives:

* The goal is to understand Serverless architecture, cost advantages, and core components: Lambda, API Gateway.
* Practice building an end-to-end Serverless application and deploying it using the SAM framework.

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                   | Start Date | Completion Date | Reference Material                        |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 2   | - Serverless Concept and Advantages: Clearly understood Serverless architecture as a computing model where AWS manages the server infrastructure, and users only pay for actual consumption time. Grasped the advantages of cost optimization and unlimited auto-scaling.                                                                                                   | 11/17/2025 | 11/17/2025      |
| 3   | - Serverless Compute Service (Lambda): Mastered AWS Lambda as the core Serverless compute service, allowing the execution of Functions without provisioning or managing servers. Understood the concepts of Concurrency and Memory Allocation.                                              | 11/18/2025 | 11/18/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - API Gateway: Clearly understood Amazon API Gateway as a fully managed service that allows the creation, maintenance, monitoring, and securing of large-scale REST, HTTP, and WebSocket APIs to act as the Front-end for Lambda Functions. |  11/19/2025 |  11/19/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Serverless Authentication and Security (Cognito): Grasped Amazon Cognito as an identity management service, providing sign-up, sign-in, and access control features for web and mobile Serverless applications.                            |  11/20/2025 | 11/20/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - Serverless Deployment (SAM): Introduced AWS Serverless Application Model (SAM) as a framework that simplifies the deployment of Serverless applications by using shorthand syntax built on top of CloudFormation (from Week 10).                                                                                     | 11/21/2025 | 11/21/2025      | <https://cloudjourney.awsstudygroup.com/> |


### Week 11 Achievements:

* Serverless Function Deployment (Lambda): Wrote and deployed a simple Lambda Function (e.g., querying data from DynamoDB). Configured an IAM Role with the minimum necessary access permissions for the Function.

* API Construction (API Gateway): Set up API Gateway and created a new REST API. Configured a Method (e.g., GET /items) to integrate directly with the created Lambda Function.

* NoSQL Data Management (DynamoDB): Created a DynamoDB table to store application data. Tested the latency of the API after integrating the data-accessing Lambda.

* Full Stack Deployment with SAM: Used the AWS SAM CLI to package and deploy the entire Serverless architecture (Lambda + API Gateway + DynamoDB) through a single template.yaml file.

* Serverless Application Summary: Successfully completed the construction and deployment of an end-to-end Serverless application. Outcome: Grasped the application Modernization process by shifting from traditional server architecture to the Serverless model, which helps reduce idle costs and increase development speed.

* Key Takeaways: AWS Lambda forced me to think about breaking down logic into smaller functional units, aligning with the Microservices principle. Dependency management within Functions is also a challenge that needs careful handling in Serverless.
