**AWS Transfer Family** is ==a fully managed cloud service that provides secure, scalable file transfers over industry-standard protocols==—including **Secure File Transfer Protocol (SFTP)**, **File Transfer Protocol Secure (FTPS)**, **File Transfer Protocol (FTP)**, and **Applicability Statement 2 (AS2)**—directly into and out of [Amazon Simple Storage Service (Amazon S3)](https://aws.amazon.com/s3/) or [Amazon Elastic File System (Amazon EFS)](https://aws.amazon.com/efs/). It eliminates the operational overhead of provisioning, patching, and scaling underlying file transfer servers. [[1](https://docs.aws.amazon.com/transfer/), [2](https://aws.amazon.com/aws-transfer-family/faqs/)]

---

Core Protocols & Pricing Structure

|Protocol / Feature|Standard Unit Price|Key Technical Details|
|---|---|---|
|**Server Endpoint**|**$0.30 per hour** per protocol enabled (~$219/mo)|Billed pro-rata hourly for active endpoints whether idle or transferring.|
|**Data Transfer (In/Out)**|**$0.04 per GB**|Charged for data uploaded and downloaded via SFTP, FTPS, or FTP.|
|**AS2 Messages**|**$0.01 per message**|Standard rate for B2B electronic data interchange (EDI) message exchanges.|
|**Managed Workflows**|**$0.10 per GB** processed|Optional fees for built-in file processing steps like PGP decryption.|

_Note: Standard storage and request fees for Amazon S3 or EFS apply separately._ [[1](https://aws.amazon.com/aws-transfer-family/pricing/)]

---

How AWS Transfer Family Operates

- **Storage Integration:** Files transferred through your endpoints land natively as objects in S3 or file structures in EFS, preserving metadata so downstream services like [Amazon Athena](https://aws.amazon.com/athena/) or [AWS Lambda](https://aws.amazon.com/lambda/) can process data immediately.
    
    [[1](https://aws.amazon.com/aws-transfer-family/features/)]
- **Authentication Options:** Supports service-managed identities (storing SSH keys locally in the service) or external directory integration via [AWS Managed Microsoft AD](https://aws.amazon.com/directoryservice/), custom APIs using [Amazon API Gateway](https://aws.amazon.com/apigateway/), or custom AWS Lambda authorizers. [[1](https://docs.aws.amazon.com/transfer/latest/userguide/sftp-for-transfer-family.html), [2](https://tutorialsdojo.com/aws-transfer-family/)]
- **SFTP Connectors:** Enables bi-directional workflows by allowing AWS to programmatically connect, list, download, rename, or delete files on external, partner-owned remote SFTP servers. [[1](https://docs.aws.amazon.com/transfer/latest/userguide/creating-connectors.html), [2](https://aws.amazon.com/video/watch/7516dd92a12/)]
- **Transfer Family Web Apps:** Provides a fully managed, browser-based portal where non-technical internal users or clients can securely upload and download files without needing a dedicated FTP client. [[1](https://tutorialsdojo.com/aws-transfer-family/)]
- **Security & Auditing:** Integrates with [AWS Identity and Access Management (IAM)](https://aws.amazon.com/iam/) for bucket access governance, [AWS Key Management Service (AWS KMS)](https://aws.amazon.com/kms/) for data encryption at rest, and [AWS CloudTrail](https://aws.amazon.com/cloudtrail/) for forensic logging. [[1](https://aws.amazon.com/aws-transfer-family/features/)]