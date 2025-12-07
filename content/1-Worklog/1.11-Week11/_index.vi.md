---
title: "Worklog Tuần 11"

weight: 2
chapter: false
pre: " <b> 1.11. </b> "
---


### Mục tiêu tuần 11:

* Hiểu kiến trúc Serverless, ưu điểm chi phí, và các thành phần cốt lõi: Lambda, API Gateway.
* Thực hành xây dựng một ứng dụng Serverless đầu cuối và triển khai bằng framework SAM.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Khái niệm và Ưu điểm của Serverless: Hiểu rõ kiến trúc Serverless (Phi máy chủ) là mô hình điện toán trong đó AWS quản lý máy chủ, người dùng chỉ trả tiền cho thời gian sử dụng thực tế. Nắm được ưu điểm về tối ưu chi phí và tự động mở rộng không giới hạn.                                                                                             | 17/11/2025   | 17/11/2025      |
| 3   | - Dịch vụ Tính toán Phi máy chủ (Lambda): Nắm vững AWS Lambda là dịch vụ tính toán cốt lõi của Serverless, cho phép chạy mã Function mà không cần phải cấp phát hay quản lý máy chủ. Hiểu các khái niệm Concurrency và Memory Allocation.                                            | 18/11/2025   | 18/11/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Cổng API (API Gateway): Hiểu rõ Amazon API Gateway là dịch vụ được quản lý toàn diện, cho phép tạo, duy trì, giám sát và bảo mật các API REST, HTTP và WebSocket ở quy mô lớn để làm Front-end cho các Lambda Function. | 19/11/2025   | 19/11/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Xác thực và Bảo mật Serverless (Cognito): Nắm được Amazon Cognito là dịch vụ quản lý danh tính, cung cấp tính năng đăng ký, đăng nhập và kiểm soát truy cập cho các ứng dụng web và di động Serverless.                  | 20/11/2025   | 20/11/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - Triển khai Serverless (SAM): Giới thiệu về AWS Serverless Application Model (SAM) là một khuôn khổ (framework) giúp đơn giản hóa việc triển khai các ứng dụng Serverless bằng cách sử dụng cú pháp viết tắt trên CloudFormation (từ Tuần 10).                                                                                         | 21/11/2025   | 21/11/2025      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 11:

* Triển khai Serverless Function (Lambda): Viết và triển khai một Lambda Function đơn giản (ví dụ: truy vấn dữ liệu từ DynamoDB). Cấu hình IAM Role với quyền truy cập tối thiểu cần thiết cho Function.

* Xây dựng API (API Gateway): Thiết lập API Gateway và tạo một REST API mới. Cấu hình Method (ví dụ: GET /items) để tích hợp trực tiếp với Lambda Function đã tạo.

* Quản lý Dữ liệu NoSQL (DynamoDB): Tạo một bảng DynamoDB để lưu trữ dữ liệu ứng dụng. Kiểm tra độ trễ (latency) của API sau khi tích hợp Lambda truy cập dữ liệu.

* Triển khai Toàn bộ Stack với SAM: Sử dụng AWS SAM CLI để đóng gói và triển khai toàn bộ kiến trúc Serverless (Lambda + API Gateway + DynamoDB) thông qua một file template.yaml.

* Tổng kết Ứng dụng Serverless: Đã hoàn thành việc xây dựng và triển khai một ứng dụng Serverless đầu cuối. Kết quả: Nắm được quy trình hiện đại hóa ứng dụng (Modernization) bằng cách chuyển từ kiến trúc máy chủ truyền thống sang mô hình Serverless, giúp giảm chi phí nhàn rỗi và tăng tốc độ phát triển.

* Bài học Rút ra: AWS Lambda buộc tôi phải suy nghĩ về việc chia nhỏ logic thành các đơn vị chức năng nhỏ hơn, phù hợp với nguyên tắc vi dịch vụ (Microservices). Việc quản lý Dependency trong các Function cũng là một thách thức cần được xử lý cẩn thận trong Serverless.


