---
title: "Worklog Tuần 10"

weight: 2
chapter: false
pre: " <b> 1.10. </b> "
---


### Mục tiêu tuần 10:

* Hiểu nguyên tắc Infrastructure as Code (IaC) và dịch vụ CloudFormation là cốt lõi.
* Thực hành viết, triển khai CloudFormation Template và sử dụng Change Sets để quản lý vòng đời Stack.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Khái niệm Infrastructure as Code (IaC): Hiểu rõ IaC là việc quản lý và cung cấp tài nguyên hạ tầng thông qua các tệp mã (ví dụ: JSON/YAML) thay vì cấu hình thủ công. Nắm được lợi ích về tính nhất quán và khả năng lặp lại.                                                                                             | 10/11/2025   | 10/11/2025      |
| 3   | - Dịch vụ Triển khai Cốt lõi (CloudFormation): Nắm vững AWS CloudFormation là dịch vụ IaC chính của AWS, sử dụng Templates để mô tả tài nguyên và quản lý chúng dưới dạng một Stack duy nhất.                                            | 11/11/2025   | 11/11/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Mô hình Cung cấp Ứng dụng: Phân biệt các mô hình triển khai: AWS CodeDeploy (tự động hóa việc triển khai ứng dụng lên EC2, Lambda), và AWS Elastic Beanstalk (nền tảng giúp đơn giản hóa việc triển khai ứng dụng). | 12/11/2025   | 12/11/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Các Dịch vụ CI/CD: Giới thiệu về Continuous Integration/Continuous Delivery (CI/CD). Nắm được vai trò của AWS CodeCommit (Quản lý mã nguồn), CodeBuild (Xây dựng mã), và CodePipeline (Điều phối quá trình CI/CD).                  | 13/11/2025   | 13/11/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - Quản lý Thay đổi Hạ tầng: Hiểu cách CloudFormation Change Sets cho phép người dùng xem trước những thay đổi dự kiến đối với các tài nguyên đang hoạt động trước khi thực hiện cập nhật Stack, giảm thiểu rủi ro lỗi.                                                                                         | 14/11/2025   | 14/11/2025      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 10:

* Xây dựng CloudFormation Template: Viết một CloudFormation Template bằng YAML. Template này mô tả việc khởi tạo một tài nguyên đơn giản (ví dụ: một S3 Bucket hoặc một IAM User).

* Triển khai và Quản lý Stack: Sử dụng Console hoặc AWS CLI để triển khai Template đã viết thành một Stack hoạt động. Sau đó, thực hiện cập nhật Stack bằng cách thay đổi Template và xem trước Change Set.

* Thử nghiệm Triển khai Tự động (CodeDeploy): Mô phỏng việc triển khai phiên bản ứng dụng mới lên EC2 Instance bằng CodeDeploy. Kết quả: Quan sát được quá trình triển khai tự động, giảm thời gian downtime.

* Tổng kết Ứng dụng IaC: Đã hoàn thành việc chuyển đổi tư duy quản lý hạ tầng sang IaC. Kết quả: Có khả năng tạo ra, quản lý, và lặp lại các tài nguyên hạ tầng AWS một cách nhất quán, có thể kiểm toán và dễ dàng đưa vào quy trình CI/CD.


