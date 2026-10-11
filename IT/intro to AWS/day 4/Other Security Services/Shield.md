🛡️ **AWS Shield** is ==a managed **Distributed Denial of Service (DDoS) protection service**== that safeguards applications running on AWS [4.1].

While **AWS WAF** handles complex application-layer code exploits (Layer 7) [2.1], AWS Shield focuses on blocking massive, volumetric network onslaughts (Layers 3 and 4)—such as SYN floods, UDP reflection attacks, and packet floods—designed to overwhelm your network infrastructure and knock your application offline [2.1, 4.1].

---

🎚️ The Two Tiers: Shield Standard vs. Shield Advanced

AWS Shield is deployed in two distinct service tiers based on your production requirements and budget [4.1]:

|Feature|AWS Shield Standard|AWS Shield Advanced|
|---|---|---|
|**Cost**|**Included automatically for free** [4.1].|**$3,000 / month** flat fee per organization.|
|**Activation**|On by default; requires zero configuration [4.1].|Requires manual activation and resource binding.|
|**OSI Layers**|Protects Layer 3 & 4 network traffic [2.1, 4.1].|Protects Layers 3, 4, and 7 network/web layers [2.1, 4.1].|
|**Financial Risk**|Standard protection; scaling costs apply.|**DDoS Cost Protection** (credits for scaling spikes).|
|**Support Team**|Standard AWS Support channels [4.12].|24/7 access to the **AWS SRT (Shield Response Team)**.|

---

🛡️ Deep Dive: AWS Shield Standard

- **Always-On Protection:** Every single AWS customer receives Shield Standard automatically at no extra cost [4.1].
- **Perimeter Scans:** It continuously inspects incoming traffic traveling into AWS edge locations and data centers.
- **Automatic Mitigation:** It runs inline traffic scrubbing patterns that automatically detect and block the most common, high-frequency network and transport layer DDoS attacks seamlessly without impacting application latency or performance.

---

🚀 Deep Dive: AWS Shield Advanced

Shield Advanced is tailored for enterprise applications where downtime results in massive financial or operational losses:

- **Extended Architecture Support:** It can be explicitly bound to **Amazon Route 53**, **Amazon CloudFront**, **Application Load Balancers (ALBs)**, and **AWS Global Accelerator**.
- **Layer 7 Visibility & Free WAF:** It provides advanced visibility into web application floods. When you subscribe, **AWS WAF usage and AWS Firewall Manager rules are included at no additional charge** for those resources [2.1, 2.11].
- **The AWS Shield Response Team (SRT):** During a complex or prolonged DDoS event, you get direct, manual architecture triage from specialized AWS security engineers who can write custom mitigation rules for your infrastructure in real-time.
- **DDoS Cost Protection:** If a massive attack forces your EC2 Auto Scaling groups or CloudFront distributions to scale out dramatically to absorb the traffic, AWS will credit your account back for those infrastructure cost spikes.

---

🤝 Perimeter Security Cheat Sheet

Keep your edge security definitions perfectly mapped out in your notes using this hierarchy:

1. **AWS Shield Standard:** The baseline network armor. Blocks standard layer 3/4 packet floods automatically [2.1, 4.1].
2. **AWS Shield Advanced:** Enterprise-grade defense. Adds 24/7 expert engineer support, cost protection, and deeper diagnostics [4.1].
3. **AWS WAF:** The application traffic filter. Inspects text strings inside HTTP headers to block SQLi, XSS, and bad bots [2.1, 2.11].
4. **AWS Firewall Manager:** The central policy administrator. Dynamically deploys WAF rules and Shield Advanced settings across dozens of separate AWS accounts simultaneously.

---
