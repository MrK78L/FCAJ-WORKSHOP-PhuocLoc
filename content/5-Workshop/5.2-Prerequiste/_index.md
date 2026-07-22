---
title: "Set Up the AWS Account, IAM, and Tools"
date: 2026-07-20
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---

# Prepare the AWS environment

1. Select `ap-southeast-1` as the main Region.
2. Enable root MFA and use a separate IAM or Identity Center user for deployment.
3. Grant only the permissions needed by the CloudOffice SAM stack.
4. Create an AWS Budget and configure email alerts.
5. Install Node.js 22.x, npm, AWS CLI v2, SAM CLI, and Docker Desktop.

```powershell
node --version
npm --version
aws --version
sam --version
docker --version
aws configure
aws sts get-caller-identity
aws configure get region
```

Confirm the account and Region before deployment. Never commit access keys to source control.
