**AWS Wavelength** is ==an edge computing infrastructure service that embeds AWS compute and storage capabilities directly into the data centers of telecommunication providers at the edge of **5G networks**==. By doing so, it allows mobile and connected device traffic to reach application backends in single-digit milliseconds without traversing multiple hops across the public internet. [[1](https://n2ws.com/blog/aws-wavelength-ultra-low-latency-solution), [2](https://www.youtube.com/watch?v=EhMqwPqPzcY&t=34)]

---

Core Components & Pricing Model

|Component / Metric|Details|Pricing / Access Model|
|---|---|---|
|**Wavelength Zone**|Logical extension of a parent AWS Region hosted inside a 5G carrier data center|On-demand EC2 and EBS pricing (typically ~25–50% higher than parent region rates)|
|**Carrier Gateway**|Specialized gateway routing traffic between mobile devices and the Wavelength Zone|No extra gateway hourly fee; standard data transfer rates apply|
|**Carrier IP Address**|Local IP assigned directly from the mobile network provider pool|Allocated via your account's Network Border Group|
|**Supported Compute**|Amazon EC2 instances, Amazon EBS volumes, Amazon ECS, and Amazon EKS|Hourly pay-as-you-go or applicable instance savings plans|

---

How AWS Wavelength Operates

- **VPC Extension:** You stretch your existing [Amazon Virtual Private Cloud (VPC)](https://aws.amazon.com/vpc/) from a parent AWS Region into one or more designated Wavelength Zones by provisioning a specialized Wavelength subnet. [[1](https://docs.aws.amazon.com/whitepapers/latest/overview-deployment-options/wavelength.html), [2](https://www.geeksforgeeks.org/devops/what-is-aws-wavelength/)]
- **Local Carrier Routing:** Instead of routing traffic through an Internet Gateway, mobile device traffic hits the carrier's cell tower and is routed straight through a **Carrier Gateway** directly into your edge-hosted EC2 instances. [[1](https://www.geeksforgeeks.org/devops/what-is-aws-wavelength/), [2](https://www.youtube.com/watch?v=_UHNoxoyv6A&t=462)]
- **Regional Interconnectivity:** While high-performance processing happens locally at the 5G edge, your instances maintain a high-bandwidth, secure connection back to the parent AWS Region to query regional services like Amazon DynamoDB or [Amazon RDS](https://aws.amazon.com/rds/). [[1](https://docs.aws.amazon.com/whitepapers/latest/overview-deployment-options/wavelength.html), [2](https://www.geeksforgeeks.org/devops/what-is-aws-wavelength/)]

---

Key Global Partners & Use Cases

AWS partners with major telecom providers globally—including **Verizon** in the U.S., **Vodafone** in Europe, **KDDI** in Japan, and **Bell** in Canada—spanning over 30 cities worldwide. It powers high-performance applications such as: [[1](https://aws.amazon.com/wavelength/locations/), [2](https://aws.amazon.com/wavelength/customers/)]

- **Real-Time Gaming & AR/VR:** Eliminating input lag for cloud-streamed gaming and immersive visual rendering.
- **Autonomous Vehicles & Robotics:** Providing low-latency sensor telemetry and remote supervision for automated delivery droids and connected cars.
- **Smart Factories:** Executing near-instant machine learning inference for real-time assembly line quality inspections. [[1](https://www.verizon.com/business/products/5g/edge-computing/aws-wavelength-5g/), [2](https://aws.amazon.com/blogs/industries/verizon-evolves-its-5g-network-and-accelerates-its-speed-and-reach-powered-by-aws/), [3](https://aws.amazon.com/wavelength/customers/), [4](https://aws.amazon.com/wavelength/resources/), [5](https://n2ws.com/blog/aws-wavelength-ultra-low-latency-solution)]