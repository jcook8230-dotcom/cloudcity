**Encryption at rest** is ==the security practice of protecting data while it is statically stored on a physical disk, solid-state drive, or tape==.

This prevents unauthorized users or bad actors from reading sensitive files if they manage to gain physical access to the hard drives or bypass network perimeter defenses. In AWS, encryption at rest is heavily automated and relies tightly on **AWS KMS** to manage the cryptographic keys.

---

🛡️ How AWS Handles Encryption at Rest

When you enable encryption at rest in AWS, the underlying infrastructure handles the heavy lifting through hardware-accelerated encryption.

- **S3 Bucket Encryption (SSE-S3 & SSE-KMS):** S3 encrypts your data at the object level. By default, every bucket automatically applies server-side encryption (SSE-S3). If you need an audit trail of who used the key, you swap it to **SSE-KMS**.
- **EBS Volume Encryption:** When you launch an EC2 instance with an encrypted Elastic Block Store (EBS) volume, all data moving between the instance and the volume is encrypted. This includes snapshots created from that volume and any subsequent volumes created from those snapshots.
- **Database Encryption:** Services like **Amazon RDS** and **DynamoDB** support encryption at rest seamlessly. Turning it on encrypts the underlying storage tables, database logs, automated backups, and read replicas.

---

🧱 Encryption Types: Server-Side vs. Client-Side

You can implement encryption at rest in two distinct locations depending on your compliance requirements:

|Attribute|Server-Side Encryption (SSE)|Client-Side Encryption|
|---|---|---|
|**Where it happens**|Inside the AWS cloud infrastructure.|On your local machine/app before uploading.|
|**Who manages it**|AWS handles the encryption process automatically.|Your software application handles the process.|
|**Visibility**|AWS sees plaintext data briefly during transit.|AWS only ever sees completely unreadable ciphertext.|
|**Key Custody**|Keys can be AWS-managed or Customer-managed.|You manage keys locally or use KMS remotely.|

---

🔍 Monitoring & Compliance with CloudTrail

Because encryption keys act as the ultimate guardrails for your data, compliance frameworks require strict auditing. Every time an AWS service requests a data key from KMS to encrypt or decrypt a block of data, **AWS CloudTrail logs the event**. This allows security teams to view exact time stamps, the requesting IAM identity, and the specific resource being accessed.

---

