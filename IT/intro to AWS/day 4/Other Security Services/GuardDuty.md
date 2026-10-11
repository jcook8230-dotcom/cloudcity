**Amazon GuardDuty** is ==a continuous, intelligent **threat detection service** that monitors your AWS accounts, workloads, and data for malicious activity==. [[1](https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_finding-types-active.html), [2](https://www.youtube.com/watch?v=hJKIzLe49kE&t=92)]

While CloudTrail, CloudWatch, and AWS Config log identity actions and state baselines, GuardDuty acts as your **cloud-native burglar alarm** [1.1]. It sits passively beside your infrastructure, analyzing massive streams of metadata using machine learning, anomaly detection, and integrated global threat intelligence to spotlight active attacks. [[1](https://www.stormit.cloud/blog/amazon-guardduty/), [2](https://www.youtube.com/watch?v=E5p_WnP4pw8&t=121), [3](https://www.youtube.com/watch?v=hJKIzLe49kE&t=92)]

---

📥 Foundational Telemetry (Zero Performance Impact)

The major advantage of GuardDuty is its **agentless architecture** for standard coverage. It consumes background AWS data streams directly without requiring you to install software or configure log forwarding, completely eliminating infrastructure performance overhead. It monitors three core logs by default: [[1](https://www.youtube.com/watch?v=E5p_WnP4pw8&t=121)]

- **VPC Flow Logs:** Analyzes network traffic patterns inside your infrastructure to look for unusual outbound connections.
- **DNS Query Logs:** Inspects outbound DNS lookups to see if a resource is communicating with known malicious domains.
- **CloudTrail Management & Data Events:** Audits account API footprints to flag patterns matching credential abuse or data exfiltration. [[1](https://aws.github.io/aws-security-services-best-practices/guides/guardduty/), [2](https://aws.amazon.com/guardduty/features/), [3](https://www.youtube.com/watch?v=E5p_WnP4pw8&t=121)]

---

🛡️ Specialized Protection Plans

GuardDuty includes specialized modules you can enable depending on your workload mix: [[1](https://www.youtube.com/watch?v=hJKIzLe49kE&t=1659)]

- **Malware Protection (EC2, S3, & Backups):** Scans files for viruses, ransomware, or spyware. For EC2, it takes a temporary snapshot of the attached **EBS volume** to scan it agentlessly so your live production servers never experience disk slowdowns. [[1](https://www.trendmicro.com/trendaivisiononecloudriskmanagement/knowledge-base/aws/GuardDuty/enable-guardduty-protection-features.html), [2](https://note.com/terraskytech/n/naf31f1a84992?hl=en)]
- **Runtime Monitoring:** Optional eBPF-based lightweight agents that let GuardDuty look _inside_ running operating systems or container pods (**ECS, EKS, Fargate, EC2**) to detect post-compromise behaviors like file tampering or reverse shell executions. [[1](https://aws.amazon.com/about-aws/whats-new/2026/07/amazon-guardduty-sfm/), [2](https://note.com/terraskytech/n/naf31f1a84992?hl=en)]
- **Database & AI Protection:** Analyzes anomalous login behavior on **Amazon RDS/Aurora** instances and monitors **Amazon Bedrock/SageMaker** environments for cost-harvesting attacks or prompt injections. [[1](https://aws.amazon.com/guardduty/), [2](https://aws.amazon.com/about-aws/whats-new/2026/07/amazon-guardduty-ai-protection-aws/)]

---

🚨 GuardDuty Finding Severities

When GuardDuty uncovers a threat, it generates a **Finding** tagged with a score from 0.1 to 10.0, grouped into three primary categories: [[1](https://www.nops.io/glossary/what-is-aws-guard-duty/)]

|Severity Category|Score Range|Real-World Attack Scenarios|Immediate Action Required?|
|---|---|---|---|
|**High**|7.0 – 8.9|`Crypto:EC2/BitcoinMined` (An instance is hijacked for mining), compromised IAM root credentials.|**Yes** — The resource is actively compromised.|
|**Medium**|4.0 – 6.9|`UnauthorizedAccess:IAMUser/ConsoleLogin` (A user logged in from an unexpected foreign country).|**Investigate** — Behavior deviates heavily from the normal baseline.|
|**Low**|1.0 – 3.9|`Recon:EC2/PortProbeUnprotectedPort` (An internet scanner is probing open ports on your public instance).|**Monitor** — The attack attempt was blocked or unsuccessful.|

---

🔄 Closing the Loop: Automated Remediation

GuardDuty is purely detective, but you can build a complete **automated response loop**. When a High finding occurs: [[1](https://www.stormit.cloud/blog/amazon-guardduty/)]

1. GuardDuty routes the JSON payload to **Amazon EventBridge**.
2. EventBridge triggers an **AWS Lambda function**.
3. The Lambda function automatically detaches the compromised IAM policy or modifies the targeted Security Group to isolate the instance from the network. [[1](https://builder.aws.com/content/33KXBsIKgirXK0dz8EZfCKc7vsQ/amazon-guardduty-deep-dive-architecture-detections-2025-updates-and-playbooks), [2](https://www.stormit.cloud/blog/amazon-guardduty/), [3](https://note.com/terraskytech/n/naf31f1a84992?hl=en)]

---

🧠 Security Services Cheat Sheet

- **AWS Shield:** DDoS mitigation protecting network edges (Layers 3, 4, and 7).
- **AWS WAF:** Web Application Firewall blocking SQL injection and cross-site scripting (Layer 7).
- **Amazon GuardDuty:** Intelligent behavioral threat detection for internal infrastructure.
- **AWS Security Hub:** A centralized dashboard that aggregates findings from GuardDuty, Macie, Inspector, and IAM Access Analyzer. [[1](https://www.stormit.cloud/blog/amazon-guardduty/), [2](https://www.youtube.com/watch?v=hJKIzLe49kE&t=92)]