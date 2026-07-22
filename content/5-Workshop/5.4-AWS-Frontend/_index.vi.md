---
title: "Thiết lập frontend trên AWS"
date: 2026-07-20
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---

# Thiết lập frontend trên Amazon S3 và CloudFront

Backend stack đã tạo một S3 bucket riêng cho frontend. Trong giai đoạn đầu, frontend chạy local để kiểm tra API và Cognito; sau đó được build, upload lên S3 và phân phối riêng tư qua CloudFront.

## Nội dung

1. [Kết nối frontend với API và Cognito](5.4.1-frontend-config/)
2. [Build và upload frontend lên S3](5.4.2-s3-hosting/)
3. [Thiết lập CloudFront và CORS](5.4.3-cloudfront/)
4. [Kiểm tra hệ thống trên AWS](5.4.4-verification/)
