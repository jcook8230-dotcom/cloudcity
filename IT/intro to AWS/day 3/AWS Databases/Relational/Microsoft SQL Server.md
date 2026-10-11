**Microsoft SQL Server** is ==an enterprise-grade relational database management system (RDBMS) widely utilized for transaction processing, business intelligence, and data analytics==. On AWS, you can deploy SQL Server across several managed and unmanaged structural layouts while navigating licensing compliance and high-availability frameworks.

---

Three Core Deployment Models on AWS

AWS provides distinct methods for hosting SQL Server based on your preferred balance of administrative control and automated operations:

1. Amazon RDS for SQL Server (Fully Managed)

The standard fully managed path [Amazon RDS]. AWS handles the entire infrastructure lifecycle—including server provisioning, storage allocation, OS security patches, and automated daily backups [Amazon RDS, Oracle].

- **Scale and Performance:** Supports provisioning up to **64 TiB of block storage** using high-speed Amazon EBS SSD volumes (gp3 or io2), scaling up to **256,000 Provisioned IOPS** for heavy production workloads [Oracle].
- **High Availability:** Utilizes **SQL Server Database Mirroring** or **Always On Availability Groups** natively under the hood to automatically replicate data synchronously across multiple physical Availability Zones [Amazon RDS, Oracle].

2. SQL Server on AWS Outposts (Hybrid Cloud)

Enables you to run fully managed Amazon RDS for SQL Server directly on your own **on-premises hardware** [AWS Compute]. AWS ships physical hardware racks straight to your data center, allowing you to run local SQL Server databases with identical cloud APIs while meeting strict local data residency or ultra-low latency requirements [AWS Compute].

3. Self-Managed SQL Server on Amazon EC2

Deploying the SQL Server binaries directly onto a raw Windows Server or Linux EC2 virtual machine [MySQL, Oracle]. This gives database administrators absolute access to the underlying operating system and system files (`sysadmin` rights), but forces your team to manually design, run, and audit high availability, backups, and licensing compliance [PostgreSQL, Oracle].

---

The Two Licensing Paths

Because Microsoft SQL Server is proprietary enterprise software, deploying it on AWS requires selecting a strict licensing model:

- **License Included (LI):** You do not buy a software license ahead of time [Oracle]. Instead, AWS rents the SQL Server software license directly to you by bundling it into your standard hourly compute charge [Oracle]. This is available for standard editions (Web, Express, Standard, and Enterprise) and avoids long-term contract lock-ins.
- **Bring Your Own License (BYOL):** If your organization already owns perpetual SQL Server licenses with Microsoft Software Assurance, you can migrate them directly to AWS. This approach is typically executed on **Amazon EC2 Dedicated Hosts** or Dedicated Instances to satisfy Microsoft's physical core licensing tracking requirements.

---

Architectural Design Comparison

|Feature|Amazon RDS for SQL Server|Self-Managed on Amazon EC2|
|---|---|---|
|**Operating System**|Managed automatically by AWS (Windows-backed).|Choice of **Windows Server** or **Linux** (Ubuntu, RHEL).|
|**Administrative Access**|Restricted via console/API; no direct OS or host access.|**Full administrator / root access** to the OS filesystem [Oracle].|
|**High Availability**|**Multi-AZ synchronous replication** (turnkey checkbox) [Amazon RDS, Oracle].|Manually configured **Always On Availability Groups** across instances [PostgreSQL, Oracle].|
|**Custom Agent Jobs**|Supported natively via standard SQL Server Agent APIs.|Supported with full control over custom subsystem scripts.|

---

Key Enterprise Migration and Integration Features

- **Native Backup/Restore:** Amazon RDS for SQL Server supports native `.bak` file backups. You can take an on-premises database backup file, upload it securely to an **Amazon S3 bucket**, and trigger an RDS stored procedure to restore it directly into the cloud [Buckets].
- **Active Directory Integration:** Connects seamlessly with **AWS Directory Service** or your on-premises Microsoft Active Directory, allowing database users to authenticate securely using standard Windows Authentication single sign-on (SSO) credentials.