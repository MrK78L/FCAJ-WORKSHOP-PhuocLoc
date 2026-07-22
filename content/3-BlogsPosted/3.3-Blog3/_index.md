---
title: "Blog 3"
date: 2026-07-21
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

# Session Policies in Amazon EKS Pod Identity

Amazon EKS Pod Identity session policies allow teams to narrow IAM permissions for individual pods without creating a separate IAM Role for every workload. This supports more consistent least-privilege enforcement in large Kubernetes environments.

## Key Points

- A session policy is an inline IAM policy specified when a Pod Identity association is created or updated.
- Effective permissions are the intersection of the IAM Role policy and the session policy.
- A session policy can reduce permissions but cannot grant permissions absent from the IAM Role.
- Multiple workloads can reuse one role while receiving different restrictions.
- The approach reduces IAM Role proliferation and the risk of reaching account quotas.
- Same-account and cross-account patterns are supported through role chaining.
- Associations can be configured through the AWS Console, AWS CLI, or AWS SDK.

## Example Use Case

Two pods use the same base IAM Role. A session policy allows the first pod to read only one S3 bucket, while another session policy allows the second pod to call only selected AWS APIs. Each workload receives narrower permissions even though the base role is shared.

## Benefits

- Better least-privilege enforcement.
- Fewer IAM Roles to create and maintain.
- Easier permission isolation among workloads.
- More scalable identity administration for large EKS clusters.

## Image

*Add an illustrative image here.*

## Reference Link

*Add the published article URL here.*

## Guide

*Add detailed instructions here.*
