---
title: "Event 3"
weight: 1
chapter: false
pre: " <b> 4.3. </b> "
---

# “DevOps on AWS Workshop”

### Date & Time
**Monday, November 17, 2025, (8:30 AM – 17:00 PM)**  
**Location:** AWS Vietnam Office  
**Role:** Attendee  

---

## Event Purpose

The workshop was designed to provide comprehensive knowledge and hands-on experience with **AWS DevOps services**, covering CI/CD pipelines, Infrastructure as Code, container services, and monitoring & observability.  
Participants gained understanding of **DevOps culture, principles, and best practices**, along with practical implementation of DevOps workflows on AWS.

---

# Agenda Overview

## **Morning Session (8:30 AM – 12:00 PM)**

---

### **8:30 – 9:00 AM | Welcome & DevOps Mindset**

- Recap of AI/ML session from previous workshop  
- DevOps Culture & Principles: collaboration, automation, continuous improvement  
- Key Metrics:
  - **DORA Metrics**: deployment frequency, lead time for changes, MTTR, change failure rate  
  - **MTTR**: speed of recovery from failures  
  - **Deployment Frequency**: measuring release pace  
- How DevOps improves software delivery & operational performance  

---

### **9:00 – 10:30 AM | AWS DevOps Services – CI/CD Pipeline**

#### **Source Control: CodeCommit & Git Strategies**
- CodeCommit: secure & fully managed Git repositories  
- Git Strategies:
  - GitFlow  
  - Trunk-based Development  
- Best practices for branching & team workflows  

#### **Build & Test: CodeBuild**
- Buildspec configuration, environment variables  
- Unit tests, integration tests, test automation  
- Integration with testing frameworks & code quality tools  

#### **Deployment: CodeDeploy**
- Blue/Green deployments  
- Canary deployments  
- Rolling updates  
- When to choose which deployment strategy  

#### **Orchestration: CodePipeline**
- Pipeline stages: Source → Build → Test → Deploy  
- Automated triggers, parallel execution  
- Integrating CodeCommit, CodeBuild, CodeDeploy  

#### **Demo: Full CI/CD Pipeline**
- CodeCommit repo setup  
- CodeBuild automated build  
- CodeDeploy Blue/Green deployment  
- CodePipeline orchestration  
- Testing automated deployments  

---

### **10:30 – 10:45 AM | Break**

---

### **10:45 AM – 12:00 PM | Infrastructure as Code (IaC)**

#### **AWS CloudFormation**
- YAML/JSON templates  
- Stacks, change sets, rollback  
- Drift detection  
- Template best practices & nested stacks  

#### **AWS CDK**
- Define infrastructure using TypeScript/Python/Java/C#/Go  
- Reusable constructs & patterns  
- Type safety & IDE support  
- Better developer experience than raw CloudFormation  

#### **Demo: CloudFormation vs CDK**
- Deploy VPC + EC2 using CFN YAML  
- Deploy same architecture with CDK TypeScript  
- Comparison: maintainability, readability, complexity  

#### **When to choose CFN vs CDK**
- Depends on team expertise  
- Hybrid approaches are viable  

---

# **Lunch Break (12:00 – 1:00 PM)**

---

# Afternoon Session (1:00 – 5:00 PM)

---

## **1:00 – 2:30 PM | Container Services on AWS**

### **Docker Fundamentals**
- Containers, images, Dockerfiles  
- Microservices architecture  
- Benefits: portability, consistency, efficiency  

### **Amazon ECR**
- Secure image storage  
- Vulnerability scans  
- Lifecycle policies  
- Integration with ECS/EKS  

### **Amazon ECS**
- Task definitions, services  
- Rolling & Blue/Green deployments  
- Auto-scaling  
- Load balancing  

### **Amazon EKS**
- Kubernetes concepts: pods, services, deployments  
- Managed control plane  
- Node groups, add-ons  
- Rolling & canary deployments  
- Cluster autoscaler & HPA  

### **AWS App Runner**
- Simplified deployment from source or image  
- Auto-scaling based on traffic  
- Ideal for microservices & APIs  

### **Demo & Case Study**
- Deploy sample app with App Runner  
- Deploy again using ECS Fargate  
- Compare complexity, cost, operations  

---

### **2:30 – 2:45 PM | Break**

---

## **2:45 – 4:00 PM | Monitoring & Observability**

### **Amazon CloudWatch**
- Metrics, logs, alarms  
- Dashboards for applications  
- Naming conventions & log retention  
- Alert configuration best practices  

### **AWS X-Ray**
- Distributed tracing for microservices  
- Service map visualization  
- Latency & performance analysis  
- Integration with Lambda, API Gateway, ECS  

### **Demo: End-to-End Observability**
- Setting up CloudWatch metrics & logs  
- Building dashboards  
- Alarm configuration  
- Enabling X-Ray tracing  
- Analyzing traces & service maps  

### **Best Practices**
- Avoid alert fatigue  
- Dashboards per team: Dev, Ops, Management  
- On-call processes: escalation, incident workflows  
- SLO/SLI for reliability  

---

## **4:00 – 4:45 PM | DevOps Best Practices & Case Studies**

### **Deployment Strategies**
- Feature flags  
- A/B testing  
- AWS AppConfig & LaunchDarkly usage  

### **Automated Testing**
- Test pyramid: unit → integration → E2E  
- Automated gates in pipelines  
- Improving test coverage  

### **Incident Management & Postmortems**
- Incident detection & escalation  
- Recovery process  
- Blameless postmortems  
- Continuous improvement  

### **Case Studies: Startup & Enterprise**
- Startup: rapid scale, cost optimization  
- Enterprise: cultural transformation  
- Common challenges and solutions  
- Measuring ROI with DORA metrics  

---

### **4:45 – 5:00 PM | Q&A & Wrap-up**
- DevOps career pathways  
- AWS certification roadmap  
- Recommended learning resources  
- Key takeaways  

---

# Key Highlights

- Fully automated CI/CD with CodePipeline  
- IaC with CloudFormation & CDK  
- Container service comparison: ECS vs EKS vs App Runner  
- Full observability with CloudWatch + X-Ray  
- DevOps = culture change + automation + continuous improvement  
- Best practices: feature flags, test automation, incident response  

---

# Key Learnings

- DevOps is primarily a culture shift  
- CI/CD automation boosts release speed & reliability  
- IaC enables version control & consistency  
- Container strategy depends on complexity & team capability  
- Observability is mandatory for production systems  
- DevOps requires continuous learning & improvement  

---

# Application to My Work

- Implement CI/CD using CodePipeline  
- Adopt IaC using CFN or CDK  
- Evaluate containerizing existing services  
- Improve CloudWatch dashboards & alarms  
- Apply DevOps principles daily  
- Introduce incident management & postmortems  

---

# Personal Experience

The workshop was immersive and highly practical:

- CI/CD pipeline demo clarified automated workflows  
- Clear understanding of CloudFormation vs CDK  
- Container service comparison was extremely helpful  
- Observability session emphasized monitoring & tracing importance  
- Case studies showed real DevOps transformations  
- Career discussion provided strong motivation  

---

# Takeaways

- Start small with DevOps practices  
- Culture matters more than tools  
- Choose tools fitting team expertise  
- Monitor everything  
- Keep learning continuously  
- Use DORA metrics to evaluate improvement  

---

### Some Event Photos
*Add your event photos here*

