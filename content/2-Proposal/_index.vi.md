---
title: "Đề xuất dự án CloudOffice"
date: 2026-07-20
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# CloudOffice – Hệ thống quản lý cho thuê văn phòng trên AWS

## 1. Tóm tắt dự án

CloudOffice là nền tảng web hỗ trợ khách hàng tìm kiếm văn phòng, xem thông tin chi tiết, gửi yêu cầu thuê và đặt lịch tham quan. Hệ thống đồng thời cung cấp khu vực quản trị để quản lý văn phòng, khách hàng, yêu cầu thuê, hợp đồng, hình ảnh và theo dõi hoạt động vận hành.

Giải pháp được xây dựng theo kiến trúc serverless trên AWS nhằm giảm công việc quản trị máy chủ, hỗ trợ mở rộng theo nhu cầu và phù hợp với phạm vi một project thực tập. Frontend sử dụng React, TypeScript và Vite; backend sử dụng API Gateway, AWS Lambda và DynamoDB; người dùng được xác thực bằng Amazon Cognito.

## 2. Vấn đề và nhu cầu

Việc quản lý thông tin văn phòng bằng bảng tính hoặc nhiều công cụ riêng lẻ dễ dẫn đến dữ liệu không đồng nhất, khó theo dõi trạng thái yêu cầu thuê và mất nhiều thời gian khi tổng hợp hợp đồng, lịch hẹn hoặc báo cáo.

CloudOffice hướng đến việc tập trung các nghiệp vụ này trên một hệ thống duy nhất:

- Khách hàng có thể tìm kiếm và xem văn phòng phù hợp.
- Người dùng đăng nhập có thể gửi yêu cầu thuê và đặt lịch xem văn phòng.
- Người dùng theo dõi hồ sơ, lịch hẹn, yêu cầu thuê và hợp đồng của mình.
- Quản trị viên quản lý văn phòng, khách hàng, yêu cầu, hợp đồng và báo cáo.
- Hình ảnh và tài liệu hợp đồng được lưu trữ an toàn trên Amazon S3.
- Hệ thống gửi cảnh báo khi Lambda gặp lỗi hoặc hợp đồng sắp hết hạn.

## 3. Mục tiêu và phạm vi

### Mục tiêu

- Xây dựng một ứng dụng web có thể triển khai thực tế trên AWS.
- Áp dụng kiến trúc serverless để hạn chế quản lý máy chủ.
- Phân quyền khách hàng và quản trị viên bằng Cognito và JWT.
- Quản lý dữ liệu bằng DynamoDB theo mô hình single-table design.
- Tự động xử lý hình ảnh và theo dõi hợp đồng sắp hết hạn.
- Ghi log, tạo cảnh báo và chuẩn bị quy trình vận hành sau triển khai.

### Phạm vi chức năng

- Trang chủ, tìm kiếm, danh sách và chi tiết văn phòng.
- Đăng ký, đăng nhập, hồ sơ người dùng và ảnh đại diện.
- Yêu cầu thuê, lịch xem văn phòng và hợp đồng cá nhân.
- Dashboard quản trị, Customer 360, sơ đồ mặt bằng và pipeline yêu cầu thuê.
- CRUD văn phòng, khách hàng, yêu cầu thuê, lịch hẹn và hợp đồng.
- Upload ảnh văn phòng, avatar và tài liệu hợp đồng bằng presigned URL.
- Báo cáo CSV, giám sát lỗi và cảnh báo hợp đồng hết hạn.

## 4. Kiến trúc giải pháp

![Kiến trúc tổng thể CloudOffice](/images/2-Proposal/cloudoffice-architecture.jpg)

### Luồng hoạt động chính

1. Khách hàng và quản trị viên truy cập frontend React được lưu trên S3 và phân phối qua CloudFront.
2. Frontend gửi request đến Amazon API Gateway HTTP API.
3. Amazon Cognito xác thực người dùng; JWT authorizer bảo vệ các API riêng tư.
4. Business Logic Lambda xử lý nghiệp vụ và đọc/ghi dữ liệu trong DynamoDB.
5. Ảnh hoặc tài liệu được upload trực tiếp lên S3 thông qua presigned URL.
6. Khi có ảnh mới, Image Processor Lambda tối ưu ảnh và lưu kết quả sang processed bucket.
7. EventBridge kích hoạt Lambda kiểm tra hợp đồng mỗi ngày; SNS gửi email cảnh báo.
8. CloudWatch lưu log, theo dõi lỗi Lambda và kích hoạt SNS Alarm khi cần.

### Dịch vụ AWS sử dụng

| Dịch vụ | Vai trò trong CloudOffice |
| --- | --- |
| Amazon S3 | Lưu frontend, ảnh gốc, ảnh đã xử lý và tài liệu hợp đồng. |
| Amazon CloudFront | Phân phối frontend qua HTTPS và cache nội dung tĩnh. |
| Amazon API Gateway | Cung cấp HTTP API cho frontend. |
| AWS Lambda | Xử lý nghiệp vụ, tối ưu hình ảnh và kiểm tra hợp đồng hết hạn. |
| Amazon DynamoDB | Lưu dữ liệu văn phòng, khách hàng, yêu cầu thuê, lịch hẹn và hợp đồng. |
| Amazon Cognito | Đăng ký, đăng nhập, phát hành token và phân nhóm admin. |
| Amazon EventBridge | Chạy lịch kiểm tra hợp đồng hằng ngày. |
| Amazon CloudWatch | Lưu log, metric và cảnh báo lỗi Lambda. |
| Amazon SNS | Gửi email cảnh báo vận hành và hợp đồng sắp hết hạn. |
| AWS SAM/CloudFormation | Khai báo, triển khai và cập nhật hạ tầng bằng mã. |
| AWS WAF | Lớp bảo vệ tùy chọn cho CloudFront khi triển khai production. |

## 5. Thiết kế kỹ thuật

### Frontend

- React 18, TypeScript và Vite.
- Gọi API thông qua biến môi trường `VITE_API_BASE_URL`.
- Tích hợp Cognito để đăng ký, đăng nhập và lưu phiên người dùng.
- Giao diện public và admin được tách theo vai trò.

### Backend

- Node.js 22.x chạy trên AWS Lambda.
- Business Logic Lambda cung cấp API cho văn phòng, khách hàng, yêu cầu thuê, lịch hẹn, hợp đồng và báo cáo.
- Image Processor Lambda được kích hoạt khi S3 nhận ảnh mới.
- Contract Expiry Notifier Lambda chạy theo lịch và gửi thông báo qua SNS.

### Dữ liệu và bảo mật

- DynamoDB dùng khóa `PK`, `SK` và ba Global Secondary Index để phục vụ nhiều mẫu truy vấn.
- S3 bật mã hóa phía máy chủ và chặn public access.
- API riêng tư yêu cầu JWT từ Cognito; chức năng admin tiếp tục kiểm tra group `admin` trong backend.
- IAM Role của từng Lambda chỉ được cấp quyền cần thiết đến DynamoDB, S3 hoặc SNS.

## 6. Kế hoạch triển khai

| Giai đoạn | Nội dung |
| --- | --- |
| Phân tích | Xác định người dùng, chức năng, dữ liệu và yêu cầu vận hành. |
| Thiết kế | Vẽ kiến trúc AWS, thiết kế API và mô hình DynamoDB. |
| Phát triển | Xây dựng frontend, Lambda và template AWS SAM. |
| Triển khai thử nghiệm | Deploy backend, seed dữ liệu, cấu hình Cognito và chạy frontend local với API AWS. |
| Triển khai frontend | Build React, upload lên S3 và bật CloudFront khi tài khoản được phê duyệt. |
| Kiểm thử và hoàn thiện | Kiểm tra nghiệp vụ, quyền truy cập, upload, cảnh báo, log và sửa lỗi. |

## 7. Chi phí dự kiến

Project ưu tiên các dịch vụ tính phí theo mức sử dụng như Lambda, API Gateway và DynamoDB On-Demand. Trong môi trường học tập có ít người dùng, phần lớn lưu lượng ở mức thấp; tuy nhiên chi phí thực tế còn phụ thuộc số request, dung lượng S3, data transfer, CloudFront và thời gian lưu log.

Trước khi triển khai cần tạo ước tính bằng AWS Pricing Calculator và thiết lập AWS Budget. AWS WAF là thành phần tùy chọn vì có chi phí cố định ngoài phí request.

## 8. Rủi ro và phương án xử lý

| Rủi ro | Phương án xử lý |
| --- | --- |
| Cấu hình CORS sai | Chỉ cho phép đúng URL frontend và kiểm tra preflight request. |
| Phân quyền admin sai | Dùng Cognito group, JWT và kiểm tra quyền tại Lambda. |
| Lộ thông tin xác thực | Không lưu access key trong source; dùng IAM Role và biến môi trường. |
| S3 bị public ngoài ý muốn | Bật Block Public Access, dùng presigned URL và CloudFront OAC. |
| Dữ liệu bị xóa nhầm | Cân nhắc bật DynamoDB Point-in-Time Recovery ở production. |
| Lỗi xử lý ảnh | Theo dõi CloudWatch Logs, giới hạn kích thước và kiểm tra định dạng file. |
| Vượt ngân sách | Dùng AWS Budgets, log retention và chỉ bật CloudFront/WAF khi cần. |

## 9. Kết quả kỳ vọng

- Hoàn thiện hệ thống quản lý cho thuê văn phòng có giao diện khách hàng và quản trị.
- Triển khai được một kiến trúc serverless trên AWS bằng AWS SAM.
- Bảo vệ tài khoản và API bằng Cognito, JWT và IAM Role.
- Quản lý dữ liệu, ảnh và hợp đồng trên DynamoDB và S3.
- Theo dõi hệ thống qua CloudWatch và nhận cảnh báo bằng SNS.
- Có tài liệu triển khai, kiểm thử, xử lý lỗi và dọn dẹp tài nguyên.
