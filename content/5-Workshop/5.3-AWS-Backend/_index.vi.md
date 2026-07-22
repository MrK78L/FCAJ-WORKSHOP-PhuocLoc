---
title: "Thiết lập hạ tầng backend AWS"
date: 2026-07-20
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---

# Thiết lập hạ tầng backend AWS

Hạ tầng CloudOffice được khai báo trong AWS SAM template và được CloudFormation tạo đồng bộ. Stack bao gồm API Gateway, Lambda, DynamoDB, Cognito, S3, EventBridge, CloudWatch và SNS.

## Nội dung

1. [Kiểm tra template và tạo CloudFormation stack](5.3.1-sam-setup/)
2. [Kiểm tra tài nguyên và cấu hình dữ liệu ban đầu](5.3.2-aws-resources/)

{{% notice note %}}
Ở lần thiết lập đầu tiên, nên để `EnableCloudFront=false` và `EnablePointInTimeRecovery=false`. Hai tùy chọn này có thể bật sau khi backend hoạt động ổn định và ngân sách đã được xem xét.
{{% /notice %}}
