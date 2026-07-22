---
title: "Event 1"
date: 2026-05-23
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---

# Bài thu hoạch “FCAJ Community Day – Conference Call”

## Mục đích của sự kiện

Sự kiện tạo không gian để thành viên FCAJ, mentor và những người làm việc trong lĩnh vực công nghệ chia sẻ kiến thức thực tế về trí tuệ nhân tạo, dịch vụ AWS, kiến trúc cloud, bảo mật và quá trình xây dựng sản phẩm. Người tham dự cũng có cơ hội trao đổi và học hỏi từ các dự án cùng kinh nghiệm thực tế của diễn giả.

## Diễn giả và chủ đề

- **Anh Tịnh** – *Build a Second Brain*
- **Hải Anh** – *Friendly AI Assistant with Amazon QuickSight*
- **Thịnh** – *From Edge to Origin: CloudFront as Your Foundation*
- **Team VIB** – *36 Hours with LotusHacks – Building UTMorpho from Idea to Reality*
- **Đào Đức** – *Deep-Dive Talk: How Does an LLM Actually Work?*
- **Cát Vy** – *Enterprise-Grade Multi-Agent System*

## Nội dung nổi bật

### Tư duy ứng dụng AI

Việc sử dụng mô hình ngôn ngữ lớn đòi hỏi ngữ cảnh rõ ràng và chuyên biệt thay vì cung cấp quá nhiều dữ liệu không liên quan. Người phát triển cần tránh sao chép mã nguồn hoặc plugin từ Internet mà không hiểu mục đích và kiến trúc của chúng.

### Bản chất xác suất của LLM

Mô hình ngôn ngữ lớn có tính bất định. Ngay cả khi đặt `temperature` bằng 0, kết quả vẫn có thể khác nhau do quá trình xử lý GPU hoặc cơ chế tối ưu của nhà cung cấp API.

### Kiến trúc Multi-Agent cho doanh nghiệp

Một agent đơn lẻ khó xử lý hiệu quả mọi tác vụ phức tạp. Hệ thống doanh nghiệp có thể phân chia trách nhiệm cho các agent chuyên biệt về phân tích, nghiên cứu, điều phối và quản trị rủi ro. Vai trò cùng cơ chế phối hợp cần được xác định rõ ràng.

### Hạ tầng và bảo mật với AWS

Amazon CloudFront không chỉ tăng tốc phân phối nội dung mà còn giúp giảm mức độ lộ trực tiếp của origin, tiếp nhận lưu lượng phân tán và tích hợp với các cơ chế bảo mật AWS. Kiến trúc và chi phí cần được đánh giá trước khi chọn phương án triển khai.

### Thực hành AI qua Hackathon

Team VIB giới thiệu ứng dụng sử dụng AI để tạo và chỉnh sửa giao diện HTML/CSS. Những bài học quan trọng gồm kiểm soát mức sử dụng token, giới hạn tính năng để tập trung vào giá trị cốt lõi và tránh để AI sinh mã quá phức tạp.

## Những gì học được

### Ngữ cảnh là yếu tố quan trọng

AI hoạt động hiệu quả hơn khi được cung cấp ngữ cảnh cụ thể, vai trò rõ ràng, giới hạn phù hợp và mục tiêu chính xác.

### Không tin tưởng tuyệt đối vào output của AI

Dữ liệu và mã nguồn do AI sinh ra cần được hệ thống và con người kiểm tra. Ứng dụng nên có validation, fallback và exception handling để xử lý output sai hoặc không đúng định dạng.

### Bảo mật cần được thiết kế từ đầu

Hệ thống AI thực tế phải xem xét rò rỉ dữ liệu, prompt injection, kiểm soát truy cập và audit trail. Bảo mật cần là một phần của kiến trúc thay vì được bổ sung sau khi phát triển.

### Sản phẩm thực tế khác với demo

Một ứng dụng hoàn chỉnh cần kiến trúc rõ ràng, trách nhiệm được phân chia hợp lý, bảo mật phù hợp và tập trung vào giá trị cốt lõi. Việc thêm quá nhiều công nghệ hoặc tính năng có thể làm hệ thống khó bảo trì.

## Ứng dụng vào công việc

### Tối ưu quá trình phát triển backend

Khi xây dựng backend phức tạp hoặc tích hợp AI, controller và business logic cần xử lý lỗi an toàn. Các định dạng do AI sinh ra, chẳng hạn JSON, phải được kiểm tra kỹ để tránh làm hệ thống gặp lỗi.

### Thiết kế và triển khai UI/UX

AI có thể hỗ trợ phác thảo và tinh chỉnh giao diện trên Figma hoặc bằng HTML/CSS, nhưng cần có quy tắc thiết kế và giới hạn rõ ràng. Điều này giúp output nhất quán, gọn gàng và tránh sinh mã không cần thiết.

### Quản trị hạ tầng cloud

CloudFront có thể được cân nhắc để phân phối nội dung tĩnh và hình ảnh, đồng thời giảm mức độ lộ trực tiếp của origin. Bảo mật, giám sát, khả năng mở rộng và chi phí nên được xem xét ngay từ giai đoạn thiết kế kiến trúc.

## Trải nghiệm tại sự kiện

Tham dự sự kiện là một trải nghiệm mới mẻ và hữu ích, giúp em có thêm góc nhìn thực tế về AI, dịch vụ AWS và cách thiết kế dự án cho môi trường thực tế.

### Học hỏi từ các diễn giả

Các diễn giả chia sẻ kiến thức bằng cách gần gũi và sinh động. Nội dung bao gồm AI, CloudFront, thiết kế hệ thống an toàn và những bài học rút ra từ quá trình phát triển dự án thực tế.

### Trải nghiệm kỹ thuật thực tế

Dự án của Team VIB để lại nhiều ấn tượng. Trong 36 giờ, nhóm đã xây dựng ứng dụng có giao diện kéo thả, quy trình Multi-Agent và nhiều tính năng hoạt động được.

### Bài học rút ra

Phát triển sản phẩm thực tế khác nhiều so với làm demo. Ngoài việc viết mã, nhóm cần quan tâm đến bảo mật, kiến trúc rõ ràng, độ tin cậy khi vận hành và giá trị cốt lõi. Công nghệ và tính năng cần được lựa chọn có mục đích.

### Hình ảnh sự kiện

*Thêm hình ảnh tham gia sự kiện tại đây.*

> Nhìn chung, sự kiện cung cấp nhiều kiến thức kỹ thuật hữu ích và giúp em cải thiện tư duy về thiết kế hệ thống, bảo mật và phát triển sản phẩm thực tế.
