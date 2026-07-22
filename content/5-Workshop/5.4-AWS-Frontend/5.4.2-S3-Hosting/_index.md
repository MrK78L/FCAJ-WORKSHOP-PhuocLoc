---
title: "Set Up the S3 Frontend Bucket"
date: 2026-07-20
weight: 2
chapter: false
pre: " <b> 5.4.2. </b> "
---

# Build and upload the frontend

Create the production environment file, then run:

```powershell
npm run frontend:build
aws s3 sync frontend\dist s3://YOUR_FRONTEND_BUCKET --delete --region ap-southeast-1
```

Verify the bucket against `FrontendBucketName` before using `--delete`. Keep encryption and Block Public Access enabled and do not create a public bucket policy.
