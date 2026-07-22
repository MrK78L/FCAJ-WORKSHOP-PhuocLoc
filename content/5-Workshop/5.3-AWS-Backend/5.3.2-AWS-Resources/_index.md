---
title: "Verify and Initialize Backend Resources"
date: 2026-07-20
weight: 2
chapter: false
pre: " <b> 5.3.2. </b> "
---

# Verify AWS resources

Retrieve stack outputs:

```powershell
aws cloudformation describe-stacks --stack-name cloffice-backend --region ap-southeast-1 --query "Stacks[0].Outputs"
```

Verify API Gateway routes, all three Lambda functions, the DynamoDB table and GSIs, Cognito pool/client/admin group, three private encrypted S3 buckets, CloudWatch logs/alarm, and the SNS topic. Confirm the SNS email subscription.

Seed DynamoDB:

```powershell
cd backend
npm run seed -- --table cloffice-offices-table --region ap-southeast-1
```

Create a Cognito administrator, set a permanent password, add it to `admin`, and verify the public `/offices` API.
