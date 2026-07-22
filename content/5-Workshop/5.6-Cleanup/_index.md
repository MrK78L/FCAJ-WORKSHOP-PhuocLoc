---
title: "Verify and Clean Up AWS Resources"
date: 2026-07-20
weight: 6
chapter: false
pre: " <b> 5.6. </b> "
---

# Verify and clean up

Review CloudFormation, API Gateway, Lambda, DynamoDB, Cognito, S3, CloudFront, EventBridge, CloudWatch, and SNS. Record outputs and test results.

```powershell
aws sts get-caller-identity
cd backend
sam delete --stack-name cloffice-backend --region ap-southeast-1
```

If S3 buckets contain objects, compare their names with stack outputs before emptying them. Remove any separate WAF stack, check CloudFront and logging resources, and review Billing and AWS Budgets. Cleanup is irreversible; confirm the account, Region, stack, and bucket names first.
