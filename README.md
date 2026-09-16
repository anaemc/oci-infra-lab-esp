# OCI Cloud Engineering Lab – Arquitectura End-to-End

## 📌 Descripción

Este proyecto documenta el diseño e implementación de un entorno completo en la nube utilizando Oracle Cloud Infrastructure, con el objetivo de aprender y aplicar los conceptos fundamentales de Cloud Engineering en un entorno práctico.

El laboratorio cubre múltiples dominios clave:

* Arquitectura cloud
* Networking
* Seguridad
* Compute
* Bases de datos (IaaS y PaaS)
* Almacenamiento
* Integración de aplicaciones

---

## 🎯 Objetivos del Proyecto

El objetivo principal es construir una arquitectura funcional que simule un entorno real de producción, permitiendo:

* Comprender la segmentación de redes (subnets públicas y privadas)
* Implementar control de acceso mediante IAM
* Desplegar aplicaciones en instancias de cómputo
* Integrar almacenamiento y bases de datos
* Aplicar principios de seguridad en capas
* Comparar modelos IaaS vs PaaS

---

## 🧠 Enfoque de aprendizaje

Este laboratorio está diseñado bajo el principio de:

> "Aprender haciendo, pero entendiendo el porqué de cada decisión."

Cada componente ha sido configurado siguiendo:

* Buenas prácticas de arquitectura cloud
* Principios de seguridad (least privilege, aislamiento de red)
* Patrones utilizados en entornos empresariales

---

## 🏗️ Tipo de arquitectura

Se implementa una arquitectura tipo **3-tier**:

```text
Internet
   │
   ▼
Load Balancer (capa pública)
   │
   ▼
Application Layer (web-vm en subnet privada)
   │
   ▼
Data Layer (bases de datos)
```

Incluyendo un modelo híbrido:

* Base de datos autogestionada (PostgreSQL en VM)
* Base de datos gestionada (Autonomous Database)

---

## ☁️ Equivalencia en otros proveedores cloud

| OCI              | AWS          | Azure           | GCP                 |
| ---------------- | ------------ | --------------- | ------------------- |
| VCN              | VPC          | Virtual Network | VPC                 |
| Compute Instance | EC2          | Virtual Machine | Compute Engine      |
| Load Balancer    | ELB          | Azure LB        | Cloud Load Balancer |
| Object Storage   | S3           | Blob Storage    | Cloud Storage       |
| Autonomous DB    | RDS / Aurora | Azure SQL       | Cloud SQL           |

---

## 🚀 Alcance

Este laboratorio utiliza principalmente recursos del nivel **Always Free**, lo que permite:

* Aprender sin costo
* Simular arquitecturas reales
* Iterar y experimentar sin riesgo

---

## 👤 Público objetivo

Este proyecto está dirigido a:

* Ingenieros IT en transición a Cloud
* DevOps junior/intermedio
* Estudiantes de cloud computing
* Profesionales que buscan construir un portfolio técnico
---
