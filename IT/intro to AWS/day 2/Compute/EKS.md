**Amazon EKS** (==Elastic Kubernetes Service==) is a managed service that makes it easy to run **open-source Kubernetes** on AWS without needing to install, operate, and maintain your own Kubernetes control plane. It provides a production-ready, highly available architecture across multiple Availability Zones, ensuring full compatibility with standard upstream Kubernetes tooling and plugins.

---

Core Structural Architecture

Kubernetes separates infrastructure into a brain (Control Plane) and a workforce (Worker Nodes). EKS natively manages both halves with flexible configurations:

1. The Managed Control Plane

AWS completely takes over the complex task of running the Kubernetes control plane.

- **High Availability:** EKS automatically runs and scales the API server and `etcd` database across three physical Availability Zones within a region.
- **Self-Healing:** If a master node crashes, EKS automatically detects, terminates, and replaces it with zero downtime.

2. Worker Node Infrastructure

You choose how to back your cluster with compute capacity using three primary node strategies:

- **Managed Node Groups:** AWS automates the provisioning, creation, configuration, and rolling updates of Amazon EC2 instances acting as worker nodes.
- **AWS Fargate (Serverless Nodes):** Eliminates EC2 completely. Every time you deploy a Kubernetes Pod, Fargate spins up an isolated, right-sized serverless compute boundary for it. You pay strictly for the vCPU and memory consumed by the pod.
- **Self-Managed Nodes:** You manually provision custom EC2 instances and register them into the cluster. This is best for complex, highly specific hardware or OS modifications.

---

Core Kubernetes vs. EKS Construct Mapping

To help transition from raw Kubernetes concepts to EKS, here is how core components align with AWS infrastructure:

|Kubernetes Concept|EKS Implementation|Purpose|
|---|---|---|
|**Pod**|Container Running on EC2 / Fargate|The smallest deployable unit of a container.|
|**Ingress Controller**|AWS Load Balancer Controller (ALB)|Routes external internet traffic directly to pods.|
|**Persistent Volume**|Amazon EBS / Amazon EFS|Persistent storage that remains intact if a pod dies.|
|**K8s ServiceAccount**|IAM Roles for Service Accounts (IRSA)|Assigns distinct AWS permissions directly to a single pod.|

---

Key Operational Advantages of EKS

- **Native IAM Security Integration:** Through IAM Roles for Service Accounts (IRSA), you can tie an AWS IAM policy directly to a Kubernetes pod. For example, your "payment pod" can be granted access to a secure database, while a "logging pod" right next to it on the same node is structurally blocked.
- **Seamless Hybrid Cloud (EKS Anywhere):** Allows you to use the exact same EKS management software, dashboards, and tooling to run Kubernetes clusters inside your own on-premises bare-metal hardware or VMware environments.
- **VPC Native Networking:** EKS utilizes the Amazon VPC CNI plugin. This means every individual pod deployed in your cluster receives a real, native IP address directly from your AWS Virtual Private Cloud (VPC), allowing for ultra-fast networking and standard security group filtering.