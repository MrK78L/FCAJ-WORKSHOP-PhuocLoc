---
title: "Kiểm tra và cấu hình tài nguyên backend"
date: 2026-07-20
weight: 2
chapter: false
pre: " <b> 5.3.2. </b> "
---

# Kiểm tra các dịch vụ AWS sau khi tạo stack

## 1. Lấy stack output

```powershell
aws cloudformation describe-stacks `
  --stack-name cloffice-backend `
  --region ap-southeast-1 `
  --query "Stacks[0].Outputs"
```

Lưu `ApiUrl`, `CognitoUserPoolId`, `CognitoClientId`, `FrontendBucketName`, `StorageBucketName` và `ProcessedBucketName`.

## 2. Kiểm tra từng dịch vụ

- **API Gateway:** HTTP API `cloffice-api` đã có các route CloudOffice.
- **Lambda:** business logic, image processor và contract expiry notifier ở trạng thái hoạt động.
- **DynamoDB:** bảng `cloffice-offices-table` dùng chế độ On-Demand và có GSI1–GSI3.
- **Cognito:** User Pool, App Client và group `admin` đã được tạo.
- **S3:** frontend, storage và processed bucket đều bật mã hóa và Block Public Access.
- **CloudWatch/SNS:** log group, alarm và topic cảnh báo đã tồn tại.

## 3. Xác nhận SNS

Mở email đã khai báo trong `AlertEmail` và chọn **Confirm subscription**.

## 4. Seed dữ liệu DynamoDB

```powershell
cd D:\THUCTAPTT\cloudoffice\backend
npm run seed -- --table cloffice-offices-table --region ap-southeast-1
```

## 5. Tạo admin Cognito

Dùng AWS CLI hoặc Cognito Console để tạo người dùng, đặt mật khẩu vĩnh viễn và thêm vào group `admin`. Sau đó gọi `ApiUrl/offices` để xác nhận API public trả về dữ liệu.
