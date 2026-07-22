---
title: "CloudOffice Architecture Overview"
date: 2026-07-20
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

# Workshop overview

CloudOffice combines a React/Vite frontend with an AWS serverless backend for customer and office-rental administration workflows.

![CloudOffice deployment architecture](/images/5-Workshop/5.1-Workshop-overview/cloudoffice-architecture.jpg)

- S3 and CloudFront host and distribute the frontend.
- API Gateway exposes the API; Cognito authenticates users.
- Lambda runs business logic, image processing, and contract checks.
- DynamoDB stores application data; S3 stores media and documents.
- EventBridge, CloudWatch, and SNS schedule, monitor, and alert.
- AWS SAM and CloudFormation define and deploy the stack.
