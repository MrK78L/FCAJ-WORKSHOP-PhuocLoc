---
title: "Connect the Frontend to AWS"
date: 2026-07-20
weight: 1
chapter: false
pre: " <b> 5.4.1. </b> "
---

# Configure API Gateway and Cognito

Create `frontend/.env.development.local` from stack outputs:

```env
VITE_API_BASE_URL=https://YOUR_API_ID.execute-api.ap-southeast-1.amazonaws.com
VITE_COGNITO_USER_POOL_ID=YOUR_POOL_ID
VITE_COGNITO_CLIENT_ID=YOUR_CLIENT_ID
VITE_USE_DEMO_FALLBACK=false
VITE_BYPASS_ADMIN_AUTH=false
```

Run `npm run frontend:dev:aws`, open `http://localhost:5173`, and verify API data, Cognito sign-up/sign-in, JWT-protected calls, and admin-group access.
