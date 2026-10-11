🦺 **Amazon Inspector** is ==an automated, cloud-native **vulnerability management service**== that continuously scans your AWS workloads for software vulnerabilities and unintended network exposure.

While **GuardDuty** acts as a burglar alarm looking for _active attacks_, Amazon Inspector acts as a **home inspector**, proactively searching for _weak spots, outdated software, and structural flaws_ before a hacker can exploit them.

---

🔍 Key Areas Inspector Scans

Amazon Inspector continuously and automatically discovers workloads to scan across four primary targets:

- **EC2 Instances:** Scans the operating system and installed software packages for known CVEs (Common Vulnerabilities and Exposures). It can run completely agentlessly or leverage the standard AWS Systems Manager (SSM) agent.
- **Container Images (ECR):** Scans container images stored in the Amazon Elastic Container Registry (ECR) both upon upload and continuously afterward as new vulnerabilities are discovered globally.
- **AWS Lambda Functions:** Scans the application dependencies and custom package code inside your serverless Lambda functions for code-level security vulnerabilities.
- **Code Scans:** Inspects static application code within development pipelines for structural security issues, such as hardcoded API keys or cleartext secrets.

---

⚙️ How It Works: Continuous vs. On-Demand

Older vulnerability assessment tools required security teams to manually schedule scans. Amazon Inspector works **event-driven and continuously**:

1. **Trigger Event:** A new EC2 instance launches, an image is pushed to ECR, or a new global CVE database update is released.
2. **Automated Assessment:** Inspector immediately scans the target package inventory without requiring manual human oversight.
3. **Risk Scoring:** Inspector provides a highly contextualized **Inspector Risk Score**. This modifies standard global CVE severity ratings by looking at your active network configuration (e.g., if a piece of software has a critical flaw but the EC2 instance is completely closed off from the internet, the risk score drops).

---

⚔️ The Security Suite: Inspector vs. GuardDuty vs. Macie

It is incredibly common to mix up these three specialized security tools. Keep them distinct in your Obsidian notes using this matrix:

|Service|Primary Objective|What It Actually Looks At|
|---|---|---|
|**Amazon Inspector**|**Vulnerability Management**|Outdated software patches, CVEs, and unintended open ports.|
|**Amazon GuardDuty**|**Threat Detection**|Anomalous behavior, compromised instances, and active attacks.|
|**Amazon Macie**|**Data Privacy**|Sensitive personal data (SSNs, credit cards, PII) leaked in S3 buckets.|

---

