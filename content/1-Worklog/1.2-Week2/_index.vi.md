---
title: "Worklog Tuần 2"

weight: 1
chapter: false
pre: " <b> 1.2. </b> "
---


### Mục tiêu tuần 2:

* Mục tiêu là nắm vững mô hình Trách nhiệm chung và các thành phần cốt lõi của IAM.
* Thực hiện thiết lập Groups/Users theo nguyên tắc Đặc quyền Tối thiểu và kích hoạt MFA.
### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Mô hình Trách nhiệm Chung (Shared Responsibility Model): Phân biệt rõ ràng trách nhiệm của AWS (Bảo mật của Cloud: hạ tầng vật lý) và trách nhiệm của Người dùng (Bảo mật trong Cloud: cấu hình, dữ liệu). Hiểu rằng đây là nguyên tắc nền tảng của bảo mật trên AWS.                                                                                             | 15/09/2025   | 15/09/2025      |
| 3   | - Thành phần cơ bản của IAM (Users & Groups): Nắm vững cách tạo và quản lý IAM Users (danh tính cho người dùng) và gán họ vào IAM Groups để quản lý quyền truy cập tập trung, tiết kiệm thời gian.                                            | 16/09/2025   | 16/09/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Cơ chế Ủy quyền (Roles & Policies): Hiểu rõ cách các IAM Policies (tài liệu JSON định nghĩa quyền) được tạo ra và gán cho Roles hoặc Users để định nghĩa chính xác các hành động được phép/bị cấm trên tài nguyên AWS. | 17/09/2025   | 17/09/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Nguyên tắc Đặc quyền Tối thiểu (Least Privilege): Áp dụng nguyên tắc Least Privilege làm kim chỉ nam để luôn cấp những quyền tối thiểu cần thiết cho một danh tính, tránh việc lạm dụng hoặc lộ lọt quyền hạn.                  | 18/09/2025   | 18/09/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - Bảo mật Danh tính bằng MFA: Hiểu tầm quan trọng của Multi-Factor Authentication (MFA) trong việc bảo vệ tài khoản. Thiết lập MFA là bước bắt buộc để tăng cường bảo mật cho tài khoản quản trị (Root User và IAM User quan trọng).                                                                                         | 19/09/2025   | 19/09/2025      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 2:

* Cấu hình IAM Users và Groups: Tạo một IAM Group có tên là DevTeam và một IAM User mới. Gán User vào Group DevTeam. Kết quả: Xác nhận User tự động thừa hưởng các quyền được gán cho Group, đơn giản hóa việc quản lý truy cập theo nhóm.

* Thực hành với IAM Policies: Xây dựng một IAM Policy cho phép User chỉ được phép đọc (Read-Only) các bucket S3 cụ thể. Ngược lại, thử nghiệm một Policy từ chối truy cập vào dịch vụ EC2. Kết quả: Hiểu rõ cách Policy hoạt động theo cơ chế Implicit Deny và kiểm soát truy cập chi tiết.

* Tổng kết Ứng dụng Bảo mật: Đã hoàn thành việc thiết lập MFA cho các User quan trọng và áp dụng thành công nguyên tắc Đặc quyền Tối thiểu (Least Privilege) thông qua các Policy tùy chỉnh. Kết quả: Thiết lập được nền tảng bảo mật vững chắc cho các tuần triển khai tiếp theo.

