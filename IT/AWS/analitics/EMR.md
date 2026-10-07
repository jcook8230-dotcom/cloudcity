**Amazon EMR (Elastic MapReduce)** is ==a cloud-native **big data platform** designed to process vast amounts of data using open-source, distributed frameworks like **Apache Spark**, Hive, Presto, and HBase==. It detaches compute from storage, allowing you to dynamically scale clusters up or down to handle petabyte-scale data engineering, machine learning, and data analytics workloads.

---

Core Deployment Options & Pricing

|Deployment Option|Pricing Structure|Best Used For|
|---|---|---|
|**EMR on EC2**|Amazon EMR fee (**$0.015 to $0.27/hr** per instance) + standard [Amazon EC2](https://aws.amazon.com/ec2/) and [Amazon EBS](https://aws.amazon.com/ebs/) charges|Custom cluster sizing, fine-grained infrastructure tuning, and cost-effective Spot Instance fleets.|
|**EMR on EKS**|Amazon EMR fee (**$0.015/hr** per vCPU) + standard [Amazon EKS](https://aws.amazon.com/eks/) compute infrastructure costs|Teams already standardized on container orchestration who want to share Kubernetes clusters.|
|**EMR Serverless**|Pay-as-you-go capacity based on actual resources consumed (**vCPU, memory, and storage per hour**)|Variable, unpredictable, or automated pipelines where you want zero cluster management.|

---

How Amazon EMR Operates

- **Decoupled Architecture:** Instead of storing data directly inside the compute instances, EMR natively reads and writes data directly to [Amazon Simple Storage Service (Amazon S3)](https://aws.amazon.com/s3/) using the optimized EMR File System (EMRFS), or to the Amazon EBS volumes attached to cluster nodes.
- **Node Types (on EC2):**
    - _Primary Node:_ Coordinates the cluster, tracks application health, and manages the distributed file system metadata.
    - _Core Nodes:_ Run tasks and store HDFS data directly on their attached storage drives.
    - _Task Nodes:_ Provide pure compute capacity to execute tasks without storing persistent distributed file data, making them ideal for aggressive scaling using **Amazon EC2 Spot Instances**.
- **Instance Fleets:** Simplifies capacity sourcing by letting you specify a target capacity and provision a blend of Spot and On-Demand instances across various instance types and Availability Zones.
- **Studio Environment:** Provides a unified web-based interface (EMR Studio) based on Jupyter Notebooks, allowing data scientists to build, debug, and run analytical code collaboratively without accessing the AWS Management Console.

---

Ecosystem Integration

Amazon EMR hooks directly into the **AWS Glue Data Catalog** for unified metadata management, integrates with **AWS IAM Identity Center** for fine-grained user authentication, and streams auditing footprints to [AWS CloudTrail](https://aws.amazon.com/cloudtrail/) to maintain enterprise security alignment.