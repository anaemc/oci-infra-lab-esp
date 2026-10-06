# Identity & Compartments

## 1. Overview

Identity and resource organization in this laboratory are managed
using Oracle Cloud Infrastructure Identity and Access Management
(IAM).

The design separates resources into dedicated compartments according
to their functional role and uses IAM policies to control access.

Workload authentication is handled through OCI workload identity
mechanisms rather than storing long-lived OCI API credentials on the
compute instance.

## 2. Tenancy Structure

The laboratory uses a simple compartment structure under the tenancy
root compartment:

```text
root
├── networking
├── compute
├── storage
└── database
```

The structure separates resources by functional responsibility rather
than creating a separate compartment for every individual resource.


---

## 3. Compartments

| Compartment | Purpose | Main resources |
|---|---|---|
| `networking` | Network infrastructure | VCN, subnets, gateways, route tables, Security Lists, NSGs |
| `compute` | Compute workloads | `web-vm` |
| `storage` | Object storage resources | Object Storage buckets |
| `database` | Database services | Autonomous Database |

The compartment structure provides logical separation of resources
while keeping the laboratory simple enough to operate and understand.

The `networking` compartment contains the shared network foundation,
while workload resources are placed in dedicated functional
compartments.

Los compartments no son un mecanismo de seguridad por sí mismos.  Son
principalmente una frontera lógica y administrativa, sobre la que después
se construyen las políticas IAM.

Compartments organize resources; IAM policies determine who can access them.

---

## 4. Access Control

```text
IAM
│
├── Human access
│   └── Users / Groups / Policies
│
└── Workload access
    └── Dynamic Groups / Instance Principals / Policies
```
### Users and Groups

Human access to OCI resources is managed through IAM users and groups.

Policies are attached to groups rather than directly to individual
users whenever possible.

This allows permissions to be managed according to roles and makes
access easier to audit and maintain.

## 5. Workload Identity

The application VM uses OCI workload identity to authenticate to OCI
services without storing long-lived user credentials on the instance.

### Dynamic Group

The compute instance is included in the `app-instances` dynamic group.

The dynamic group allows IAM policies to grant permissions to the
instance as a workload identity.

### Instance Principal

The `web-vm` uses Instance Principal authentication when accessing
OCI APIs.

For example:

```bash
oci os ns get --auth instance_principal
```

The command successfully retrieves the Object Storage namespace without
requiring an OCI user API key or configuration file containing
long-lived credentials.

## 6. Resource Organization

Resources are organized according to their functional role:

```text
networking
    └── VCN and network infrastructure

compute
    └── web-vm

storage
    └── Object Storage buckets

database
    └── Autonomous Database

This organization makes it easier to reason about ownership,
permissions and resource management.


---

## 7. Design Decisions

### Functional compartment separation

Resources are grouped by function rather than by individual service
instance.

### Group-based permissions

IAM permissions are assigned to groups where possible instead of
being granted individually to users.

### Workload identity

The compute workload uses Instance Principal authentication instead of
storing long-lived OCI credentials on the VM.

### Separation of infrastructure and workloads

Network infrastructure is isolated in the `networking` compartment,
while compute, storage and database resources are organized separately.

