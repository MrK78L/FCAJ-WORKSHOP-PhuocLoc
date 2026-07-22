---
title: "Tạo CloudFormation stack"
date: 2026-07-20
weight: 1
chapter: false
pre: " <b> 5.3.1. </b> "
---

# Kiểm tra template và tạo stack backend

## 1. Kiểm tra mã nguồn

```powershell
cd backend
node --check functions\business-logic\app.mjs
node --check functions\image-processor\index.mjs
node --check functions\contract-expiry-notifier\index.mjs
npm test
```

## 2. Kiểm tra AWS SAM template

```powershell
sam validate `
  --template-file infra\template.yaml `
  --lint `
  --region ap-southeast-1
```

## 3. Build Lambda cho AWS

```powershell
sam build `
  --use-container `
  --config-file samconfig.toml `
  --no-cached
```

## 4. Tạo CloudFormation stack

```powershell
sam deploy `
  --config-file samconfig.toml `
  --template-file .aws-sam\build\template.yaml `
  --parameter-overrides `
    ProjectName=cloffice `
    AlertEmail=YOUR_REAL_EMAIL `
    CorsAllowOrigin="http://localhost:5173" `
    EnablePointInTimeRecovery=false `
    EnableCloudFront=false
```

Xem change set trước khi xác nhận. CloudFormation sẽ tạo tài nguyên và rollback nếu quá trình thiết lập thất bại.

## 5. Kiểm tra trạng thái

Trong AWS Console, mở **CloudFormation → Stacks → cloffice-backend**. Stack phải chuyển sang `CREATE_COMPLETE` hoặc `UPDATE_COMPLETE`.
