**AWS Outposts** is ==a fully managed service that extends native AWS infrastructure, APIs, and management tools directly into your on-premises data center, co-location space, or local facility==. It allows you to run compute and storage locally for low-latency applications while maintaining a consistent hybrid experience with the public AWS cloud. [[1](https://aws.amazon.com/outposts/)]

---

Core Attributes & Structure

| Feature / Attribute | Specification                   | Description                                                                                   |
| ------------------- | ------------------------------- | --------------------------------------------------------------------------------------------- |
| **Form Factors**    | **42U Racks & 1U/2U Servers**   | Industry-standard racks for data centers or compact servers for space-constrained edge sites. |
| **Pricing Model**   | **3-Year/1-Year Subscription**  | Billed via capacity commitments (compute and storage tiers) rather than per-request usage.    |
| **Local Services**  | **EC2, EBS, S3, RDS, ECS, EKS** | Native AWS services run physically on-prem while linking back to a parent Region.             |
| **Management**      | **Remote AWS Control Plane**    | AWS automatically handles underlying hardware maintenance, firmware updates, and patching.    |

---

How AWS Outposts Operates

- **VPC Extension:** You stretch your existing [Amazon Virtual Private Cloud (VPC)](https://aws.amazon.com/vpc/) on-premises by creating a dedicated subnet mapped explicitly to your Outpost hardware. [[1](https://aws.amazon.com/blogs/compute/running-aws-infrastructure-on-premises-with-aws-outposts/)]
- **Local Gateway (LGW):** Acts as a virtual router that connects workloads running on your Outpost directly to your local corporate network or data sources without needing to transit the public internet. [[1](https://docs.aws.amazon.com/outposts/latest/userguide/what-is-outposts.html)]
- **The Service Link:** A secure, encrypted network connection that ties your on-premises hardware back to the parent AWS Region for telemetry, API management, and optional data synchronization. [[1](https://docs.aws.amazon.com/outposts/latest/userguide/what-is-outposts.html)]