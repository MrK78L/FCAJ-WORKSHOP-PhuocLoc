---
title: "Kết nối frontend với AWS"
date: 2026-07-20
weight: 1
chapter: false
pre: " <b> 5.4.1. </b> "
---

# Cấu hình API Gateway và Cognito cho frontend

Tạo `frontend/.env.development.local` từ CloudFormation output:

```env
VITE_API_BASE_URL=https://YOUR_API_ID.execute-api.ap-southeast-1.amazonaws.com
VITE_COGNITO_USER_POOL_ID=YOUR_POOL_ID
VITE_COGNITO_CLIENT_ID=YOUR_CLIENT_ID
VITE_USE_DEMO_FALLBACK=false
VITE_BYPASS_ADMIN_AUTH=false
```

Chạy frontend với origin đã cho phép trong CORS:

```powershell
cd D:\THUCTAPTT\cloudoffice
npm run frontend:dev:aws
```

Mở `http://localhost:5173` và kiểm tra:

- API `/offices` tải được dữ liệu DynamoDB.
- Người dùng có thể đăng ký, xác nhận email và đăng nhập Cognito.
- Token được gửi trong header `Authorization` cho API riêng tư.
- Admin group truy cập được giao diện quản trị.

Sau khi thay đổi biến môi trường, phải khởi động lại Vite.
