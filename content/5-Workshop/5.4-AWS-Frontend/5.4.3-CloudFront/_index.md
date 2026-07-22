---
title: "Configure CloudFront and CORS"
date: 2026-07-20
weight: 3
chapter: false
pre: " <b> 5.4.3. </b> "
---

# Configure CloudFront

After account approval, redeploy with `EnableCloudFront=true`. Record `CloudFrontUrl` and `CloudFrontDistributionId`, wait for `Deployed`, and invalidate cached files after frontend updates.

```powershell
aws cloudfront create-invalidation --distribution-id YOUR_DISTRIBUTION_ID --paths "/*"
```

Redeploy the backend with `CorsAllowOrigin` set to the exact CloudFront URL. Verify HTTPS, React route fallback, API CORS, and private S3 access through OAC.
