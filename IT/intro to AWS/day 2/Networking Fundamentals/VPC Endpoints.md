**Amazon VPC Endpoints** ==enable you to privately connect your Virtual Private Cloud (VPC) to supported AWS services and VPC endpoint services powered by **AWS PrivateLink**==.

Before VPC Endpoints, if an EC2 instance in a private subnet needed to securely read data from an Amazon S3 bucket or send a log message to Amazon CloudWatch, the traffic had to travel out through a NAT Gateway and across the public internet to reach the public AWS service endpoint.

A VPC Endpoint completely removes the internet from the equation. It acts as a private door within your network, keeping all traffic **entirely within the private AWS network backbone**.

---

The 2 Primary Types of VPC Endpoints

AWS provides two distinct architectural variations of endpoints, depending on the service you are trying to reach:

1. Interface Endpoints (Powered by AWS PrivateLink)

An Interface Endpoint provisions an **Elastic Network Interface (ENI)** with a private IP address directly inside your specified subnet.

- **How it works:** It uses a private IP address allocated out of your subnet's CIDR block. Any traffic sent to that service is directed straight to that local network interface.
- **Cost Structure:** You pay a small hourly fee for keeping the interface active, plus a per-gigabyte data processing charge.
- **Supported Services:** Most AWS services (e.g., Amazon EC2 APIs, Systems Manager, CloudWatch, Kinesis, SNS, SQS).

2. Gateway Endpoints

A Gateway Endpoint is a logical target that you add directly to your **VPC Route Tables**. It does not use private IPs or network interfaces inside your subnet.

- **How it works:** You point internet-bound traffic destined for specific services straight to the gateway object (e.g., `vpce-xxxxxx`).
- **Cost Structure:** **Completely free of charge.** There are no hourly fees or data processing costs.
- **Supported Services:** Restricted strictly to **Amazon S3** and **Amazon DynamoDB**.

---

Architectural Traffic Flow Compared

```
[ Traditional Method (Public Network) ]
[ Private EC2 Instance ] ──> [ NAT Gateway ] ──> [ Internet Gateway ] ──> [ Public Internet ] ──> [ Amazon S3 ]

[ Endpoint Method (Private Network Backbone) ]
[ Private EC2 Instance ] ──(Via Route Table or Local ENI)──> [ VPC Endpoint ] ──> [ Amazon S3 / CloudWatch ]
```

---

Key Structural Differences

|Feature|Interface Endpoints|Gateway Endpoints|
|---|---|---|
|**AWS Technology**|Powered by AWS PrivateLink|Logical Gateway Route Target|
|**VPC Infrastructure**|Creates a physical **ENI with Private IP** inside your subnet|Modifies your **Route Table** rules directly|
|**Cost**|Hourly fee + Data processing charges apply|**100% Free**|
|**On-Premises Access**|Can be accessed over AWS Direct Connect or VPN|Cannot be accessed directly via VPN/Direct Connect|
|**Supported Services**|Over 100+ AWS services, Marketplace apps, custom services|**Amazon S3** and **Amazon DynamoDB** only|

---

Security and Endpoint Policies

VPC Endpoints don't just secure your network routing; they also drastically tighten your data governance. You can attach a **VPC Endpoint Policy** (written as a standard IAM JSON policy document) directly to the endpoint. This allows you to restrict traffic at the network boundary. For example, you can write an endpoint policy that states:

- _"Instances using this S3 Endpoint are **only** allowed to read from corporate bucket `my-company-data`."_
- _"Any attempts to exfiltrate data to a personal or external AWS S3 bucket through this endpoint are completely blocked."_