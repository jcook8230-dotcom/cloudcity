**Security Groups** act as virtual firewalls for your Amazon EC2 instances and other VPC resources, controlling both inbound and outbound TCP/IP traffic at the **individual resource level** rather than the subnet boundary.

While a Route Table maps out the road network (where traffic _can_ go), a Security Group acts like a security guard stationed directly at the front door of your specific virtual server, deciding who is permitted to enter or exit.

Core Operational Principles

- **Stateful Filtering:** Security Groups are **stateful**. This means if you create a rule allowing a specific inbound request to enter your EC2 instance (e.g., web traffic on port 80), the return outbound traffic is **automatically allowed** back out, regardless of your outbound rule configurations.
- **Implicit Deny by Default:** When you create a new Security Group, it contains **zero inbound rules**. All incoming traffic is completely blocked by default until you explicitly add an "Allow" rule.
- **No Deny Rules:** You can only specify **Allow rules**. You cannot create a rule to explicitly block or deny a specific IP address (for explicit Deny rules, you must use Network ACLs at the subnet level).
- **Dynamic Attachment:** You can attach multiple Security Groups to a single EC2 instance (up to 5 by default). Changes made to your rules are **applied instantly** to all attached resources without requiring a server reboot.

---

Anatomy of a Security Group Rule

Every rule you define within a Security Group requires four specific parameters to evaluate traffic:

```
[ Protocol: TCP ] ──> [ Port Range: 443 ] ──> [ Source: 0.0.0.0/0 ] ──> [ Action: Allow ]
```

- **Type/Protocol:** The network protocol being utilized (e.g., TCP, UDP, ICMP, or All Traffic).
- **Port Range:** The specific port or range of ports the traffic is targeting (e.g., Port `80` for HTTP, Port `443` for HTTPS, or Port `22` for SSH).
- **Source / Destination:**
    - For **Inbound Rules**, the _Source_ dictates where the traffic is coming from (e.g., a specific IP like `203.0.113.50/32`, an IP range, or another Security Group).
    - For **Outbound Rules**, the _Destination_ dictates where the instance is allowed to send traffic.
- **Description:** A text label to help document the purpose of the rule for auditing.

---

Security Group Rule Referencing (Chaining)

One of the most powerful features of Security Groups is the ability to reference **another Security Group as a Source**, rather than hardcoding unstable IP addresses. This allows you to build highly secure, multi-tier architectures:

```
┌─────────────────────────────────────────────── Amazon VPC ───────────────────────────────────────────────┐
│                                                                                                          │
│  [ Public Tier ]                                       [ Private Tier ]                                  │
│  ┌─────────────────────────────┐                       ┌─────────────────────────────┐                   │
│  │  Application Load Balancer  │                       │      EC2 App Instances      │                   │
│  │  (SG: alb-sg)               │                       │      (SG: app-sg)           │                   │
│  └──────────────┬──────────────┘                       └──────────────▲──────────────┘                   │
│                 │                                                     │                                  │
│                 └─────── (Traffic sent from alb-sg) ──────────────────┘                                  │
│                          Inbound Rule: Allow TCP 8080 from "alb-sg"                                      │
└──────────────────────────────────────────────────────────────────────────────────────────────────────────┘
```

Instead of allowing port 8080 open to the whole world (`0.0.0.0/0`) on your private application servers, you configure your `app-sg` inbound rule to **only allow traffic originating from resources attached to `alb-sg`**. If your load balancer scales out from 2 instances to 20 instances, the private app servers automatically trust the new instances without any firewall updates.

---

Default Settings

Every VPC automatically comes with a **Default Security Group**. If you do not specify a Security Group when launching an EC2 instance, AWS automatically assigns the default one.

- Its default inbound rule allows all traffic originating from **itself** (instances sharing that same default group can talk to one another).
- Its default outbound rule allows **all outbound traffic** to any destination (`0.0.0.0/0`).