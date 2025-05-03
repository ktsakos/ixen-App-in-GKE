
# **iXen: Secure IoT Platform on Kubernetes**

## **Overview**

**iXen** aims to overcome the limitations of existing IoT platforms in the cloud by addressing **security** and **interoperability** challenges.  
It is:

- **Interoperable and expandable** – services can be added or removed.
- **Secure by design** – access is granted only to authorized users or services based on roles and policies.

Built on **Service-Oriented Architecture (SOA)** principles and aligned with **EU standards** for context information management, iXen is implemented as a composition of **RESTful microservices** deployed in the cloud.

---

## **Architecture**

iXen adopts a **3-tier architecture**:

1. **Device Layer**
   - Connects a wide variety of IoT devices to the cloud.

2. **Middle Layer**
   - Manages **IoT data functionality** such as:
     - Database services
     - Security
     - Context management
   - Enables:
     - Devices to publish information
     - Users/services to subscribe and receive updates
     - **Flow-based programming** for rapid app development

3. **Application Layer**
   - Provides IoT applications to customers via **subscription models**

> **Performance Note**: Experimental analysis shows that iXen responds in **real-time** to complex service requests under **heavy workloads**.

---

## **Reference**

> Euripides G.M. Petrakis, Xenofon Koundourakis,  
> *"iXen: Secure Service Oriented Architecture and Context Information Management in Cloud"*,  
> International Journal of Ubiquitous Systems and Pervasive Networks (JUSPN), Vol. 14, No. 2, pp. 1–10, January 2021.
> [Read the full paper (PDF)](https://www.intelligence.tuc.gr/~petrakis/publications/JUSPN2020.pdf)

---

## **MSc Thesis Context**

In the context of my MSc thesis (**[TEXT LINK TO BE ADDED HERE]**), iXen was **converted into a microservice-based application**.

---

## **Repository Contents**

This repository contains:

- All **Kubernetes manifests** required for deploying iXen in a cluster using `kubectl`.
- The **source code** to be stored on the **NFS server** and mounted via Persistent Volumes.

### **Subfolder Structure**

Each subfolder includes the necessary YAML templates:

- `StatefulSets`
- `Deployments`
- `Secrets`
- `PVCs` / `PVs`

If a **PEP Proxy** is required (as described in the iXen architecture), additional YAML files are included in a dedicated subfolder for each corresponding microservice.

---

## **Deployment Instructions**

To deploy iXen:

1. Ensure your Kubernetes cluster is set up.
2. Apply all YAML templates **in order**, using:
   ```bash
   kubectl apply -f <filename>.yaml
   ```

> ⚠️ **Important**:  
> For the **Orion** service, apply the **Deployment** YAML **before** the **Service** YAML due to a known bug.

---

## **Code Configuration (PHP)**

In the `code/` folder (PHP):

- Edit:
  - `redirect.php`
  - `Mysubscription.php`
- Update the **NodePort** and **Node IP** of the **Apache service**, as it may change with each pod deployment.

**Tip**: Review the PHP code to understand how REST API calls are structured within the application workflows.

---

## **GCP Deployment Notes**

If using **Google Cloud Platform (GKE)**:

- **Avoid using LoadBalancer services** to reduce costs.
- Instead, use **NodePort services** for externally accessible microservices.
- Configure **GCP port forwarding rules** appropriately to route external traffic.

---

## **Known Issues & Tips**

- 🐞 **Orion Service Bug**: Deployment YAML must be applied before its Service YAML.
- 🔐 **Secrets**:
  - Use **Base64-encoded** values by default.
  - Optionally, **plain text** secrets are supported.
