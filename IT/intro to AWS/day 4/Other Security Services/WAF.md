🧱 ==**AWS WAF (Web Application Firewall)**== is a specialized web application firewall that helps protect your web applications and APIs against common web exploits and malicious bots that may affect availability, compromise security, or consume excessive resources [2.1].

Unlike a standard firewall or Security Group which operates at the Network/Transport layers (Layer 3 and 4), AWS WAF operates strictly at the **Application Layer (Layer 7)** of the OSI model [2.1]. This means it can inspect the actual contents of incoming HTTP and HTTPS requests, including headers, cookies, query strings, and body data [2.11].

---

🛡️ What AWS WAF Protects Against

AWS WAF is designed to intercept and block sophisticated web attacks before they ever reach your backend servers [2.1]:

- **OWASP Top 10 Flaws:** It provides defense against widespread application-layer vulnerabilities like **SQL Injection (SQLi)** (malicious code injected into database queries) and **Cross-Site Scripting (XSS)** (malicious scripts injected into web pages) [2.11].
- **DDoS Protection (Layer 7):** It stops application-level floods, such as HTTP flood attacks, by implementing rate-limiting rules [2.1, 2.11].
    
- **Bots and Scrapers:** It can block or challenge automated web scrapers, credential-stuffing bots, and brute-force login attempts [2.1].

---

⚙️ How It Works: Web ACLs and Rules

To deploy AWS WAF, you create a **Web ACL (Access Control List)** and associate it with an internet-facing resource [2.11]. Within that Web ACL, you define rules using two primary approaches:

1. **AWS Managed Rules:** Pre-configured rule sets created and maintained by AWS and security partners [2.1]. These give you immediate protection against common threats without requiring you to write custom regex patterns [2.1].
2. **Custom Rules:** Rules you write yourself to filter traffic based on specific parameters:
    - _IP Allow/Block Lists:_ Permit or deny traffic from specific IP addresses.
    - _Geo-Match Rules:_ Block or allow traffic originating from specific countries.
    - _String/Regex Matches:_ Block requests that contain specific malicious patterns in the user-agent header or URI string [2.11].

---

🔌 Where Can You Deploy AWS WAF?

AWS WAF cannot be attached directly to an individual EC2 instance. Instead, it must be attached to an infrastructure component sitting in front of your applications [2.11]:

- **Amazon CloudFront:** Secures traffic right at the global edge locations, stopping attacks closest to the user before they enter the core AWS network [2.11].
- **Application Load Balancer (ALB):** Protects regional web application routing paths.
- **Amazon API Gateway:** Secures serverless REST and HTTP API endpoints.
- **AWS AppSync:** Secures GraphQL APIs.

---

🤝 The Edge Protection Duo: WAF vs. Shield

AWS WAF works hand-in-hand with **AWS Shield** to provide complete perimeter protection, but they tackle different angles [2.1]:

|Feature|AWS WAF|AWS Shield (Standard/Advanced)|
|---|---|---|
|**OSI Layer**|**Layer 7** (Application Layer) [2.1]|**Layers 3 & 4** (Network & Transport) [2.1]|
|**Primary Focus**|SQLi, XSS, bad bots, customized HTTP filtering [2.1, 2.11].|Volumetric DDoS attacks (SYN floods, UDP reflection) [2.1].|
|**Inspection Depth**|Looks deep inside the HTTP request body and headers [2.11].|Looks at traffic volume, packet headers, and network flow.|

---