---
title: "Thiết lập frontend bucket S3"
date: 2026-07-20
weight: 2
chapter: false
pre: " <b> 5.4.2. </b> "
---

# Build và đưa frontend lên Amazon S3

## 1. Cấu hình production

Tạo `frontend/.env.production.local` với API URL và Cognito ID hiện tại.

## 2. Build ứng dụng

```powershell
npm run frontend:build
```

## 3. Upload lên S3

Đối chiếu bucket với output `FrontendBucketName`, sau đó chạy:

```powershell
aws s3 sync frontend\dist `
  s3://YOUR_FRONTEND_BUCKET `
  --delete `
  --region ap-southeast-1
```

## 4. Kiểm tra cấu hình bucket

- Block Public Access đang bật.
- Server-side encryption dùng AES-256.
- Không tạo public bucket policy.
- CloudFront Origin Access Control sẽ là thành phần đọc object production.

{{% notice warning %}}
`--delete` xóa object không còn trong thư mục build. Chỉ chạy sau khi đã xác nhận chính xác frontend bucket.
{{% /notice %}}
