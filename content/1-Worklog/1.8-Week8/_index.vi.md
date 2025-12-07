---
title: "Worklog Tuần 8"

weight: 1
chapter: false
pre: " <b> 1.8. </b> "
---


### Mục tiêu tuần 8:

* Nắm được các loại Load Balancer (ALB, NLB) và vai trò của chúng trong việc phân phối tải.
* Thực hành cấu hình Auto Scaling Group (ASG) dựa trên chỉ số CPU để đạt tính sẵn sàng cao và khả năng mở rộng đàn hồi.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Khái niệm Cân bằng Tải (ELB): Hiểu rõ Elastic Load Balancing (ELB) là dịch vụ phân phối lưu lượng truy cập mạng đến nhiều mục tiêu (Targets) trên nhiều Availability Zones để tăng tính sẵn sàng và khả năng chịu lỗi.                                                                                             | 27/10/2025   | 27/10/2025      |
| 3   | - Phân biệt các Loại Load Balancer: Phân biệt ba loại Load Balancer chính: Application Load Balancer (ALB) (lớp 7, HTTP/HTTPS), Network Load Balancer (NLB) (lớp 4, TCP/UDP), và Gateway Load Balancer (GLB).                                            | 28/10/2025   | 28/10/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Khái niệm Tự động Mở rộng (ASG): Nắm được Auto Scaling Group (ASG) là một nhóm các EC2 Instance được coi là một thực thể logic để tự động điều chỉnh số lượng Instance dựa trên nhu cầu tải. | 29/10/2025   | 29/10/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Các Chiến lược Scaling: Phân biệt các chiến lược Scaling trong ASG: Target Tracking Scaling (duy trì chỉ số ở một mức), Simple Scaling (dựa trên ngưỡng), và Step Scaling (tăng hoặc giảm theo từng bước).                  | 30/10/2025   | 30/10/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - Health Checks và Sticky Sessions: Hiểu vai trò của Health Checks trong việc kiểm tra và tự động loại bỏ các Instance bị lỗi. Nắm được khái niệm Sticky Sessions (lưu trữ phiên) và ảnh hưởng của nó đến việc phân phối tải.                                                                                         | 31/10/2025   | 31/10/2025      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 8:

* Cấu hình Application Load Balancer (ALB): Khởi tạo một ALB đa AZ và cấu hình Listener (cổng 80). Tạo Target Group trỏ đến các EC2 Instance tầng ứng dụng trong Private Subnet.

* Triển khai Auto Scaling Group (ASG): Thiết lập một Launch Template cho EC2 Instance, sau đó tạo ASG với các thông số Min/Max/Desired Capacity. Đặt ASG để chạy trên các Private Subnet.

* Cấu hình Scaling Policy Dựa trên CPU: Thiết lập Target Tracking Scaling Policy cho ASG, đặt mục tiêu duy trì mức sử dụng CPU trung bình là 60%. Kết quả: Xác nhận ASG tự động mở rộng khi tải CPU tăng và thu nhỏ khi tải giảm.

* Kiểm thử Khả năng Chịu lỗi: Mô phỏng lỗi bằng cách thủ công chấm dứt một trong các EC2 Instance đang chạy. Kết quả: ASG tự động phát hiện lỗi thông qua Health Check và khởi tạo một Instance thay thế, xác nhận kiến trúc có khả năng tự phục hồi.

* Tổng kết Ứng dụng Tính sẵn sàng: Đã hoàn thành việc thiết lập hệ thống cân bằng tải và tự động mở rộng. Kết quả: Hệ thống ứng dụng hiện đã có tính sẵn sàng cao (HA) và khả năng mở rộng đàn hồi (Elastic Scalability), có thể xử lý các đỉnh tải đột ngột và tự phục hồi sau lỗi Instance.

