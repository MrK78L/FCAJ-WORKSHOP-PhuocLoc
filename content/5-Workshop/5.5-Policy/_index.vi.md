---
title: "Thiết lập bảo mật, giám sát và cảnh báo"
date: 2026-07-20
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---

# Hoàn thiện thiết lập bảo mật và giám sát

## IAM và Cognito

- Dùng IAM Role cho Lambda thay vì access key.
- Giới hạn quyền Lambda đến đúng DynamoDB table, S3 bucket và SNS topic cần sử dụng.
- Dùng Cognito JWT Authorizer cho API riêng tư.
- Kiểm tra group `admin` tại backend trước khi thực hiện nghiệp vụ quản trị.

## S3 và CloudFront

- Bật mã hóa và Block Public Access cho cả ba bucket.
- Upload bằng presigned URL có thời hạn ngắn.
- Dùng CloudFront OAC thay cho public website bucket.
- Có thể gắn AWS WAF vào CloudFront nếu ngân sách cho phép.

## CloudWatch, SNS

- Log Group của Lambda lưu log 14 ngày.
- CloudWatch Alarm cảnh báo khi Business Logic Lambda phát sinh lỗi.
- SNS gửi email cho người phụ trách vận hành.


## Checklist

- [ ] CORS chỉ cho phép CloudFront URL.
- [ ] SNS subscription đã xác nhận.
- [ ] S3 không public.
- [ ] User thường không truy cập được admin API.
- [ ] CloudWatch nhận log và metric.
- [ ] AWS Budget đã bật cảnh báo chi phí.
