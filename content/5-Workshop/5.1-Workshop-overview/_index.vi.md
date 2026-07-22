---
title: "Tổng quan kiến trúc CloudOffice"
date: 2026-07-20
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

# Tổng quan workshop

CloudOffice gồm frontend React/Vite và backend serverless. Khách hàng tìm văn phòng, gửi yêu cầu thuê và đặt lịch; quản trị viên quản lý dữ liệu, hợp đồng, hình ảnh và báo cáo.

{{% notice info %}}
### Vị trí chèn hình kiến trúc workshop

`![Kiến trúc triển khai CloudOffice](/images/5-Workshop/5.1-Workshop-overview/cloudoffice-architecture.png)`
{{% /notice %}}

## Thành phần chính

- S3 và CloudFront lưu trữ, phân phối frontend.
- API Gateway nhận request từ ứng dụng.
- Cognito xác thực và phân quyền user/admin.
- Lambda xử lý nghiệp vụ, hình ảnh và cảnh báo hợp đồng.
- DynamoDB lưu dữ liệu theo single-table design.
- S3 lưu ảnh gốc, ảnh xử lý và PDF hợp đồng.
- EventBridge, CloudWatch và SNS thực hiện lịch chạy, giám sát và cảnh báo.
- AWS SAM/CloudFormation quản lý toàn bộ hạ tầng.

## Kết quả cần đạt

- Backend stack triển khai thành công.
- Frontend gọi được API AWS và đăng nhập qua Cognito.
- Các luồng văn phòng, yêu cầu thuê, lịch hẹn, hợp đồng và upload hoạt động.
- CloudWatch có log; SNS nhận được email xác nhận và cảnh báo.
