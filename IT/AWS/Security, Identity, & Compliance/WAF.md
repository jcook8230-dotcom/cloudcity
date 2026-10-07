**AWS WAF (Web Application Firewall)** is ==a cloud-native security service operating at the **Application Layer (Layer 7)** to protect web applications and APIs from common web exploits, automated bots, and malicious HTTP/HTTPS traffic==. It functions as a programmable gatekeeper by inspecting incoming web requests before they reach your underlying application backends. [[1](https://www.pump.co/blog/aws-waf/), [2](https://www.youtube.com/watch?v=Jh0LBZMkMkQ&t=446)]

---

Core Pricing & Components

|Component|Standard Unit Price|Description|
|---|---|---|
|**Web ACL**|**$5.00/month**|Base container (prorated hourly) for organizing your inspection rules|
|**Rules**|**$1.00/month**|Individual custom rules or standard managed rule groups added to a Web ACL|
|**Request Processing**|**$0.60 per 1 million**|Fee for web requests inspected and processed by the Web ACL|
|**Bot Control**|**$10.00/month** + requests|Subscription per Web ACL for advanced bot visibility and mitigation|
|**Fraud Control**|**$10.00/month** + requests|Subscription for account takeover prevention and credential stuffing protection|

_Note: Organizations leveraging [AWS Shield Advanced](https://aws.amazon.com/shield/features/) receive inclusion coverage for basic WAF web ACLs, standard rules, and request processing fees up to 50 billion requests per month._ [[1](https://aws.amazon.com/blogs/security/aws-shield-advanced-is-embracing-the-aws-waf-anti-ddos-managed-rule-group-what-changes-and-how-to-prepare/), [2](https://hykell.com/knowledge-base/aws-waf-pricing-and-cost-management/)]

---

How AWS WAF Operates

- **Request Inspection:** Evaluates individual HTTP/S attributes including query strings, URIs, HTTP headers, body content (up to standard or extended inspection limits), and source IP geographical locations. [[1](https://aws.amazon.com/waf/pricing/), [2](https://www.youtube.com/watch?v=-9YzrRCzaKM&t=795)]
- **Terminating & Non-Terminating Actions:** Supports actions like `Allow` and `Block` (which halt further evaluation) alongside `Count` (which logs the match without interrupting flow). [[1](https://aws.amazon.com/blogs/networking-and-content-delivery/cost-effective-ways-for-securing-your-web-applications-using-aws-waf/)]
- **Interactive Challenges:** Integrates native `CAPTCHA` and silent browser/device `Challenge` actions to automatically weed out bad scripts and automated scraping tools from legitimate human users. [[1](https://www.pump.co/blog/aws-waf/)]
- **Managed Rule Groups:** Allows developers to deploy pre-configured rule sets from AWS or third-party vendors via the [AWS Marketplace](https://aws.amazon.com/waf/) to defend against the OWASP Top 10 vulnerabilities like SQL injection and cross-site scripting (XSS).
    
    [[1](https://docs.aws.amazon.com/decision-guides/latest/decision-guides/waf-or-shield.html), [2](https://www.youtube.com/watch?v=Jh0LBZMkMkQ&t=446)]

---

Integration Architecture

AWS WAF attaches directly to edge and regional endpoints including **Amazon CloudFront**, **Application Load Balancer (ALB)**, **Amazon API Gateway**, and **AWS AppSync**. For deeper implementation specifics, consult the official [AWS WAF Developer Guide](https://docs.aws.amazon.com/waf/latest/developerguide/what-is-aws-waf.html). [[1](https://docs.aws.amazon.com/decision-guides/latest/decision-guides/waf-or-shield.html), [2](https://docs.aws.amazon.com/waf/latest/developerguide/what-is-aws-waf.html), [3](https://www.pump.co/blog/aws-waf/)]

If you'd like, let me know:

- What **specific AWS endpoints** (e.g., CloudFront, ALB) you plan to attach WAF to
- Whether you need help configuring **Bot Control** or custom rules
- Your estimated **monthly request volume** for a precise cost projection