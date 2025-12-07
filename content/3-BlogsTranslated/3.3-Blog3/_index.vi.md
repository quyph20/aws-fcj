---
title: "Blog 3"
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---

# Xây dựng mạng chăm sóc sức khỏe Resilient với AWS Cloud WAN và SD-WAN

Trong lĩnh vực Bán lẻ và Chăm sóc Sức khỏe, yêu cầu kết nối mạng ổn định và độ sẵn sàng cao là vô cùng quan trọng để phục vụ khách hàng và duy trì hoạt động liên tục. Các tổ chức trong lĩnh vực này thường phải kết nối mạng doanh nghiệp với cửa hàng, trung tâm liên lạc, trung tâm phân phối—hoặc trong trường hợp của Best Buy Health: **các Trung tâm Chăm sóc Khách hàng (Care Centers)**.

Best Buy Health cung cấp các giải pháp chăm sóc sức khỏe tại nhà, thiết bị công nghệ thân thiện với người lớn tuổi, cùng đội ngũ nhân viên hỗ trợ chuyên nghiệp cho các nhu cầu kỹ thuật, khẩn cấp và xã hội. Bài viết này mô tả giải pháp kỹ thuật mà Best Buy Health sử dụng để tích hợp **Fortinet FortiGate SD-WAN** vào **Amazon VPC** thông qua **AWS Cloud WAN**. Cách tiếp cận “transitive” này cho phép Best Buy Health **hợp nhất thiết kế mạng và mô hình vận hành** giữa các chi nhánh và hệ thống chạy trên AWS.

---

## Tổng quan kiến trúc

Best Buy Health sử dụng mô hình **hub-and-spoke** để kết nối nhiều Care Center với các workload chạy trên AWS. Kiến trúc của họ bao gồm:

- **AWS Cloud WAN** làm lớp điều phối mạng toàn cầu  
- **SD-WAN (Fortinet FortiGate)** để kết nối bảo mật và tối ưu hóa từ các chi nhánh  
- **Transit Gateway (TGW)** làm trung tâm kết nối trong từng AWS Region  
- **Các đường hầm Site-to-Site VPN** giữa thiết bị SD-WAN và AWS  
- **Các thiết bị dự phòng** để tăng độ sẵn sàng  

Thiết kế này giúp Best Buy Health:

- Đơn giản hóa vận hành  
- Giảm nhu cầu cấu hình thủ công  
- Cải thiện hiệu năng kết nối giữa các Care Center và workload AWS  

---

## Các thành phần chính của kiến trúc

### **1. Mạng lõi AWS Cloud WAN**

Đây là mạng lõi toàn cầu giúp quản lý:

- Định tuyến  
- Kết nối liên vùng  
- Chính sách mạng  

Cloud WAN kết nối các Region, TGW và SD-WAN Appliances thông qua Cloud WAN Attachments.

---

### **2. SD-WAN Management VPC**

VPC này chứa hai thiết bị FortiGate hoạt động theo mô hình dự phòng:

- Một thiết bị dùng cho **quản lý**  
- Một thiết bị dùng cho **VPN và SD-WAN termination**

VPC này hỗ trợ:

- Thiết lập đường hầm IPSec  
- Routing động (BGP over IPSec)  
- Chính sách egress chung  

---

### **3. Transit Gateway (TGW)**

Transit Gateway đóng vai trò **trung tâm kết nối trong Region**, liên kết:

- SD-WAN VPC  
- Application VPC  
- Shared Services VPC  
- Các VPC khác trong cùng Region  

---

### **4. Các Care Center (Chi nhánh)**

Mỗi Care Center sử dụng thiết bị **FortiGate SD-WAN** đặt tại chi nhánh.

Thiết bị này thiết lập:

- Hai đường hầm VPN dự phòng đến AWS  
- Tự động định tuyến và chuyển hướng khi có sự cố  
- Kiểm soát lưu lượng thông minh (Application Aware Routing)  

---

## Luồng xử lý mạng

1. Thiết bị SD-WAN tại Care Center thiết lập **hai đường hầm IPSec** đến FortiGate trong AWS  
2. FortiGate kết nối vào **Transit Gateway**  
3. Transit Gateway điều phối lưu lượng đến các Application VPC  
4. Cloud WAN quản lý và điều phối định tuyến giữa các Region  

Tất cả định tuyến được quản lý **tập trung**, hạn chế tối đa cấu hình thủ công ở chi nhánh.

---

## Lý do Best Buy Health chọn mô hình này

###  **1. Đơn giản hóa vận hành**
Cloud WAN giúp:

- Trung tâm hóa cấu hình mạng  
- Dễ dàng áp dụng chính sách toàn hệ thống  
- Giảm xử lý thủ công tại chi nhánh  

---

###  **2. Tăng khả năng phục hồi (Resilience)**

Nhiều lớp dự phòng:

- SD-WAN Appliances  
- IPSec tunnels  
- Transit Gateway  
- Kết nối liên vùng  

Cho phép hệ thống duy trì hoạt động ngay cả khi một thành phần gặp sự cố.

---

###  **3. Tăng cường bảo mật**
Fortinet SD-WAN cung cấp:

- Kiểm soát truy cập  
- Chính sách tường lửa thống nhất  
- Mã hóa end-to-end  

---

### **4. Mở rộng linh hoạt**
Dễ dàng thêm Care Center mới chỉ bằng:

- Plug-and-play thiết bị SD-WAN  
- Tự động thiết lập tunnel  
- Tự động áp dụng chính sách Cloud WAN  

---

## Kết luận

Giải pháp kết hợp giữa **AWS Cloud WAN** và **Fortinet SD-WAN** cho phép Best Buy Health xây dựng một **mạng lưới chăm sóc sức khỏe resilient, bảo mật, hiệu quả**.

Mô hình này giúp họ:

- Giảm chi phí vận hành  
- Đơn giản hóa quản lý mạng tại scale lớn  
- Cải thiện hiệu năng kết nối  
- Tăng độ tin cậy cho các dịch vụ chăm sóc sức khỏe quan trọng  

