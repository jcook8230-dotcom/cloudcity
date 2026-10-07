**AWS Database Migration Service (AWS DMS)** is ==a managed cloud service that allows you to move and replicate relational databases, data warehouses, and NoSQL data stores to AWS or between external and on-premises environments with minimal downtime==. It keeps your source database fully operational during the data transfer process by streaming live changes continuously until you are ready to cut over. [[1](https://aws.amazon.com/dms/faqs/), [2](https://www.geeksforgeeks.org/devops/aws-database-migration-service/), [3](https://docs.aws.amazon.com/dms/latest/userguide/Welcome.html), [4](https://aws.amazon.com/compare/database-migration-service-dms-and-migration-hub/)]

---

Core Deployment & Pricing Models

|Option / Deployment|Pricing Basis|Best Used For|
|---|---|---|
|**On-Demand Replication Instance**|Pay-as-you-go hourly rate (e.g., `dms.t3.micro` at **$0.0186/hr**, `dms.r5.large` at **$0.176/hr**)|Predictable, steady-state multi-terabyte data transfers|
|**AWS DMS Serverless**|Pay-per-use capacity rate (~**$0.082 per DCU-hour**)|Complex heterogeneous workloads with variable, auto-scaling traffic|
|**Homogeneous Migrations**|Pay-per-use hourly rate for active migration time only|Moving between identical database engines (e.g., MySQL to Aurora)|

_Note: Data transfer into AWS DMS is free, and standard internal transfers between DMS and Amazon RDS/EC2 within the same Availability Zone carry no extra charge._ [[1](https://aws.amazon.com/dms/pricing/)]

---

How AWS DMS Operates

- **Full Load & Change Data Capture (CDC):** Supports full initial data loads, ongoing data replication via CDC to keep source and target completely synchronized, or a combination of both. [[1](https://aws.amazon.com/documentation-overview/dms/), [2](https://perfsys.com/blog/aws-dms-complete-guide/)]
- **Homogeneous vs. Heterogeneous Migrations:**
    
    - _Homogeneous_ moves data between matching engine types (e.g., Oracle to Oracle) with minimal configuration.
    - _Heterogeneous_ involves shifting to different target engines (e.g., Oracle to PostgreSQL). This requires a two-step process using **DMS Schema Conversion (DMS SC)** or the downloadable [AWS Schema Conversion Tool (AWS SCT)](https://aws.amazon.com/dms/) to first translate object types and code before DMS moves the actual data. [[1](https://www.geeksforgeeks.org/devops/aws-database-migration-service/), [2](https://aws.amazon.com/dms/faqs/), [3](https://aws.amazon.com/documentation-overview/dms/), [4](https://perfsys.com/blog/aws-dms-complete-guide/)]
    
- **Resilience & Self-Healing:** Continuously monitors connection health and replication logs, automatically restarting interrupted tasks or failing over to redundant infrastructure in Multi-AZ deployments. [[1](https://aws.amazon.com/dms/features/)]

---

Security and Ecosystem Integration

AWS DMS protects data in transit using SSL/TLS encryption and integrates natively with [AWS IAM](https://aws.amazon.com/iam/) for strict permission scoping, [AWS KMS](https://aws.amazon.com/kms/) for encryption key governance, and [AWS Secrets Manager](https://aws.amazon.com/systems-manager/) for automated source and target credential handling. For complete technical documentation, see the official [AWS Database Migration Service Guide](https://docs.aws.amazon.com/dms/). [[1](https://aws.amazon.com/dms/), [2](https://aws.amazon.com/dms/features/)]