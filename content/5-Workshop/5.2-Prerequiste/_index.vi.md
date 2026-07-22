---
title: "Thiết lập tài khoản, IAM và công cụ AWS"
date: 2026-07-20
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---

# Thiết lập tài khoản và môi trường AWS

## 1. Chọn Region

Đăng nhập AWS Management Console và chọn Region **Asia Pacific (Singapore) – `ap-southeast-1`**. Sử dụng thống nhất Region này cho CloudFormation, Lambda, DynamoDB, Cognito, S3 và CloudWatch.

## 2. Thiết lập bảo mật tài khoản

- Bật MFA cho root user và không sử dụng root user cho công việc hằng ngày.
- Tạo IAM user hoặc IAM Identity Center user dành cho việc triển khai.
- Chỉ cấp quyền cần thiết cho CloudFormation, Lambda, API Gateway, DynamoDB, S3, Cognito, IAM, CloudWatch, EventBridge và SNS.
- Không lưu access key trong source code hoặc đưa lên Git.

## 3. Thiết lập quản lý chi phí

- Mở **Billing and Cost Management** để kiểm tra Free Tier và hóa đơn.
- Tạo AWS Budget với ngưỡng phù hợp cho môi trường học tập.
- Cấu hình email nhận cảnh báo khi chi phí thực tế hoặc dự báo vượt ngưỡng.

## 4. Cài đặt công cụ

Cài Node.js 22.x, npm, AWS CLI v2, AWS SAM CLI và Docker Desktop, sau đó kiểm tra:

```powershell
node --version
npm --version
aws --version
sam --version
docker --version
```

## 5. Cấu hình AWS CLI

```powershell
aws configure
aws sts get-caller-identity
aws configure get region
```

Kết quả `get-caller-identity` phải đúng AWS Account dự kiến và Region mặc định nên là `ap-southeast-1`.

## 6. Chuẩn bị mã nguồn

```powershell
npm install
npm run frontend:install
npm run backend:install
```

{{% notice warning %}}
Không tiếp tục triển khai nếu AWS Account hoặc Region chưa đúng. Docker phải chạy trước khi build Lambda có thư viện `sharp`.
{{% /notice %}}
