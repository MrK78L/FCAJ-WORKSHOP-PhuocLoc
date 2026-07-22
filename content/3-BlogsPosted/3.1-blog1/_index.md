---
title: "Blog 1"
date: 2026-07-21
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# Using AD FS and Tableau to Query Data Securely with AWS Lake Formation

## Objective

Build a solution that allows enterprise users to sign in with Active Directory through AD FS, access Tableau, and view only the data authorized for them in AWS Lake Formation.

## Architecture flow

```text
User
  → Active Directory
  → AD FS (SAML)
  → AWS IAM Identity Center / IAM Role
  → Tableau Server or Tableau Cloud
  → Amazon Athena
  → AWS Lake Formation
  → Amazon S3 Data Lake
```

## Security benefits

### Single Sign-On

- Users sign in once with their enterprise AD accounts.
- Separate IAM users are not required for each Tableau user.
- Authentication follows the organization's password and identity policies.

### No long-lived access keys

Tableau does not need to store an AWS access key and secret key. AWS issues temporary credentials after successful federated authentication.

### Fine-grained access control

Lake Formation supports row-level, column-level, and cell-level filtering. For example, Finance may view salary information, employees may only view basic personnel data, and managers may be restricted to their own departments.

### Auditing

AWS CloudTrail, Athena query history, and Lake Formation audit logs help identify who accessed data, when access occurred, and which queries were executed.

## Relevant AWS capabilities

### AWS Lake Formation

- Fine-grained data permissions.
- Row- and column-level security.
- LF-Tags for tag-based access control.
- Cross-account sharing through AWS Resource Access Manager.
- Integration with IAM Identity Center.

### Amazon Athena

- Athena engine version 3.
- Prepared statements and query-result reuse.
- Apache Iceberg support for ACID transactions.
- Serverless SQL queries directly against S3 data.

### Amazon S3

- Intelligent-Tiering, Access Points, Versioning, and lifecycle rules.
- Object Lambda for request-time object transformation when required.

### Tableau and IAM Identity Center

- SAML SSO and direct Athena connectivity.
- Live connections, extract refresh, and row-level security.
- Centralized users, groups, permission sets, federation, and temporary credentials.

## Cost optimization

- Store analytical data as Parquet instead of CSV to reduce storage and scanned bytes.
- Partition datasets by date or another frequently filtered field.
- Use compression formats such as Snappy, ZSTD, or GZIP.
- Configure S3 lifecycle transitions for older data.
- Reuse Athena query results when source data has not changed.
- Scale Tableau infrastructure only when self-hosting it on EC2 or ECS requires additional capacity.

## Reference Architecture

![Architecture for secure data queries with AD FS, Tableau, and AWS Lake Formation](/images/3-blogsposted/3.1-blog1/Blog1.jpg)

Reference: https://awsstudygroup.com/2022/08/16/cach-su-dung-ad-fs-user-va-tableau-de-truy-van-du-lieu-mot-cach-an-toan-trong-aws-lake-formation/
