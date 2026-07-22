---
title: "Blog 2"
date: 2026-07-21
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

# Xây dựng kiến trúc dữ liệu đa Region đáng tin cậy với AWS Glue và AWS Lake Formation

## 1. Mục tiêu

Xây dựng Data Lake đa Region trên AWS nhằm:

- Đảm bảo tính sẵn sàng cao và hỗ trợ khôi phục sau thảm họa.
- Quản trị và chia sẻ dữ liệu tập trung.
- Phân quyền chi tiết đến bảng, cột hoặc hàng dữ liệu.
- Phục vụ phân tích theo lô và gần thời gian thực.
- Mở rộng linh hoạt và kiểm soát chi phí lưu trữ, xử lý.

## 2. Luồng kiến trúc

```text
Nguồn dữ liệu ERP / CRM / IoT
  → AWS Glue Jobs
  → Amazon S3 Data Lake tại Region chính
  → Glue Data Catalog và AWS Lake Formation
  → Amazon Athena
  → Amazon QuickSight / người dùng nghiệp vụ

Amazon S3 Cross-Region Replication
  → S3 bucket tại Region dự phòng
  → Glue Data Catalog và quyền Lake Formation được đồng bộ
  → Athena / Amazon EMR / Amazon Redshift
```

## 3. Các khả năng quan trọng

### AWS Glue

- **Glue Data Quality:** phát hiện giá trị thiếu hoặc bất thường và tạo báo cáo chất lượng dữ liệu.
- **Glue Flex Jobs:** giảm chi phí cho các tác vụ ETL không cần hoàn thành ngay.
- **Glue Studio:** thiết kế ETL trực quan và tạo mã PySpark.
- **Glue runtime mới:** cải thiện hiệu năng Spark và hỗ trợ Iceberg, Hudi, Delta Lake.

### AWS Lake Formation

- **LF-Tags:** phân quyền dựa trên thuộc tính như phòng ban hoặc độ nhạy cảm.
- **Row-level security:** giới hạn bản ghi mà từng người dùng được xem.
- **Column-level security:** bảo vệ các trường dữ liệu nhạy cảm.
- **Cross-account sharing:** chia sẻ dữ liệu có kiểm soát mà không cần sao chép.
- **Hybrid access mode:** hỗ trợ quá trình chuyển đổi từ cơ chế phân quyền chỉ dùng IAM.

## 4. Lợi ích của kiến trúc

| Tiêu chí | Giải pháp |
| --- | --- |
| Tính sẵn sàng cao | Sao chép dữ liệu S3 sang Region dự phòng. |
| Khôi phục sau thảm họa | Chuẩn bị catalog, quyền và dịch vụ phân tích tại Region thứ hai. |
| Quản trị dữ liệu | Lake Formation quản lý quyền tập trung và chi tiết. |
| Khả năng mở rộng | S3, Glue và Athena là các dịch vụ có khả năng mở rộng theo nhu cầu. |
| Bảo mật | Kết hợp AWS KMS, IAM, Lake Formation và CloudTrail. |
| Hiệu năng | Sử dụng Parquet, partition, compression và Athena engine mới. |
| Tối ưu chi phí | Áp dụng Glue Flex, S3 Lifecycle và query-result reuse. |

## 5. Kết luận

AWS Glue và Lake Formation cung cấp nền tảng xử lý, catalog và quản trị cho một Data Lake hiện đại. Khi kết hợp S3 Cross-Region Replication, Glue Data Quality, LF-Tags, Apache Iceberg, Parquet, partition và lifecycle policies, kiến trúc có thể hỗ trợ phân tích dữ liệu ổn định, bảo mật và kiểm soát chi phí tốt hơn.

## Sơ đồ kiến trúc tham khảo

![Sao chép Data Lake giữa Region nguồn và Region đích](/images/3-blogsposted/Blog2.1.jpg)

![Sao chép Glue Data Catalog và quyền Lake Formation giữa các Region](/images/3-blogsposted/Blog2.2.jpg)

![Đồng bộ thay đổi Glue và Lake Formation bằng kiến trúc hướng sự kiện](/images/3-blogsposted/Blog2.3.jpg)

**Nguồn tham khảo:** https://awsstudygroup.com/2023/05/06/xay-dung-kien-truc-du-lieu-hien-dai-da-region-va-dang-tin-cay-bang-cach-su-dung-aws-glue-va-aws-lake-formation/
