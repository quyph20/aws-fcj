---
title: "Worklog Tuần 6"

weight: 1
chapter: false
pre: " <b> 1.6. </b> "
---



### Mục tiêu tuần 6:

* Mục tiêu là hiểu và tự thiết lập một Virtual Private Cloud (VPC) phân lớp.
* Thực hành tạo Public/Private Subnet, cấu hình Internet Gateway và NAT Gateway cho mạng an toàn.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Khái niệm VPC: Hiểu rõ Amazon Virtual Private Cloud (VPC) là nền tảng mạng cốt lõi của AWS, cho phép tạo ra một mạng ảo biệt lập, tùy chỉnh (logical isolation) trong đám mây công cộng.                                                                                             | 13/10/2025   | 13/10/2025      |
| 3   | - Phân vùng Subnets: Nắm được khái niệm Subnets và vai trò phân vùng mạng. Phân biệt Public Subnet (cho tài nguyên công khai) và Private Subnet (cho tài nguyên nội bộ, bảo mật).                                            | 14/10/2025   | 14/10/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Định tuyến và Internet Gateway: Hiểu vai trò của Internet Gateway (IGW). Nắm được cách Route Table (Bảng định tuyến) điều hướng lưu lượng truy cập giữa các Subnets và IGW. | 15/10/2025   | 15/10/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Bảo mật Cấp độ Mạng (Security Groups & NACLs): Phân biệt giữa Security Groups (SG) (tường lửa cấp độ Instance) và Network Access Control Lists (NACLs) (tường lửa cấp độ Subnet).                  | 16/10/2025   | 16/10/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - N.A.T Gateway: Hiểu vai trò của NAT Gateway trong việc cho phép các Instance trong Private Subnet truy cập Internet mà không bị lộ địa chỉ IP riêng ra ngoài.                                                                                         | 17/10/2025   | 17/10/2025      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 6:
* Thiết lập VPC và Subnets Đa AZ: Khởi tạo một VPC mới với CIDR block tùy chỉnh. Tạo các Public và Private Subnets trải dài qua ít nhất hai Availability Zones để đảm bảo tính sẵn sàng cao (HA).

* Cấu hình Định tuyến ra Internet: Cấu hình Internet Gateway và Route Table chính (Main Route Table) để đảm bảo lưu lượng từ Public Subnet được định tuyến chính xác ra Internet.

* Thiết lập NAT cho Mạng Nội bộ: Khởi tạo NAT Gateway và đặt nó trong Public Subnet. Tạo Route Table riêng cho Private Subnet, định tuyến lưu lượng ra ngoài qua NAT Gateway thay vì IGW.

* Triển khai Lớp Bảo mật Kép: Thiết lập Network ACLs để kiểm soát lưu lượng đi vào/ra cấp Subnet và cấu hình Security Group chặt chẽ chỉ cho phép các port cần thiết cho các Instance EC2 trong Private Subnet.

* Tổng kết Ứng dụng Mạng và Kiểm thử: Khởi chạy các Instance kiểm thử ở cả hai Subnets và xác minh: Instance công cộng có thể truy cập từ Internet; Instance riêng tư có thể ping ra Internet (qua NAT) nhưng không thể truy cập trực tiếp từ ngoài. Kết quả: Đã tạo ra một kiến trúc mạng an toàn, phân lớp.


