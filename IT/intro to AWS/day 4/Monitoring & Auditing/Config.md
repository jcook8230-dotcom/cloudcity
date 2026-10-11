**AWS Config** is a fully managed service that provides you with a **detailed resource inventory, configuration history, and compliance auditing** for your entire AWS infrastructure.

While CloudTrail records _who_ made an API call, AWS Config continuously monitors _what_ your resources look like, tracking exactly how their configurations change over time and checking those changes against pre-defined compliance guardrails.

---

🧱 The Core Mechanics of AWS Config

AWS Config acts as both a time machine and a compliance officer for your cloud infrastructure:

- **Configuration Recorder:** It continuously discovers and maps the relationships between your AWS resources (such as an EC2 instance connected to a specific Security Group and VPC). Whenever a setting changes, it records the delta.
- **Configuration History (The Time Machine):** It maintains a visual point-in-time timeline of your assets. If a database goes down on a Tuesday, you can pull up AWS Config to see exactly what changed in that database's network rules on Monday night.
- **Managed Rules (The Compliance Officer):** You can implement built-in or custom rules that define what your infrastructure _should_ look like. For example:
    - _Rule:_ "All S3 buckets must have public read access disabled."
    - _Rule:_ "All EBS volumes must be encrypted at rest."

---

🚨 Compliance & Automated Remediation

When a resource drifts from its intended state, AWS Config handles the enforcement loop through two pathways:

1. **Non-Compliant Flags:** If a developer turns off encryption on an S3 bucket or opens port 22 (SSH) to the public internet on a Security Group, AWS Config immediately evaluates it, flags the resource as **Non-compliant**, and triggers an alert via Amazon SNS.
2. **Automated Remediation:** You can link AWS Config rules to **AWS Systems Manager (SSM) Automation documents**. If a resource is flagged as non-compliant, Config can automatically execute a script to fix it in real-time (e.g., instantly applying a private bucket policy back onto a leaked bucket).

---

🛡️ The Big Three: CloudWatch vs. CloudTrail vs. Config

Because these tracking tools are frequently used together, keeping their distinct responsibilities organized in your notes is essential:

|Service|Ultimate Focus|Core Diagnostic Question|
|---|---|---|
|**Amazon CloudWatch**|**Performance & Logs**|_"Is my system running hot? Why is memory utilization spiking?"_|
|**AWS CloudTrail**|**API & Identity Auditing**|_"Who logged in at 2:00 AM and deleted this DynamoDB table?"_|
|**AWS Config**|**Compliance & Resource State**|_"What did this security group look like last Thursday before it broke?"_|

---