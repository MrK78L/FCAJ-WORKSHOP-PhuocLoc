---
title: "Blog 3"
date: 2026-07-21
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

# Session Policies trong Amazon EKS Pod Identity

Amazon EKS Pod Identity bổ sung session policies, cho phép thu hẹp quyền IAM cho từng pod mà không cần tạo một IAM Role riêng cho mọi workload. Tính năng này hỗ trợ áp dụng nguyên tắc đặc quyền tối thiểu hiệu quả hơn trong môi trường Kubernetes quy mô lớn.

## Các điểm chính

- Session policy là IAM inline policy được chỉ định khi tạo hoặc cập nhật Pod Identity association.
- Quyền hiệu lực là phần giao giữa quyền của IAM Role và session policy.
- Session policy chỉ có thể thu hẹp, không thể bổ sung quyền không tồn tại trong IAM Role.
- Nhiều workload có thể sử dụng chung một role nhưng nhận các giới hạn quyền khác nhau.
- Giải pháp giúp giảm số lượng IAM Role và hạn chế nguy cơ chạm quota tài khoản.
- Hỗ trợ mô hình cùng tài khoản và liên tài khoản thông qua role chaining.
- Có thể cấu hình association bằng AWS Console, AWS CLI hoặc AWS SDK.

## Tình huống sử dụng

Hai pod sử dụng cùng một IAM Role cơ sở. Session policy của pod thứ nhất chỉ cho phép đọc một S3 bucket cụ thể, trong khi session policy của pod thứ hai chỉ cho phép gọi một số AWS API nhất định. Mỗi workload nhận quyền hẹp hơn mặc dù sử dụng chung role.

## Lợi ích

- Thực thi đặc quyền tối thiểu tốt hơn.
- Giảm số lượng IAM Role cần tạo và quản lý.
- Dễ cô lập quyền giữa các workload.
- Quản trị danh tính hiệu quả hơn cho EKS cluster lớn.

## Hình ảnh

*Thêm hình ảnh minh họa tại đây.*

## Link tham khảo

*Bổ sung đường dẫn bài viết tại đây.*

## Hướng dẫn

*Bổ sung nội dung hướng dẫn chi tiết tại đây.*
