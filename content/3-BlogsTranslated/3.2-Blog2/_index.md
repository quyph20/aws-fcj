---
title: "Blog 2"
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---


# How CommBank Made Their CommSec Trading Platform Highly Available and Operationally Resilient

CommSec, Australia’s leading online broker and a subsidiary of the Commonwealth Bank of Australia (CommBank), helps millions of customers grow their wealth by making it easy, accessible, and affordable to invest in both Australian and international markets.

CommSec provides essential services such as market research, portfolio management, and trade execution. Because customers expect round-the-clock availability, the platform must maintain exceptional reliability. As a regulated entity under ASIC, CommSec must also ensure data sovereignty and platform resilience to protect the integrity of Australia’s financial markets.

This post explores how CommSec used AWS services to build a resilient, high-performing trading platform while meeting strict regulatory requirements and delivering an exceptional customer experience.

---

## Challenges of Operating a Multicloud Environment

CommSec was the first critical workload in CommBank to transition from on-premises data centers to the public cloud.

- **2015**: migrated web + mobile tier  
- **2019**: migrated application tier  

They initially adopted an **active–active multicloud architecture** (AWS + another cloud) to build resilience confidence.

However, operating multicloud introduced several challenges:

- Two deployment pipelines  
- Two different operating models  
- Custom failover requiring external witnesses  
- Additional operational overhead  
- Reduced development velocity  
- Limited ability to use cloud-native services  
- Innovation slowed due to parity requirements  

---

## Solution Overview

By early **2025**, CommSec rearchitected its app, web, and mobile tiers to run **entirely on AWS**, now that AWS had become CommBank’s preferred cloud provider.

They introduced a new fault-isolation boundary:

### **➡ Availability Zone (AZ) became the new fault domain**

Using **Amazon Application Recovery Controller (ARC) zonal shift**, CommSec can:

- Fail over away from impaired AZs  
- Handle infrastructure or application gray failures  
- Maintain physical + logical isolation across multiple AZs  

ARC zonal shift was enabled on their load balancers so they could divert traffic away from impaired AZs **without control plane dependencies**.

This simplification allowed them to replicate previous multicloud resilience—**but with far less complexity**.

### Key benefits:

- **Out-of-the-box failover** using ARC zonal shift  
- **Validated playbooks** with regular testing  
- Deployment + OS patching became **2× faster**  
- Running across 3 AZs enabled **25% base capacity reduction** compared to the old 4-stack multicloud setup  
- Lower operational cost  

---

## Resilience Improvements

### **1. Resilient Scaling**
Because scale-in/out happens multiple times daily:

- All scale-out bootstrap logic was redesigned to be **self-contained**  
- Application binaries stored in **Amazon S3 in the same AWS account**  
→ No external dependencies during scaling  

### **2. Handling Extreme Traffic Spikes**

CommSec traffic **triples within 3 minutes** at market open (9:59–10:02 AM).

To handle this:

- Implemented **Load Balancer Capacity Unit (LCU) reservations**  
→ Pre-allocates ALB capacity  
→ Avoids relying on reactive scaling  

### **3. Health Checks for Hard Failures**

- ALB health checks automatically remove unhealthy instances  
- Alerts notify the ops team for investigation  

### **4. Improved Exchange Connectivity**

- New **AWS Direct Connect** links to the Australian Liquidity Centre (ASX primary systems)  
- Improves reliability for market operations (ASX & CBOE)  

---

## ARC Zonal Shift to Mitigate Impairments

Launched in 2023, ARC zonal shift enables:

- Shifting traffic away from an impaired Availability Zone  
- Reducing impact from outages or partial failures  
- Supporting:
  - ALB / NLB  
  - EC2 Auto Scaling Groups  
  - Amazon EKS  

### How it works:

When CommSec initiates a zonal shift:

1. **Removes the ALB node’s IP** in the affected AZ from DNS  
   → New client requests avoid that node  
2. **Remaining ALB nodes stop routing traffic** to targets in the affected AZ  
   → Prevents routing into impaired workloads  

Cross-zone load balancing remains active in healthy AZs.

When the issue is resolved:

- They cancel the zonal shift  
- Traffic is restored evenly across all AZs  

---

## Benefits of ARC Zonal Shift

- Helps maintain higher availability SLAs  
- Eliminates multi-step manual failovers  
- Minimizes revenue loss during failures  
- Enables frequent, low-risk resilience testing  
- Builds organizational confidence in disaster recovery  

> “ARC zonal shift is the most efficient way for CommSec to use AWS services whilst meeting our resilience requirements… Hopefully it’s something we will never need, but our regular resilience testing ensures it’s there and will work if we ever need it.”  
> — **Henry Zhao, Staff Software Engineer, CommBank**

---

## Conclusion

By consolidating on AWS and using modern Multi-AZ architectural patterns, the CommSec trading platform now delivers:

- Exceptional reliability  
- Strong regulatory compliance  
- Enhanced customer experience  
- Simplified architecture  
- Reduced operational cost  

ARC zonal shift, optimized load balancer design, Direct Connect improvements, and robust operational playbooks together create a **highly available, operationally resilient trading platform** capable of supporting millions of Australian investors.

