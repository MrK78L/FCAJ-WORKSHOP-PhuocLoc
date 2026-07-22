---
title: "Blog 1"
date: 2026-07-21
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# Sử dụng AD FS và Tableau để truy vấn dữ liệu an toàn với AWS Lake Formation

## Mục tiêu

Xây dựng giải pháp cho phép người dùng doanh nghiệp đăng nhập bằng tài khoản Active Directory thông qua AD FS, truy cập Tableau và chỉ xem được dữ liệu đã được cấp quyền trong AWS Lake Formation.

## Luồng kiến trúc

```text
Người dùng
  → Active Directory
  → AD FS (SAML)
  → AWS IAM Identity Center / IAM Role
  → Tableau Server hoặc Tableau Cloud
  → Amazon Athena
  → AWS Lake Formation
  → Amazon S3 Data Lake
```

## Lợi ích bảo mật

### Đăng nhập một lần

- Người dùng đăng nhập bằng tài khoản Active Directory của doanh nghiệp.
- Không cần tạo một IAM User riêng cho từng người dùng Tableau.
- Việc xác thực tuân theo chính sách danh tính và mật khẩu của tổ chức.

### Không sử dụng access key dài hạn

Tableau không cần lưu AWS access key và secret key. Sau khi xác thực liên kết thành công, AWS cung cấp thông tin xác thực tạm thời cho phiên làm việc.

### Kiểm soát truy cập chi tiết

Lake Formation hỗ trợ kiểm soát ở cấp hàng, cột và ô dữ liệu. Ví dụ, bộ phận kế toán có thể xem thông tin lương; nhân viên chỉ xem dữ liệu nhân sự cơ bản; quản lý chỉ xem dữ liệu thuộc phòng ban của mình.

### Theo dõi và kiểm toán

AWS CloudTrail, lịch sử truy vấn Athena và log kiểm toán Lake Formation hỗ trợ xác định ai đã truy cập dữ liệu, thời điểm truy cập và câu truy vấn đã thực hiện.

## Các khả năng AWS liên quan

### AWS Lake Formation

- Phân quyền dữ liệu chi tiết.
- Bảo mật ở cấp hàng và cột.
- LF-Tags để quản lý quyền theo nhãn.
- Chia sẻ dữ liệu liên tài khoản thông qua AWS Resource Access Manager.
- Tích hợp với IAM Identity Center.

### Amazon Athena

- Athena engine version 3.
- Prepared statements và query-result reuse.
- Hỗ trợ Apache Iceberg và giao dịch ACID.
- Truy vấn SQL serverless trực tiếp trên dữ liệu S3.

### Amazon S3

- Intelligent-Tiering, Access Points, Versioning và lifecycle rules.
- S3 Object Lambda để biến đổi object khi có nhu cầu phù hợp.

### Tableau và IAM Identity Center

- SAML SSO và kết nối trực tiếp với Athena.
- Live connection, extract refresh và row-level security.
- Quản lý tập trung người dùng, group, permission set và temporary credentials.

## Tối ưu chi phí

- Lưu dữ liệu phân tích bằng Parquet thay cho CSV để giảm dung lượng và số byte Athena phải quét.
- Phân vùng dữ liệu theo ngày hoặc trường thường xuyên được sử dụng để lọc.
- Sử dụng các định dạng nén như Snappy, ZSTD hoặc GZIP.
- Thiết lập S3 lifecycle để chuyển dữ liệu cũ sang lớp lưu trữ phù hợp.
- Tái sử dụng kết quả truy vấn Athena khi dữ liệu nguồn không thay đổi.
- Chỉ cấu hình Auto Scaling khi Tableau được tự triển khai trên EC2 hoặc ECS và thực sự cần mở rộng.

## Sơ đồ kiến trúc tham khảo

![Kiến trúc truy vấn dữ liệu với AD FS, Tableau và AWS Lake Formation](/images/3-blogsposted/3.1-blog1/Blog1.jpg)

**Nguồn tham khảo:** https://awsstudygroup.com/2022/08/16/cach-su-dung-ad-fs-user-va-tableau-de-truy-van-du-lieu-mot-cach-an-toan-trong-aws-lake-formation/
