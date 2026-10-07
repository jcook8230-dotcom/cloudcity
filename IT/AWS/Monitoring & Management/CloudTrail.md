**AWS CloudTrail** is ==a managed compliance and auditing service that continuously records, monitors, and retains account activity across your entire AWS infrastructure==. It provides a detailed event history of actions taken through the AWS Management Console, AWS SDKs, command line tools, and native AWS services, capturing exactly **who** made a request, **what** resources were targeted, and **when** the action occurred.

---

Core Event Types & Pricing

|Event Category|Free Tier Policy|Standard Unit Pricing (Beyond Free Tier)|Description|
|---|---|---|---|
|**Management Events**|**Free** (First trail / 90-day history)|**$2.00 per 100,000 events** delivered|Control plane operations (e.g., creating an S3 bucket, launching an EC2 instance).|
|**Data Events**|None|**$0.10 per 100,000 events** delivered|Resource-level data operations (e.g., S3 `GetObject`, Lambda `Invoke`).|
|**Insights Events**|None|**$0.35 per 100,000 events** analyzed|Automated anomaly detection tracking unusual API call volumes.|

_Note: Storage costs for storing log files in Amazon S3 or streaming them to Amazon CloudWatch Logs are billed separately under those respective services' rates._

---

How AWS CloudTrail Operates

- **Automatic 90-Day Event History:** Every AWS account has CloudTrail enabled by default, keeping a rolling 90-day ledger of management events that you can search and filter in the console at no cost.
- **Multi-Region & Organization Trails:** You can configure a single "Trail" to capture events across all global AWS Regions. For corporate environments, you can deploy an Organization Trail that locks down logging configurations across every member account within [AWS Organizations](https://aws.amazon.com/organizations/).
- **Log Integrity Validation:** Uses cryptographic hashing to generate digest files. This allows compliance auditors to mathematically verify that your log files have not been modified, deleted, or tampered with since CloudTrail deposited them into your secure S3 storage bucket.
- **CloudTrail Lake:** A managed data lake feature that lets you run complex SQL queries directly against up to seven years of activity logs, eliminating the need to build separate data pipelines or parse raw JSON files manually.