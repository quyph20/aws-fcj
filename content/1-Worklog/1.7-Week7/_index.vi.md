---
title: "Worklog Tuần 7"

weight: 1
chapter: false
pre: " <b> 1.7. </b> "
---


### Mục tiêu tuần 7:

* Phân biệt các loại lưu trữ (Object/S3, Block/EBS, NoSQL/DynamoDB, Relational/RDS) và các lớp lưu trữ S3.
* Thực hành triển khai một RDS Instance Multi-AZ và thiết lập chính sách vòng đời cho S3.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Lưu trữ Đối tượng (S3): Hiểu rõ Amazon Simple Storage Service (S3) là dịch vụ lưu trữ đối tượng bền vững, có tính sẵn sàng cao. Nắm được các lớp lưu trữ S3 Storage Classes (Standard, IA, Glacier) và trường hợp sử dụng của từng loại.                                                                                             | 20/10/2025   | 20/10/2025      |
| 3   | - Lưu trữ Khối và File: Phân biệt được Amazon Elastic Block Store (EBS) (lưu trữ khối) dùng cho EC2 Instance và Amazon Elastic File System (EFS) (lưu trữ file) dùng cho các workload chia sẻ.                                            | 21/10/2025   | 21/10/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Cơ sở Dữ liệu Quan hệ (RDS): Hiểu được Amazon Relational Database Service (RDS) là dịch vụ cơ sở dữ liệu quan hệ được quản lý. Nắm được lợi ích của dịch vụ được quản lý (patching, backup, Multi-AZ) và các Engine hỗ trợ (PostgreSQL, MySQL, Aurora). | 22/10/2025   | 22/10/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Cơ sở Dữ liệu NoSQL (DynamoDB): Nắm được Amazon DynamoDB là dịch vụ cơ sở dữ liệu NoSQL dạng Key-Value có khả năng mở rộng (scalability) và hiệu suất cao. Hiểu về khái niệm Partition Key và Sort Key.                  | 23/10/2025   | 23/10/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - Chiến lược Di chuyển Dữ liệu: Hiểu các công cụ và dịch vụ được sử dụng để di chuyển lượng lớn dữ liệu hoặc mở rộng lưu trữ từ on-premises sang AWS (ví dụ: AWS Snow Family, AWS Storage Gateway).                                                                                         | 24/10/2025   | 24/10/2025      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 7:

* Quản lý Vòng đời Dữ liệu S3: Thực hành tạo một S3 Bucket, cấu hình Bucket Policy để khóa truy cập công cộng. Thiết lập Lifecycle Rule để tự động chuyển các đối tượng cũ (ví dụ: sau 30 ngày) từ S3 Standard sang S3 Standard-IA để tối ưu chi phí.

* Triển khai Hệ thống Cơ sở Dữ liệu Quan hệ: Khởi tạo một RDS Instance (sử dụng engine PostgreSQL) trong một Private Subnet (từ Tuần 6). Thiết lập Multi-AZ để đảm bảo tính sẵn sàng cao và cấu hình Security Group chỉ cho phép EC2 Instance ở tầng ứng dụng kết nối.

* Thiết lập Cơ sở Dữ liệu NoSQL Hiệu suất cao: Tạo một DynamoDB Table mới. Xác định Partition Key và Sort Key phù hợp với mô hình truy cập dữ liệu đã mô phỏng. Thực hiện các thao tác PutItem, GetItem và Query cơ bản để kiểm tra độ trễ (latency).

* Phân tích Chi phí & Hiệu suất Lưu trữ: So sánh chi phí và hiệu suất I/O giữa EBS gp3 (General Purpose SSD) và EBS io2 (Provisioned IOPS SSD). Đánh giá khi nào nên ưu tiên độ bền 11 nines của S3 so với tính nhất quán mạnh mẽ (strong consistency) của RDS.

* Tổng kết Ứng dụng Lưu trữ & Dữ liệu: Đã hoàn thành việc thiết lập các dịch vụ lưu trữ và cơ sở dữ liệu quan trọng. Kết quả: Có khả năng đưa ra quyết định kiến trúc chính xác khi lựa chọn dịch vụ lưu trữ (Đối tượng, Khối, File) và dịch vụ dữ liệu (Quan hệ, NoSQL) dựa trên yêu cầu về cấu trúc, hiệu suất và chi phí của ứng dụng.

