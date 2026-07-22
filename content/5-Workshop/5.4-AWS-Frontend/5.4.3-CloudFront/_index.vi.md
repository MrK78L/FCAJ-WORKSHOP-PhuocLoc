---
title: "Thiết lập CloudFront và CORS"
date: 2026-07-20
weight: 3
chapter: false
pre: " <b> 5.4.3. </b> "
---

# Thiết lập phân phối frontend bằng CloudFront

## 1. Bật CloudFront

Sau khi tài khoản được AWS phê duyệt, build và deploy lại stack với `EnableCloudFront=true`. CloudFormation sẽ tạo distribution, Origin Access Control và bucket policy cho frontend.

## 2. Lấy thông tin distribution

Lấy `CloudFrontUrl` và `CloudFrontDistributionId` từ stack output. Chờ distribution chuyển sang trạng thái `Deployed`.

## 3. Xóa cache sau khi cập nhật frontend

```powershell
aws cloudfront create-invalidation `
  --distribution-id YOUR_DISTRIBUTION_ID `
  --paths "/*"
```

## 4. Siết CORS

Deploy lại backend với `CorsAllowOrigin` bằng đúng `https://...cloudfront.net`, không dùng `*` trong production.

## 5. Kiểm tra

- Website tải qua HTTPS.
- Refresh trực tiếp các route React không trả 403/404.
- API request không bị lỗi CORS.
- S3 bucket vẫn private và chỉ CloudFront đọc được object.
