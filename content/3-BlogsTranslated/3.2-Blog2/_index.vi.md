---
title: "Blog 2"
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---

# Cách CommBank xây dựng Nền tảng Giao dịch CommSec với Tính Sẵn sàng Cao và Khả năng Phục hồi Hoạt động

CommSec — nhà môi giới trực tuyến hàng đầu của Úc và là công ty con của Commonwealth Bank of Australia (CommBank) — giúp hàng triệu khách hàng gia tăng tài sản bằng cách cung cấp nền tảng đầu tư dễ sử dụng, dễ tiếp cận và chi phí hợp lý cho cả thị trường Úc và quốc tế.

CommSec cung cấp các dịch vụ quan trọng như nghiên cứu thị trường, quản lý danh mục và thực hiện giao dịch. Vì khách hàng mong đợi hệ thống hoạt động 24/7, nền tảng cần duy trì độ tin cậy cực cao. Là tổ chức chịu sự quản lý của ASIC, CommSec cũng phải đảm bảo chủ quyền dữ liệu và khả năng phục hồi của nền tảng để bảo vệ tính toàn vẹn của thị trường tài chính Úc.

Bài viết này mô tả cách CommSec sử dụng các dịch vụ AWS để xây dựng nền tảng giao dịch có tính sẵn sàng cao, hiệu suất mạnh mẽ, đồng thời đáp ứng yêu cầu tuân thủ nghiêm ngặt và mang đến trải nghiệm người dùng vượt trội.

---

## Thách thức khi vận hành môi trường đa đám mây

CommSec là khối lượng công việc quan trọng đầu tiên trong CommBank chuyển từ trung tâm dữ liệu tại chỗ lên đám mây công cộng.

- **2015**: di chuyển tầng web + mobile  
- **2019**: di chuyển tầng ứng dụng  

Ban đầu, họ áp dụng **kiến trúc đa đám mây chủ động–chủ động (active–active)** giữa AWS và một nhà cung cấp khác để tăng độ tin cậy.

Tuy nhiên, mô hình đa đám mây tạo ra nhiều thách thức:

- Hai pipeline triển khai  
- Hai mô hình vận hành khác nhau  
- Cơ chế failover tự xây dựng, phụ thuộc hệ thống giám sát ngoài  
- Tăng chi phí vận hành  
- Tốc độ phát triển chậm  
- Hạn chế sử dụng các dịch vụ cloud-native  
- Khó đổi mới do phải giữ tính tương đồng giữa hai môi trường  

---

## Tổng quan giải pháp

Đầu **2025**, CommSec tái kiến trúc toàn bộ tầng ứng dụng, web và mobile để chạy **hoàn toàn trên AWS**, sau khi AWS được chọn làm nhà cung cấp đám mây chính của CommBank.

Họ tạo ra một ranh giới cô lập lỗi mới:

### **➡ Availability Zone (AZ) trở thành domain lỗi chính**

Với **Amazon Application Recovery Controller (ARC) – zonal shift**, CommSec có thể:

- Chuyển tải (fail traffic) khỏi AZ bị lỗi  
- Xử lý các lỗi hạ tầng hoặc lỗi “xám” (gray failures)  
- Giữ được sự cô lập vật lý + logic giữa các AZ  

ARC được bật trên load balancer để chuyển hướng traffic khỏi AZ gặp sự cố **mà không cần phụ thuộc control plane**.

Điều này giúp họ đạt được khả năng phục hồi tương tự mô hình đa đám mây trước kia — **nhưng đơn giản hơn rất nhiều**.

### Lợi ích chính:

- **Failover tự động** qua ARC zonal shift  
- **Playbook được chuẩn hóa và kiểm thử thường xuyên**  
- Tốc độ triển khai + cập nhật hệ điều hành **nhanh gấp 2 lần**  
- Chạy trên 3 AZ giúp **giảm 25% capacity cơ bản** so với mô hình cũ 4 ngăn đa đám mây  
- Giảm chi phí vận hành  

---

## Các cải tiến về khả năng phục hồi

### **1. Scaling có độ bền cao**

Vì ứng dụng scale-in/out nhiều lần mỗi ngày:

- Logic bootstrap khi scale-out được thiết kế **tự chứa**  
- Binary ứng dụng lưu trong **Amazon S3 cùng tài khoản AWS**  
→ Tránh phụ thuộc bên ngoài khi scaling  

### **2. Xử lý mức tăng đột biến lưu lượng**

Lưu lượng của CommSec **tăng gấp 3 lần chỉ trong 3 phút** (9:59–10:02 AM, lúc thị trường mở cửa).

Giải pháp:

- Sử dụng **Load Balancer Capacity Unit (LCU) reservations**  
→ Dự trữ năng lực ALB trước  
→ Tránh phụ thuộc scaling phản ứng  

### **3. Health check cho lỗi cứng (hard failures)**

- ALB tự động loại instance không khỏe  
- Tạo cảnh báo để đội vận hành xử lý  

### **4. Cải thiện kết nối với sở giao dịch**

- Thiết lập liên kết **AWS Direct Connect** với Australian Liquidity Centre  
→ Cải thiện độ tin cậy cho hoạt động thị trường (ASX & CBOE)  

---

## ARC Zonal Shift để giảm thiểu sự cố

Ra mắt năm 2023, ARC zonal shift cho phép:

- Chuyển tải khỏi AZ đang gặp sự cố  
- Giảm ảnh hưởng từ outage hoặc lỗi một phần  
- Hỗ trợ:
  - ALB / NLB  
  - EC2 Auto Scaling  
  - Amazon EKS  

### Cách hoạt động:

Khi kích hoạt zonal shift:

1. **ALB loại bỏ IP node trong AZ bị lỗi khỏi DNS**  
   → Request mới không đi vào node đó  
2. **Các node ALB còn lại dừng gửi traffic** đến target trong AZ bị lỗi  
   → Ngăn traffic đi vào workload không khỏe  

Load balancing chéo AZ vẫn hoạt động ở các AZ khỏe.

Khi sự cố được khắc phục:

- Hủy zonal shift  
- Traffic phân phối lại như bình thường  

---

## Lợi ích của ARC Zonal Shift

- Tăng SLA khả dụng  
- Loại bỏ failover thủ công nhiều bước  
- Giảm thất thoát doanh thu khi xảy ra lỗi  
- Cho phép kiểm thử khả năng phục hồi thường xuyên, rủi ro thấp  
- Tăng niềm tin nội bộ về khả năng chịu lỗi của hệ thống  

> “ARC zonal shift là cách hiệu quả nhất để CommSec sử dụng dịch vụ AWS mà vẫn đáp ứng yêu cầu về tính phục hồi… Hy vọng chúng tôi sẽ không bao giờ cần dùng đến nó, nhưng việc kiểm thử thường xuyên giúp đảm bảo rằng nó sẽ hoạt động khi cần.”  
> — **Henry Zhao, Staff Software Engineer, CommBank**

---

## Kết luận

Bằng cách hợp nhất lên AWS và sử dụng các mô hình kiến trúc Multi-AZ hiện đại, nền tảng giao dịch CommSec hiện cung cấp:

- Độ tin cậy vượt trội  
- Tuân thủ quy định mạnh mẽ  
- Trải nghiệm khách hàng tốt hơn  
- Kiến trúc đơn giản hóa  
- Giảm chi phí vận hành  

ARC zonal shift, thiết kế load balancer tối ưu, kết nối Direct Connect và các playbook vận hành vững chắc đã tạo nên một **nền tảng giao dịch có tính sẵn sàng cao và khả năng phục hồi mạnh mẽ**, phục vụ hàng triệu nhà đầu tư tại Úc.
