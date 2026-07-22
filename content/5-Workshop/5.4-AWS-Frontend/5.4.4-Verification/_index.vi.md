---
title: "Kiểm tra hệ thống trên AWS"
date: 2026-07-20
weight: 4
chapter: false
pre: " <b> 5.4.4. </b> "
---

# Kiểm tra sau khi thiết lập AWS

## Xác thực và phân quyền

- Đăng ký, xác nhận email và đăng nhập bằng Cognito.
- Kiểm tra API riêng tư từ chối request thiếu token.
- Kiểm tra user thường không sử dụng được chức năng admin.

## Dữ liệu và nghiệp vụ

- Xem danh sách và chi tiết văn phòng từ DynamoDB.
- Tạo yêu cầu thuê, lịch hẹn và kiểm tra dữ liệu được lưu đúng.
- Upload ảnh hoặc tài liệu bằng presigned URL.
- Xác nhận Image Processor Lambda tạo ảnh trong processed bucket.

## Vận hành

- Kiểm tra log của từng Lambda trong CloudWatch.
- Xem metric lỗi và trạng thái CloudWatch Alarm.
- Xác nhận SNS đã sẵn sàng gửi email.
- Kiểm tra lịch EventBridge của Contract Expiry Notifier.

Nếu có lỗi, xem API Gateway CORS, Lambda Logs, IAM Role và biến môi trường frontend trước khi triển khai lại.
