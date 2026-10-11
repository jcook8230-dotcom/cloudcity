**Elastic Load Balancing (ELB)** ==automatically distributes incoming application traffic across multiple targets==—such as Amazon EC2 instances, containers, IP addresses, and AWS Lambda functions—within one or more Availability Zones.

By acting as the single point of entry for your application, ELB ensures **high availability, fault tolerance, and seamless scalability**. If an underlying server fails, the load balancer detects the failure, stops routing traffic to that specific target, and redistributes the load to the remaining healthy servers.

---

The 4 Types of AWS Load Balancers

AWS offers four specialized load balancers designed for different architectural layers and protocols:

1. Application Load Balancer (ALB)

Operates at the **Application Layer (Layer 7)** of the OSI model. It inspects the actual content of HTTP/HTTPS requests to make advanced routing decisions.

- **Key Capabilities:** Supports **path-based routing** (e.g., sending `/api` requests to one fleet of servers and `/images` to another) and **host-based routing** (e.g., routing `://example.com` vs `://example.com`).
- **Best Use Cases:** Modern web applications, microservices architectures, and containerized deployments (integrated with Amazon ECS or EKS).

2. Network Load Balancer (NLB)

Operates at the **Transport Layer (Layer 4)**, handling raw TCP, UDP, and TLS traffic. It is engineered for extreme performance and ultra-low latency.

- **Key Capabilities:** Capable of handling **millions of requests per second** while maintaining volatile, sub-millisecond latencies. It also provides a **static IP address** per Availability Zone and can attach an Elastic IP.
- **Best Use Cases:** High-frequency trading platforms, gaming servers, IoT data ingestion pipelines, and architectures requiring raw socket connections.

3. Gateway Load Balancer (GWLB)

Operates at **Layer 3 (Network Layer)** and Layer 4. It helps you deploy, scale, and manage third-party virtual appliances.

- **Key Capabilities:** Acts as a transparent bump-in-the-wire gateway that intercepts all traffic and funnels it through a pool of firewalls, intrusion detection systems (IDS), or deep packet inspection appliances.
- **Best Use Cases:** Centralized network security logging, enterprise inline inspection, and custom virtual firewall fleets.

4. Classic Load Balancer (CLB)

The legacy load balancer operating across both Layer 4 and Layer 7. _Note: CLB is heavily deprecated and should only be used for old applications built on the AWS EC2-Classic network layout._

---

Core Structural Mechanisms

To configure an ELB properly, you must define three basic architectural pieces:

```
[ Internet Traffic ] ──> [ Listener (Port 443) ] ──> [ Routing Rules ] ──> [ Target Group (EC2 Fleet) ]
```

- **Listeners:** A process that continuously checks for connection requests based on the protocol and port you configure (e.g., an HTTPS listener tracking port 443).
- **Target Groups:** Logical groupings of your backend destinations (like your EC2 instances or ECS tasks). A single load balancer can route to multiple distinct target groups using independent criteria.
- **Health Checks:** The load balancer periodically pings targets inside the target group using a designated path and protocol (e.g., an HTTP GET request to `/health`). If a target fails to respond successfully a set number of times, it is flagged as unhealthy, and the load balancer instantly halts routing traffic to it.

---

Load Balancer Features Compared

|Attribute|Application Load Balancer (ALB)|Network Load Balancer (NLB)|
|---|---|---|
|**OSI Layer**|Layer 7 (HTTP/HTTPS)|Layer 4 (TCP/UDP/TLS)|
|**Performance Scale**|Millions of requests (Elastic scaling)|Ultra-high throughput (Instant scaling)|
|**Routing Features**|Path, Host, Query-string, HTTP Headers|Static IP, Port forwarding|
|**SSL/TLS Offloading**|Yes (Decrypts traffic at the ALB)|Yes (High-speed hardware encryption)|