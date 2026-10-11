**Network ACLs (Access Control Lists)** ==act as an optional layer of security for your VPC, serving as a **stateless firewall for controlling traffic in and out of one or more subnets**==.

While a Security Group acts as a guard at the door of an individual virtual server (instance level), a Network ACL acts as a security checkpoint at the perimeter gate of the entire neighborhood (subnet level). Any traffic entering or exiting a subnet must pass through the Network ACL rules first.

---

Core Operational Principles

- **Stateless Filtering:** Network ACLs are **stateless**. This means that return traffic is _not_ automatically allowed. If you create an inbound rule allowing traffic into your subnet, you must explicitly create a corresponding outbound rule to allow that response traffic back out.
- **Numbered Rule Order:** Rules are processed sequentially, starting with the lowest-numbered rule (e.g., rule 100, then 200, then 300). As soon as a packet matches a rule, the decision (Allow or Deny) is applied instantly, and **no further rules are evaluated**.
- **Explicit Deny Rules:** Unlike Security Groups (which only support "Allow" rules), Network ACLs support both **Allow and Deny rules**. This makes them the primary tool for explicitly blocking malicious traffic or specific IP addresses from entering your network infrastructure.
- **The Catch-All Default:** Every Network ACL ends with an unnumbered asterisk (`*`) rule. This rule cannot be modified or deleted, and it explicitly **denies all traffic** that hasn't matched a previous numbered rule.

---

Anatomy of a Network ACL Rule

When writing a Network ACL rule, you must define five precise structural components:

```
[ Rule #: 100 ] ──> [ Protocol: TCP ] ──> [ Port: 443 ] ──> [ Source: 203.0.113.50/32 ] ──> [ Action: DENY ]
```

1. **Rule Number:** Determines the processing order (e.g., 100). It is best practice to leave gaps between numbers (e.g., 100, 110, 120) so you can insert new rules later if needed.
2. **Protocol:** The network protocol (e.g., TCP, UDP, ICMP, or All Traffic).
3. **Port Range:** The specific port number or range (e.g., `80` for HTTP, `22` for SSH).
4. **Source / Destination:** The CIDR block range indicating where the traffic originates (Inbound) or where it is going (Outbound).
5. **Action:** The explicit verdict—either **ALLOW** or **DENY**.

---

Default vs. Custom Network ACLs

AWS configures default and custom Network ACLs with completely opposite baselines:

- **The Default Network ACL:** Every VPC comes with a default Network ACL. By default, it contains a rule numbered `100` that **allows all inbound and outbound traffic** (`0.0.0.0/0`). If you create a subnet and don't associate it with a custom ACL, it automatically inherits this wide-open default behavior.
- **Custom Network ACLs:** When you create a brand-new, custom Network ACL, it starts with **zero numbered rules**. It will completely **block all inbound and outbound traffic** by default until you manually insert your own numbered rules.

---

The Ephemeral Port Pitfall

Because Network ACLs are stateless, a common mistake is configuring an inbound rule for a web server (e.g., Allow Inbound Port 443) but forgetting to open up the **Ephemeral Ports** on the outbound side.

When a client initiates a connection to a server on port 443, the server responds back using a temporary destination port chosen from the client's ephemeral port range (typically **1024 to 65535**). If your outbound Network ACL does not explicitly allow outbound traffic to ports 1024–65535, the response packet will be dropped, and the connection will fail.

---

Security Groups vs. Network ACLs (Quick Summary)

|Feature|Security Groups|Network ACLs|
|---|---|---|
|**Operational Level**|Instance / Resource level|Subnet boundary level|
|**State Nature**|Stateful (automatic return path)|Stateless (must manually open both ways)|
|**Rule Application**|Evaluates all rules before deciding|Evaluates sequentially by rule number|
|**Explicit Deny?**|No (Allow rules only)|Yes (Supports both Allow and Deny)|