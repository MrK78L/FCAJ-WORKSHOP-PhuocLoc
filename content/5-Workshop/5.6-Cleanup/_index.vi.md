---
title: "Kiểm tra và dọn dẹp tài nguyên AWS"
date: 2026-07-20
weight: 6
chapter: false
pre: " <b> 5.6. </b> "
---

# Kiểm tra tài nguyên đã thiết lập

Trước khi kết thúc workshop, kiểm tra CloudFormation stack, API Gateway, Lambda, DynamoDB, Cognito, S3, CloudFront, EventBridge, CloudWatch và SNS. Ghi lại stack output và kết quả kiểm thử.

# Dọn dẹp môi trường học tập

## 1. Xác nhận tài khoản

```powershell
aws sts get-caller-identity
```

## 2. Xóa stack chính

```powershell
cd backend
sam delete --stack-name cloffice-backend --region ap-southeast-1
```

## 3. Xử lý tài nguyên còn lại

- Nếu S3 bucket còn object, đối chiếu tên bucket với stack output trước khi làm trống.
- Nếu đã tạo WAF tại `us-east-1`, xóa stack WAF riêng.
- Kiểm tra CloudFront distribution, CloudWatch Log Group và SNS topic không còn ngoài dự kiến.
- Mở Billing và AWS Budget để xác nhận không còn tài nguyên phát sinh chi phí.

{{% notice warning %}}
Xóa stack và dữ liệu là thao tác không thể hoàn tác. Luôn kiểm tra AWS Account, Region, stack name và bucket name trước khi thực hiện.
{{% /notice %}}
