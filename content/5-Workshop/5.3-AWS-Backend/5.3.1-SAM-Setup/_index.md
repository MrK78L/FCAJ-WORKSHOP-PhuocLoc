---
title: "Create the CloudFormation Stack"
date: 2026-07-20
weight: 1
chapter: false
pre: " <b> 5.3.1. </b> "
---

# Validate and create the backend stack

```powershell
cd D:\THUCTAPTT\cloudoffice\backend
npm test
sam validate --template-file infra\template.yaml --lint --region ap-southeast-1
sam build --use-container --config-file samconfig.toml --no-cached
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

Review the change set before confirmation. In the CloudFormation console, verify that `cloffice-backend` reaches `CREATE_COMPLETE` or `UPDATE_COMPLETE`.
