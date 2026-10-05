# Architecture

## 1. Overview

This project implements a small production-inspired cloud environment
on Oracle Cloud Infrastructure (OCI).

The architecture is designed to demonstrate core cloud engineering
concepts including network segmentation, private compute workloads,
managed services, controlled public exposure, identity-based access
and layered security.

## 2. Architecture Diagram

![OCI Lab Architecture](../assets/architecture.png)

The diagram represents the current state of the laboratory and its
main OCI resources.

## 3. Architecture Components

| Component | Purpose |
|---|---|
| OCI VCN | Main network boundary for the laboratory |
| Public Subnet | Hosts the public-facing Load Balancer |
| App Subnet | Private network for the application VM |
| DB Subnet | Private subnet reserved for database-oriented workloads |
| Load Balancer | Public entry point for the web application |
| Web VM | Application/web workload running on Oracle Linux |
| Bastion Service | Secure administrative access to the private VM |
| Object Storage | OCI-managed object storage |
| Autonomous Database | Managed relational database service |
| IAM | Identity and access management |

## 4. High-Level Traffic Flows

### User → Application

Internet traffic reaches the OCI Load Balancer through the
public subnet.

The Load Balancer forwards requests to the `web-vm`, which resides
in the private `app-subnet`.

```text
Internet
   │
   ▼
Load Balancer
   │
   ▼
app-subnet
   │
   ▼
web-vm

### **Administrative Access**

Administrative access to the private VM is provided through the  
 OCI Bastion Service.

```text
Administrator
     │
     ▼
OCI Bastion Service
     │
     ▼
web-vm

### **Application → OCI Services**

The application VM can access supported OCI services through the  
 Service Gateway without requiring those services to be exposed  
 through the public Internet.

'''text
web-vm
   │
   ▼
Service Gateway
   ├──► Object Storage
   └──► Autonomous Database

The Autonomous Database used by this laboratory is an  
 **Autonomous Database Serverless / Always Free** deployment.  
 It uses a public endpoint and is not located inside the VCN.

## **5\. Network Segmentation**

The VCN is divided into three subnets:

* `public-subnet` — public-facing resources  
* `app-subnet` — private application workload  
* `db-subnet` — private subnet reserved for database-oriented workloads

This segmentation separates public entry points from the application  
 workload and provides a foundation for applying different network  
 controls.

## **6\. Security Architecture**

Security is implemented in multiple layers:

1. **IAM** — controls access to OCI resources.  
2. **Network segmentation** — separates public and private workloads.  
3. **Route tables and gateways** — control network paths.  
4. **Security Lists and NSGs** — control network traffic.  
5. **Bastion Service** — provides controlled administrative access.  
6. **Instance Principal** — allows the VM to authenticate to OCI  
    services without storing OCI API credentials.

Detailed security configuration is documented separately in  
 `security.md` and `networking.md`.

## **7\. Design Principles**

The architecture follows several practical cloud engineering  
 principles:

* Minimize direct public exposure.  
* Keep application workloads in private subnets where possible.  
* Use managed OCI services instead of self-managed infrastructure  
   when appropriate.  
* Separate resources using OCI compartments.  
* Use identity-based authentication for workload-to-service access.  
* Apply network security controls at the appropriate layer.  
* Keep the architecture simple enough to operate and understand.
