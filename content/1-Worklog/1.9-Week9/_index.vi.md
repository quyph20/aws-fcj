---
title: "Worklog Tuần 9"

weight: 1
chapter: false
pre: " <b> 1.9. </b> "
---
{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}


### Mục tiêu tuần 9:

* Nắm vững các dịch vụ giám sát (CloudWatch Metrics, Logs) và thông báo (SNS).
* Thực hành cấu hình CloudWatch Alarms, SNS Topic và sử dụng Systems Manager để quản lý vận hành từ xa.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Dịch vụ Giám sát Cốt lõi (CloudWatch): Hiểu rõ Amazon CloudWatch là dịch vụ trung tâm để giám sát và quản lý tài nguyên, thu thập các chỉ số (Metrics), nhật ký (Logs) và sự kiện (Events) từ AWS và các ứng dụng.                                                                                             | 03/11/2025   | 03/11/2025      |
| 3   | - Phân biệt Metrics và Logs: Phân biệt rõ ràng giữa Metrics (dữ liệu số liệu theo thời gian, ví dụ: CPU Utilization) và Logs (dữ liệu văn bản chi tiết ghi lại hoạt động). Nắm được cách CloudWatch thu thập cả hai loại.                                            | 04/11/2025   | 04/11/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Cấu hình Cảnh báo (Alarms): Hiểu cách tạo CloudWatch Alarms dựa trên các ngưỡng của Metrics (ví dụ: CPU > 80% trong 5 phút). Nắm được cách Alarms có thể kích hoạt các hành động tự động (Actions) thông qua SNS hoặc Auto Scaling. | 05/11/2025   | 05/11/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Dịch vụ Thông báo (SNS): Nắm được Amazon Simple Notification Service (SNS) là dịch vụ nhắn tin được quản lý để gửi tin nhắn đến các Subscriptions (email, SMS, Lambda, SQS) khi có sự kiện (ví dụ: cảnh báo).                  | 06/11/2025   | 06/11/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - Công cụ Quản lý Vận hành: Giới thiệu về AWS Systems Manager (SSM) là một bộ công cụ để tự động hóa các tác vụ vận hành như patch OS, chạy lệnh từ xa (Run Command) và quản lý cấu hình.                                                                                         | 07/11/2025   | 07/11/2025      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 9:

* Cấu hình CloudWatch Alarms: Tạo một CloudWatch Alarm cho EC2 Instance trong VPC (từ Tuần 6), đặt ngưỡng cảnh báo khi CPU Utilization vượt quá 75% liên tục trong 5 phút.

* Thiết lập Kênh Thông báo (SNS Topic): Khởi tạo một SNS Topic mới và cấu hình Subscription qua Email. Kết quả: Đã xác nhận nhận được email thông báo ngay khi Alarm chuyển sang trạng thái ALARM.

* Quản lý Log tập trung: Cấu hình CloudWatch Agent trên EC2 Instance để thu thập các log của ứng dụng tùy chỉnh và gửi chúng đến CloudWatch Logs. Kết quả: Có khả năng giám sát nhật ký ứng dụng từ một bảng điều khiển tập trung.

* Thực hiện Tác vụ Vận hành với SSM: Sử dụng AWS Systems Manager Run Command để thực thi một lệnh shell đơn giản (ví dụ: kiểm tra phiên bản kernel) trên một EC2 Instance mà không cần SSH trực tiếp. Kết quả: Xác nhận khả năng quản lý tài nguyên an toàn và tập trung.

* Tổng kết Ứng dụng Giám sát: Đã hoàn thành việc thiết lập các công cụ giám sát, cảnh báo và tự động hóa vận hành. Kết quả: Hệ thống có khả năng chủ động theo dõi hiệu suất, phản ứng nhanh với các sự cố và duy trì sức khỏe tài nguyên ở mức cao.


