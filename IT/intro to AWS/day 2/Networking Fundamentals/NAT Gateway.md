A **NAT Gateway** (Network Address Translation Gateway) is a highly available, managed AWS service that allows resources in a **private subnet** to connect to the internet or other AWS services, while completely **blocking the public internet from initiating inbound connections** with them.

Think of it as a one-way security valve for your network traffic. It is most commonly used to allow backend servers (like databases or app instances) to safely download software patches, run package updates, or connect to external APIs without exposing those servers to external cyber threats.

---

How a NAT Gateway Works

A NAT Gateway must always be physically placed inside a **Public Subnet** (a subnet with a direct route to an Internet Gateway) and assigned an **Elastic IP address** (a static, public IPv4 address).

```
┌─────────────────────────────────────── Amazon VPC ───────────────────────────────────────┐
│                                                                                          │
│  ┌───────────────── Private Subnet ─────────────────┐                                    │
│  │  [ Internal App Server ] (Private IP Only)       │                                    │
│  └──────────────────────────┬───────────────────────┘                                    │
│                             │ (Outbound Only: 0.0.0.0/0)                                 │
│                             ▼                                                            │
│  ┌────────────────── Public Subnet ─────────────────┐                                    │
│  │  [ NAT Gateway ] (Elastic IP) ───────────────────────> [ Internet Gateway ]          │
│  └──────────────────────────────────────────────────┘             │                      │
└───────────────────────────────────────────────────────────────────┼──────────────────────┘
                                                                    ▼
                                                            [ Public Internet ]
```

1. **The Request:** An EC2 instance in a private subnet sends a request out to the internet (e.g., `sudo apt-get update`).
2. **The Translation:** The traffic is routed to the NAT Gateway in the public subnet. The NAT Gateway replaces the instance's private IP address with its own public Elastic IP address.
3. **The Delivery:** The NAT Gateway forwards the traffic out through the Internet Gateway to the web.
4. **The Return:** When the internet resource responds, the NAT Gateway receives the data, matches it to the original request, translates the IP back, and securely passes the data down to the private instance.

---

Route Table Configurations for NAT Gateway

To make this architecture function, you must configure two distinct route tables to control how traffic flows through the gateways:

1. Public Subnet Route Table

The public subnet hosts the NAT Gateway and routes directly to the open internet via the Internet Gateway.

- **`10.0.0.0/16`** ──> `local`
- **`0.0.0.0/0`** ──> `igw-xxxxxx` _(Internet Gateway)_

2. Private Subnet Route Table

The private subnet blocks direct internet access and forces all external traffic to go through the NAT Gateway.

- **`10.0.0.0/16`** ──> `local`
- **`0.0.0.0/0`** ──> `nat-xxxxxx` _(NAT Gateway)_

---

Key Operational Characteristics

- **Highly Scalable and Managed:** Unlike legacy custom NAT Instances, you do not manage the underlying operating system or patch the software. It automatically scales its bandwidth capacity up to **100 Gbps** to handle your network load.
- **Availability Zone Bound:** A NAT Gateway is redundant within a single Availability Zone (AZ). For a highly available production architecture, you should deploy **one NAT Gateway per AZ** so that an outage in one physical data center won't take down the internet connectivity of your entire regional infrastructure.
- **Pricing Metric:** You are billed an hourly rate for keeping the NAT Gateway active, plus a per-gigabyte fee for all data that processes through the gateway.