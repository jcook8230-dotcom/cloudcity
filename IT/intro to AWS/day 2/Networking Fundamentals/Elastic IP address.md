An  **Elastic IP address (EIP)** is ==a reserved, **static, public IPv4 address** designed for dynamic cloud computing==. Unlike standard public IP addresses, which are temporary and automatically change whenever an EC2 instance is stopped, rebooted, or terminated, an Elastic IP is permanently allocated to your AWS account until you explicitly release it.

It acts as a fixed, unchanging front-door address for your public-facing cloud resources.

---

Core Operational Principles

- **Decoupled Architecture:** An Elastic IP is not bound to a specific virtual machine. You can rapidly mask the failure of an instance or software stack by **reassociating** the Elastic IP address with a completely different instance in your VPC within seconds.
- **One-to-One NAT:** The Elastic IP maps directly to the private IPv4 address of your instance through the VPC's Internet Gateway. The instance itself remains unaware of its public IP address; the translation is handled entirely by the AWS network layer.
- **Region-Locked:** Elastic IPs are bound to a specific AWS Region and cannot be moved or transferred to resources in a different region.

---

Common Use Cases

Elastic IPs are primarily utilized when external clients or systems require a predictable, hardcoded network endpoint:

- **NAT Gateways:** A managed AWS NAT Gateway requires a static, unchanging public IP address to securely funnel outbound traffic from private subnets out to the open web.
- **White-listed API Integrations:** When your application needs to talk to a third-party corporate API that requires you to provide a strict, unchanging IP address for firewall white-listing.
- **Legacy DNS Routing:** Useful if you are managing custom domain records on older domain registrars that do not support dynamic load balancer aliases (ALB DNS names) and require a static A-record (IP address).

---

Elastic IP vs. Standard Public IP

|Attribute|Elastic IP Address (EIP)|Standard Public IP Address|
|---|---|---|
|**Lifecycle**|Remains with your account until manually released.|Lost whenever the instance is **stopped** or terminated.|
|**Portability**|Can be detached from one instance and moved to another.|Permanently locked to that specific instance lifecycle.|
|**AWS Charge**|Billed by the hour when active or idle.|Minimal baseline hourly charge while running.|

---

The AWS "Idle" Penalty & Allocation Limits

To prevent the hoarding of scarce public IPv4 addresses, AWS implements strict optimization and billing rules:

1. **Standard Baseline Cost:** AWS charges a flat, small hourly fee for _every_ public IPv4 address used across the platform.
2. **The Idle Penalty:** If you allocate an Elastic IP to your account but leave it unassociated, or attach it to a stopped instance/unattached network interface, AWS continues to bill you to encourage you to release the unused address back to the public pool.
3. **Account Limits:** By default, AWS limits all accounts to a maximum of **5 Elastic IP addresses per region** to prevent accidental over-allocation. If your architecture demands more, you must explicitly submit a service quota increase request through the AWS console.