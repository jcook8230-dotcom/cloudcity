An **Internet Gateway (IGW)** is ==a horizontally scaled, redundant, and highly available VPC component that allows communication between resources in your VPC and the public internet==. It imposes no availability risks or bandwidth constraints on your network traffic.

An Internet Gateway serves two primary purposes: to provide a target in your VPC route tables for internet-bound traffic, and to perform network address translation (NAT) for instances that have been assigned public IPv4 addresses.

---

Key Operational Characteristics

- **Two-Way Traffic:** Unlike a NAT Gateway which only permits one-way outbound traffic, an Internet Gateway supports both **inbound and outbound traffic flows**. This makes it essential for hosting public-facing websites or APIs.
- **1:1 NAT Mapping:** When an EC2 instance in a public subnet sends traffic to the internet, the Internet Gateway translates its private IP address to its public or Elastic IP address, managing the return mapping seamlessly.
- **Decoupled Lifecycle:** An Internet Gateway is created independently of a VPC. It must be explicitly **attached** to a specific VPC to function, and a VPC can only have **one** Internet Gateway attached at a time.
- **Completely Serverless:** You do not manage instances or allocate bandwidth for an IGW. It scales automatically to handle your network's throughput without any configuration tuning.

---

How an Internet Gateway Forms a Public Subnet

An Internet Gateway is the defining mechanism that transforms a standard subnet into a public subnet. Without an explicit path pointing to it, resources remain entirely isolated.

```
┌───────────────────────────────── Virtual Private Cloud (VPC) ─────────────────────────────────┐
│                                                                                               │
│   [ Public Subnet ] ──(Route Table: 0.0.0.0/0)──> [ Internet Gateway ] <──> [ Public Internet ]  │
│                                                                                               │
└───────────────────────────────────────────────────────────────────────────────────────────────┘
```

To establish this path, you configure a **Route Table** attached to your subnet with the following default route:

|Destination|Target|Description|
|---|---|---|
|`10.0.0.0/16`|`local`|Handles internal VPC traffic within your private network block.|
|**`0.0.0.0/0`**|**`igw-xxxxxx`**|Forwards all traffic bound for the public internet directly to the Internet Gateway.|

---

Common Alternatives & Complements

- **NAT Gateway:** Used when instances in a _private_ subnet need to access the internet (e.g., for software patches) but must block the public internet from initiating a connection with them. The NAT Gateway itself sits in a public subnet and routes through the IGW.
- **VPC Endpoints:** Used when your instances need to talk to other AWS services (like Amazon S3 or DynamoDB) without routing traffic through an Internet Gateway or exposing data to the public internet.