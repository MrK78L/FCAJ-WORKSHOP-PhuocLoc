---
title: "Set Up Security, Monitoring, and Alerts"
date: 2026-07-20
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---

# Complete security and monitoring setup

- Use least-privilege Lambda IAM Roles and Cognito JWT authorization.
- Enforce the `admin` group in backend logic.
- Keep all S3 buckets encrypted and private; use short-lived presigned URLs and CloudFront OAC.
- Restrict production CORS to the CloudFront URL.
- Confirm CloudWatch log retention, the Lambda error alarm, SNS email.
- Enable WAF only when its additional cost is approved.
- Configure AWS Budget alerts before leaving resources running.
