---
title: "Event 3"
weight: 1
chapter: false
pre: " <b> 4.3. </b> "
---

# Bài Thu Hoạch “AWS DevOps Workshop”

## Thông Tin Sự Kiện
- **Thời gian:** Thứ Hai, 17/11/2025 – (8:30 AM - 17:00 PM )
- **Địa điểm:** Văn phòng AWS Vietnam  
- **Vai trò:** Người tham dự  

---

## Mục Đích Của Sự Kiện

Workshop được thiết kế giúp người tham dự:

- Hiểu toàn diện về DevOps culture, principles và best practices  
- Trải nghiệm thực hành các dịch vụ DevOps của AWS  
- Xây dựng CI/CD pipelines thực tế  
- Triển khai Infrastructure as Code với CloudFormation và CDK  
- So sánh các container services (ECS, EKS, App Runner)  
- Thiết lập monitoring & observability hoàn chỉnh  
- Học cách cải thiện hiệu suất, độ tin cậy và automation trong hệ thống  

---

# Tổng Quan Chương Trình

## **Buổi Sáng (8:30 – 12:00)**

### **8:30 – 9:00 | Chào Mừng & Tư Duy DevOps**
- Tóm tắt phiên AI/ML từ workshop trước  
- Văn hóa DevOps: hợp tác – tự động hóa – cải tiến liên tục  
- Các chỉ số quan trọng:
  - **DORA Metrics** (Deployment Frequency, Lead Time, MTTR, Change Failure Rate)
  - MTTR – thời gian phục hồi sau lỗi  
  - Tần suất triển khai  
- Thảo luận về lợi ích DevOps trong giao hàng phần mềm & vận hành  

---

### **9:00 – 10:30 | AWS DevOps Services – CI/CD**

#### ⭐ Source Control – AWS CodeCommit & Git Strategies
- GitFlow  
- Trunk-Based Development  
- Chọn chiến lược phù hợp dựa theo team size  

#### ⭐ Build & Test – CodeBuild
- buildspec.yml  
- Automated unit tests, integration tests  
- Artifacts, environment variables  

#### ⭐ Deployment – CodeDeploy
- Blue/Green deployment  
- Canary deployment  
- Rolling updates + rollback  

#### ⭐ Orchestration – CodePipeline
- Stages: Source → Build → Test → Deploy  
- Automated triggers, parallel execution  
- Visualization pipeline  

#### ⭐ Demo CI/CD Pipeline End-to-End  
- Tạo repo CodeCommit  
- Build & test với CodeBuild  
- Triển khai Blue/Green qua CodeDeploy  
- Điều phối bằng CodePipeline  

---

### **10:45 – 12:00 | Infrastructure as Code (IaC)**

#### ⭐ CloudFormation
- Template YAML/JSON  
- Stacks, change sets, rollback  
- Drift detection  
- Best practices: parameterization, nested stacks  

#### ⭐ AWS CDK
- Định nghĩa hạ tầng bằng TypeScript/Python  
- Constructs & reusable patterns  
- Developer experience vượt trội  
- IDE support + type safety  

#### ⭐ Demo So Sánh CloudFormation vs CDK
- Triển khai VPC + EC2 bằng YAML  
- Triển khai cùng kiến trúc bằng CDK TypeScript  
- So sánh maintainability, simplicity  

#### ⭐ Khi nào dùng CloudFormation vs CDK?
- Tuỳ team skillset & độ phức tạp  
- Có thể hybrid  

---

# Buổi Chiều (13:00 – 17:00)

## **13:00 – 14:30 | Container Services trên AWS**

### ⭐ Docker Basics
- Containers, images  
- Dockerfile, build, lifecycle  
- Lợi ích: portability, consistency  

### ⭐ Amazon ECR
- Secure docker registry  
- Image scanning  
- Lifecycle policies  

### ⭐ ECS & EKS
#### ECS:
- Task definition, services  
- Rolling/Blue-Green deployments  
- Autoscaling  

#### EKS:
- Kubernetes managed control plane  
- Pods, deployments, namespaces  
- Autoscaler  

### ⭐ AWS App Runner
- Deploy container rất đơn giản  
- Auto-scaling theo traffic  
- Use cases: web apps, APIs  

### ⭐ Demo & Case Study
- Deploy web app với App Runner  
- Deploy lại bằng ECS Fargate  
- So sánh complexity – cost – operations  

---

## **14:45 – 16:00 | Monitoring & Observability**

### ⭐ CloudWatch
- Metrics, Logs, Alarms  
- Dashboards  
- Best practices: naming convention, retention policies  

### ⭐ AWS X-Ray
- Distributed tracing  
- Service map, trace insights  
- Tích hợp Lambda, ECS, API Gateway  

### ⭐ Demo Full-Stack Observability
- Build metrics, logs  
- Thiết lập alarms  
- Kích hoạt tracing  
- Phân tích real traces  

### ⭐ Best Practices
- Alerting strategy  
- Dashboard for Developers vs Ops vs Management  
- On-Call runbooks  
- SLO/SLI  

---

## **16:00 – 16:45 | DevOps Best Practices & Case Studies**

- Feature flags & A/B testing (AppConfig, LaunchDarkly)  
- Test Automation & test pyramid  
- Quality gates trong CI/CD  
- Incident management & postmortems  
- Case study startup vs enterprise transformation  
- ROI: đo lường cải thiện DevOps qua DORA metrics  

---

## **16:45 – 17:00 | Q&A & Tổng Kết**
- Lộ trình nghề nghiệp DevOps  
- Chứng chỉ AWS phù hợp: DevOps Pro, SA, SysOps  
- Tài nguyên học tập tiếp theo  

---

# Nội Dung Nổi Bật

- CI/CD automation bằng CodePipeline → tăng tốc delivery  
- IaC với CloudFormation & CDK → nhất quán, versioned  
- Container services đa dạng: App Runner, ECS, EKS  
- Observability toàn diện: CloudWatch + X-Ray  
- Văn hoá DevOps quan trọng hơn công cụ  
- Feature flags, automated testing, incident response cực kỳ cần thiết  

---

# Những Gì Tôi Học Được

## 📌 DevOps là văn hóa – không chỉ là công nghệ
## 📌 CI/CD automation giúp giảm lỗi, tăng tốc phát triển
## 📌 IaC mang lại repeatability & maintainability
## 📌 Chọn đúng dịch vụ container tuỳ theo complexity
## 📌 Observability là yêu cầu bắt buộc cho production
## 📌 DevOps = học liên tục + cải tiến liên tục  

---

# Ứng Dụng Vào Công Việc

- Áp dụng CI/CD với CodePipeline  
- Dùng CDK/CloudFormation để quản lý hạ tầng  
- Đánh giá containerization cho apps hiện tại  
- Cải thiện dashboards & alarms  
- Áp dụng DevOps mindset trong team  
- Bắt đầu xây dựng quy trình incident response + postmortem  

---

# Trải Nghiệm Cá Nhân

- Demo CI/CD rất thực tế và hữu ích  
- Hiểu rõ sự khác biệt giữa CloudFormation và CDK  
- Comparison App Runner vs ECS vs EKS cực kỳ insightful  
- Observability session giúp tôi hiểu tầm quan trọng của tracing  
- Case studies mang lại góc nhìn thực tế  
- Roadmap nghề nghiệp DevOps rất truyền cảm hứng  

---

# Một Số Hình Ảnh Khi Tham Gia Sự Kiện
*(Thêm hình ảnh tại đây nếu cần)*

---

> **Tổng kết:**  
Workshop DevOps mang đến góc nhìn toàn diện, kỹ thuật thực chiến và định hướng rõ ràng cho việc áp dụng DevOps trong công việc. Đây là sự kiện rất hữu ích cho bất kỳ ai theo đuổi DevOps, Cloud, hoặc Software Engineering nói chung.

