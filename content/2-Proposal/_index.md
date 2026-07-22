---
title: "CloudOffice Project Proposal"
date: 2026-07-20
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# CloudOffice – Office Rental Management System on AWS

## 1. Executive summary

CloudOffice is a cloud-native web platform where customers can search for offices, view detailed information, submit rental requests, and schedule office visits. Its administration area supports office, customer, rental-request, appointment, contract, image, and operational-report management.

The project uses an AWS serverless architecture to reduce server administration and scale based on actual usage. The frontend is built with React, TypeScript, and Vite. The backend uses Amazon API Gateway, AWS Lambda, and Amazon DynamoDB, while Amazon Cognito provides authentication and customer/administrator authorization.

## 2. Problem statement

Managing offices, customers, rental requests, and contracts through spreadsheets or disconnected applications creates inconsistent data and makes status tracking difficult. Images and contract documents also need controlled storage, while administrators require a centralized operational view.

CloudOffice addresses these needs by providing:

- Searchable office listings and detailed office information.
- Customer registration, authentication, profiles, and self-service features.
- Rental requests, office-viewing appointments, and personal contract tracking.
- Administrative management of offices, customers, requests, appointments, and contracts.
- Secure image and document storage through Amazon S3.
- Monitoring and email alerts for Lambda errors and expiring contracts.

## 3. Objectives and scope

### Objectives

- Build a web application that can be deployed on AWS.
- Apply serverless services to avoid managing application servers.
- Separate customer and administrator access with Cognito and JWT authorization.
- Store operational data using a DynamoDB single-table design.
- Process uploaded images and check contract expiration automatically.
- Establish logging, alerting, deployment, and cleanup procedures.

### Functional scope

- Landing page, office search, office listing, and office details.
- Registration, sign-in, user profiles, and avatars.
- Rental requests, viewing appointments, and customer contracts.
- Admin dashboard, Customer 360, floor plans, and rental-request pipeline.
- CRUD operations for offices, customers, requests, appointments, and contracts.
- Presigned uploads for office images, avatars, and contract documents.
- CSV reports, operational monitoring, and contract-expiration alerts.

## 4. Solution architecture

![CloudOffice overall architecture](/images/2-Proposal/cloudoffice-architecture.jpg)

CloudOffice does not require a VPC in its current architecture. The backend uses regional managed and serverless AWS service endpoints.

### Main request and event flows

1. Customers and administrators access the React frontend stored in S3 and optionally distributed through CloudFront.
2. The frontend sends HTTP requests to Amazon API Gateway.
3. Amazon Cognito authenticates users, and the JWT authorizer protects private endpoints.
4. The Business Logic Lambda processes requests and reads or writes DynamoDB records.
5. Images and documents are uploaded directly to S3 through temporary presigned URLs.
6. An S3 object-created event invokes the Image Processor Lambda, which writes optimized images to the processed bucket.
7. EventBridge invokes the Contract Expiry Notifier Lambda every day.
8. CloudWatch stores logs and metrics; CloudWatch Alarms and SNS deliver operational email notifications.

### AWS services

| AWS service | Responsibility |
| --- | --- |
| Amazon S3 | Store frontend assets, original uploads, processed images, and contract files. |
| Amazon CloudFront | Optionally distribute the frontend over HTTPS using a private S3 origin. |
| Amazon API Gateway | Expose the CloudOffice HTTP API. |
| AWS Lambda | Run business logic, image processing, and contract-expiration checks. |
| Amazon DynamoDB | Store offices, customers, requests, appointments, and contracts. |
| Amazon Cognito | Register and authenticate users and maintain the administrator group. |
| Amazon EventBridge | Schedule the daily contract-expiration check. |
| Amazon CloudWatch | Store logs, metrics, and Lambda error alarms. |
| Amazon SNS | Send operational and contract-expiration email alerts. |
| AWS SAM/CloudFormation | Define, create, update, and remove AWS infrastructure. |
| AWS WAF | Provide optional CloudFront protection when production budget allows. |

## 5. Technical design

### Frontend

- React 18, TypeScript, and Vite.
- Environment variables provide the API URL and Cognito identifiers.
- Public and administrative interfaces are separated by authentication and role checks.
- The production build is stored in a private S3 bucket and can be distributed through CloudFront Origin Access Control.

### Backend

- Node.js 22.x Lambda runtime.
- Business Logic Lambda implements office, customer, request, appointment, contract, profile, upload, and report APIs.
- Image Processor Lambda is invoked by S3 events and uses `sharp` to optimize images.
- Contract Expiry Notifier Lambda runs on an EventBridge schedule and publishes alerts to SNS.

### Data and security

- DynamoDB uses `PK`, `SK`, and three Global Secondary Indexes for different query patterns.
- S3 buckets enable server-side encryption and Block Public Access.
- Private APIs require Cognito JWTs; backend logic also verifies the `admin` group.
- Each Lambda IAM Role receives only the DynamoDB, S3, or SNS permissions it needs.
- Optional DynamoDB point-in-time recovery can be enabled for production data.

## 6. Implementation plan

| Phase | Activities |
| --- | --- |
| Analysis | Identify users, functions, data, security, and operational requirements. |
| Architecture | Draw the AWS architecture and design API and DynamoDB access patterns. |
| Development | Implement the React frontend, Lambda functions, and AWS SAM template. |
| Backend setup | Build and deploy the SAM stack, seed DynamoDB, and configure Cognito. |
| Frontend setup | Configure environment variables, build React, upload to S3, and optionally enable CloudFront. |
| Verification | Test workflows, authorization, uploads, alerts, logs, and error handling. |
| Operations | Restrict CORS, configure budgets, document troubleshooting, and define cleanup procedures. |

## 7. Cost approach

CloudOffice favors usage-based services such as Lambda, API Gateway, and DynamoDB On-Demand. In a learning environment with limited traffic, usage should remain low, but actual cost still depends on request volume, S3 storage, data transfer, CloudFront traffic, and CloudWatch log retention.

An AWS Pricing Calculator estimate and AWS Budget alert should be created before deployment. AWS WAF remains optional because it introduces an additional fixed monthly cost before request charges.

## 8. Risks and mitigation

| Risk | Mitigation |
| --- | --- |
| Incorrect CORS configuration | Allow only the active local or CloudFront frontend origin. |
| Improper administrator authorization | Combine Cognito groups, JWT authorization, and backend permission checks. |
| Credential exposure | Keep access keys out of source code and use IAM Roles. |
| Accidental public S3 access | Enable Block Public Access and use presigned URLs and CloudFront OAC. |
| Accidental data deletion | Consider DynamoDB point-in-time recovery for production. |
| Image-processing failure | Validate file type and size and inspect CloudWatch Logs. |
| Unexpected cost | Configure AWS Budgets, limit log retention, and enable optional services only when required. |

## 9. Expected outcomes

- A working customer and administrator office-rental platform.
- Repeatable serverless infrastructure deployment through AWS SAM.
- Secure authentication, authorization, data, media, and contract-document handling.
- Operational monitoring and email alerts through CloudWatch and SNS.
- Deployment, verification, troubleshooting, and cleanup documentation.
