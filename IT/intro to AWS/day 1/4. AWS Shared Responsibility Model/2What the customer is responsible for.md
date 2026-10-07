==**The customer is responsible for "security _in_ the cloud,"**== which means you own the configuration, protection, and management of everything you put into or build on top of AWS.

Under the [AWS Shared Responsibility Model](https://aws.amazon.com/compliance/shared-responsibility-model/), while AWS secures the hardware and underlying facilities, the customer must secure their data, operating systems, network settings, and user access permissions.

Core Areas of Customer Responsibility

- **Customer Data:** Classifying, backing up, and protecting your data, including deciding who can view it and applying proper encryption settings.
- **Operating Systems and Patching:** Updating the guest operating system, application runtimes, and third-party software installed on virtual machines like [Amazon EC2](https://aws.amazon.com/ec2/).
- **Network Configurations:** Setting up virtual private cloud (VPC) subnets, routing tables, and configuring security groups or firewalls to block unauthorized network traffic.
- **Identity and Access Management (IAM):** Creating user accounts, enforcing strong passwords, requiring multi-factor authentication (MFA), and granting the lowest necessary access permissions.
- **Application Code:** Writing secure application logic, fixing code vulnerabilities, and managing configurations for the software your business runs.
- **Encryption Keys:** Managing and rotating encryption keys using tools like [AWS KMS](https://aws.amazon.com/kms/) to ensure data remains private.

How Responsibility Shifts by Service Type

|Cloud Model|What AWS Manages|What You (The Customer) Manage|
|---|---|---|
|**IaaS (e.g., EC2)**|Physical hardware, virtualization layer, data center security.|Operating system updates, middleware, runtime environments, and application data.|
|**PaaS / Managed (e.g., RDS)**|Hardware, OS patching, database engine installation.|Database schema design, user table data, and access permissions.|
|**SaaS / Serverless (e.g., Lambda)**|Infrastructure, scaling, runtime maintenance, and system patches.|Application source code, function triggers, and data encryption.|