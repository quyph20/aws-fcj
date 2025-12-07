---
title: "Blog 3"
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---

# Building a Resilient Care Network with AWS Cloud WAN and SD-WAN | Best Buy Health

In Retail and Healthcare, reliable connectivity and high availability are essential for serving customers and maintaining operations. Organizations in these sectors often need to connect the enterprise network to stores, contact centers, distribution hubs — or in the case of Best Buy Health, **Care Centers**.

Best Buy Health empowers care at home by providing connected health devices, friendly technology for seniors, and a care-providing team for technical, emergency, and social needs. This post describes the technical solution Best Buy Health uses to integrate **Fortinet FortiGate SD-WAN** into an **Amazon VPC** using **AWS Cloud WAN**. This “transitive” type approach allows Best Buy Health to unify its network design and operational model between branch sites and AWS.

---

## Architecture Overview

Best Buy Health uses a **hub-and-spoke model** to connect multiple Care Centers and AWS-hosted workloads. Their architecture relies on:

- **AWS Cloud WAN** for global network orchestration  
- **SD-WAN (Fortinet FortiGate)** for secure, optimized branch connectivity  
- **Transit Gateway (TGW)** within each AWS Region  
- **Site-to-Site VPN tunnels** between SD-WAN appliances and AWS  
- **Redundant management appliances** for resilience  

This design allows Best Buy Health to simplify network operations, reduce manual configuration, and improve performance between remote sites and AWS workloads.

---

## Key Architecture Components

### **1. AWS Cloud WAN Core Network**
A global network that centralizes configuration, routing, and policy.  
It connects Regions, TGWs, SD-WAN appliances, and branch locations through Cloud WAN attachments.

### **2. SD-WAN Management VPC**
Hosts two redundant **Fortinet FortiGate appliances**:

- One for **management**
- One for **VPN and SD-WAN termination**

This VPC provides:

- IPSec termination for SD-WAN tunnels  
- Dynamic routing interoperability (using BGP over IPSec)  
- Common network egress policies  

### **3. Transit Gateway**
Acts as the **Regional hub** connecting:

- SD-WAN VPC  
- Application VPCs  
- Shared services VPCs  
- Other VPCs in the Region  

### **4. Branch Locations (Care Centers)**

Care Centers connect through:

- Local FortiGate SD-WAN devices  
- Dual VPN tunnels per Region for high availability  
- Automated path steering for performance and failover  

---

## Network Traffic Flow

1. Branch SD-WAN device establishes **two IPSec VPN tunnels** to FortiGate in AWS  
2. FortiGate connects into the **Transit Gateway** inside the SD-WAN VPC  
3. Transit Gateway routes traffic to **application VPCs**  
4. Cloud WAN orchestrates routing between Regions and VPCs  

All routing is centrally controlled in Cloud WAN, minimizing manual configuration at branch sites.

---

## Why Best Buy Health Uses This Model

### **1. Simplified Network Operations**
Cloud WAN allows central policy and routing control across Regions and sites.

### **2. Enhanced Resilience**
Redundant:

- SD-WAN appliances  
- IPSec tunnels  
- Transit Gateway attachments  
- Regional interconnects  

Improves uptime for critical health services.

### **3. Consistent Security**
Using Fortinet SD-WAN:

- Consistent firewall policies  
- Encrypted tunnels  
- Uniform branch posture  

### **4. Direct AWS Integration**
SD-WAN has native Cloud WAN support — making onboarding fast and automated.

---

## Benefits Achieved

Best Buy Health improved:

- **Reliability** of connections between Care Centers and AWS  
- **Operational efficiency** through centralized Cloud WAN management  
- **Network visibility** across all Regions and sites  
- **Performance** thanks to SD-WAN path steering  
- **Scalability**, enabling new Care Centers to be added quickly  

This architecture provides a strong foundation for delivering reliable healthcare-at-home services.

---

## Conclusion

By integrating **Fortinet SD-WAN** with **AWS Cloud WAN**, **Transit Gateway**, and **Amazon VPC**, Best Buy Health achieved:

- A unified multi-Region network  
- High availability for critical Care Center operations  
- Simplified onboarding and network management  
- Strong security posture  
- A scalable platform for future expansion  

This solution demonstrates how organizations with distributed operations — especially in healthcare — can build a resilient, manageable, cloud-integrated network using AWS networking services.
