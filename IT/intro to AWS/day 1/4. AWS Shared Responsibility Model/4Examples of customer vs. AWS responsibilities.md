Under the **AWS Shared Responsibility Model**, dividing operational tasks into clear examples helps teams avoid costly security gaps or configuration overlaps.

Here are the concrete **examples of customer vs. AWS responsibilities** across different cloud deployments:

Scenario 1: Running Virtual Machines ([Amazon EC2](https://aws.amazon.com/ec2/))

This is an **Infrastructure as a Service (IaaS)** setup, where the customer maintains maximum control over the environment.

- **AWS is responsible for:** Replacing a physical memory stick in the server rack if it fails; protecting the server building against physical break-ins; securing the hypervisor software that carves the physical host into separate virtual instances.
- **The Customer is responsible for:** Upgrading the guest operating system (e.g., patching Linux or Windows Server); configuring the EC2 **Security Group** (firewall) to block malicious external IP addresses; managing administrative passwords inside the virtual machine.

Scenario 2: Storing Object Data ([Amazon S3](https://aws.amazon.com/s3/))

This is a **managed storage platform** where AWS completely abstracts away the operating system and file systems.

- **AWS is responsible for:** Replicating data across multiple data centers to guarantee **99.999999999% durability**; managing physical hard drive destruction and recycling; updating storage firmware.
- **The Customer is responsible for:** Toggling the bucket settings to **Block Public Access** to prevent data leaks; enabling **Server-Side Encryption** (SSE) via [AWS KMS](https://aws.amazon.com/kms/); managing bucket access policies for internal team members.

Scenario 3: Running a Relational Database ([Amazon RDS](https://aws.amazon.com/rds/))

This is a **Platform as a Service (PaaS)** setup, where AWS handles the overhead of database engine maintenance.

- **AWS is responsible for:** Automating the installation of database engine patches (e.g., PostgreSQL or MySQL updates); executing automated baseline snapshots; provisioning underlying storage disks.
- **The Customer is responsible for:** Creating user tables, schemas, and columns; configuring database user permissions and access strings; optimizing slow SQL queries.

Summary Matrix of Shared Responsibilities

| Technical Element           | Who is Responsible? | Concrete Real-World Example                                                                    |
| --------------------------- | ------------------- | ---------------------------------------------------------------------------------------------- |
| **Physical Facilities**     | 🏢 **AWS**          | Managing cooling systems, backup power grids, and security guards at the data center.          |
| **Identity & Access (IAM)** | 🔑 **Customer**     | Enforcing **Multi-Factor Authentication (MFA)** on all corporate cloud administrator accounts. |
| **Network Perimeter**       | 🌐 **Customer**     | Defining VPC subnets and routing traffic through Internet Gateways safely.                     |
| **Hardware Disposal**       | 💿 **AWS**          | Securely wiping and destroying decommissioned storage disks to prevent data recovery.          |
| **Application Layer**       | 💻 **Customer**     | Writing secure code that prevents SQL injection attacks or application bugs.                   |