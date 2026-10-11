**AWS CloudTrail** is ==an auditing, compliance, and governance service that records API calls and actions taken across your entire AWS account== [1.1].

While CloudWatch monitors your infrastructure's active performance, CloudTrail functions as a **security camera**, logging exactly who did what, when they did it, and from where [1.1].

---

🔍 The Core Questions CloudTrail Answers

Every time a user logs into the Console, a developer runs a command in the AWS CLI, or an infrastructure template uses an SDK, CloudTrail captures the event and logs the answers to these critical questions:

- **Who** made the request? (The specific IAM User, Role, or Federated identity) [1.1].
- **What** action was taken? (The specific API call, like `RunInstances`, `CreateBucket`, or `DeleteUser`).
- **When** did it happen? (A precise cryptographic timestamp) [1.1].
- **Which** resources were affected? (The exact ARNs of the target files, databases, or instances).
- **Where** did the request come from? (The source IP address and user agent string) [1.1].

---

📦 Event Types Tracked by CloudTrail

CloudTrail categorizes account activity into three distinct buckets:

- **Management Events (Default):** These track control plane operations performed on your AWS resources. Examples include setting up an IAM Policy, configuring a subnet, or creating an Internet Gateway [1.1]. CloudTrail logs these automatically for **90 days** completely free of charge.
- **Data Events (Optional):** These track high-volume data operations _within_ a resource itself. Examples include a user downloading an object from an S3 bucket or invoking an AWS Lambda function [1.17, 1.27]. These are turned off by default due to ingestion volume but can be enabled for tight security auditing.
- **Insights Events (Optional):** These leverage machine learning to analyze your management logs and automatically flag **unusual or anomalous activity**, such as a sudden massive spike in resource deletions or an unexpected burst of API failures.

---

🛡️ Best Practices & Storage Architecture

Because CloudTrail logs are the ultimate source of truth for an investigation, protecting the log integrity is crucial:

1. **S3 Storage & KMS Encryption:** You can configure CloudTrail to continuously deliver log files directly to a secure Amazon S3 bucket [1.9, 1.11]. These files should be encrypted using **AWS KMS symmetric keys** [1.3].
2. **Log File Integrity Validation:** Turning this feature on tells CloudTrail to generate cryptographic hashes for your log files. This allows you to mathematically prove if a log file was tampered with, modified, or deleted after delivery.
3. **Multi-Region Trails:** Always configure your trails to apply to **All Regions**. This ensures that if a malicious actor accesses your account and spins up unauthorized EC2 instances in an obscure foreign region, the activity is still fully captured and centralized.

---

🤝 The Cloud Monitoring Trio

To keep your notes perfectly organized, remember how CloudTrail integrates with the other primary governance services:

|Service|Primary Question Answered|Focus Metric|
|---|---|---|
|**AWS CloudTrail**|_"Who initiated this action or API call?"_ [1.1]|**Identity Auditing**|
|**Amazon CloudWatch**|_"How is this system performing right now?"_ [1.27]|**Performance Metrics**|
|**AWS Config**|_"How has this resource's configuration changed over time?"_|**Compliance History**|