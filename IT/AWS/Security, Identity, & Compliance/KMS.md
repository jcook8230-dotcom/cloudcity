**AWS Key Management Service (AWS KMS)** is ==a managed cloud security service that lets you create and control the cryptographic root keys used to protect and sign your data across your infrastructure==. It relies on hardware security modules validated under FIPS 140-3 Security Level 3 to ensure that your master keys never leave the hardware unencrypted. [[1](https://docs.aws.amazon.com/kms/latest/developerguide/overview.html), [2](https://aws.amazon.com/kms/features/), [3](https://www.techtarget.com/it-infrastructure/definition/AWS-Key-Management-Service-AWS-KMS)]

---

Key Management Tiers and Pricing

|Key Management Type|Monthly Storage Fee|API Usage Fee|Description|
|---|---|---|---|
|**Customer Managed Key (CMK)**|**$1.00/month** (prorated hourly)|Yes ($0.03 per 10,000 symmetric requests)|Fully owned and managed by your organization.|
|**AWS Managed Key**|**Free**|Yes (billed for API usage)|Created and managed automatically by integrated AWS services.|
|**AWS Owned Key**|**Free**|**Free**|Shared collection of keys managed by AWS across multiple accounts.|

_Note: The [AWS KMS Free Tier](https://aws.amazon.com/kms/pricing/) includes **20,000 requests per month** for symmetric operations, calculated globally across all available regions._ [[1](https://aws.amazon.com/kms/pricing/), [2](https://cloudburn.io/tools/aws-kms-pricing-calculator)]

---

How Cryptography Works in AWS KMS

- **Envelope Encryption:** Instead of sending massive files directly through KMS, AWS services use a practice called envelope encryption. The service generates a local data key to encrypt your raw data, and then encrypts that data key using your master KMS key stored in the secure hardware boundary. [[1](https://aws.amazon.com/kms/faqs/), [2](https://aws.amazon.com/kms/features/), [3](https://builder.aws.com/content/2gXslT410ZTS9BvYEFTXwZ7DARx/aws-key-management-service)]
- **Symmetric vs. Asymmetric Keys:** Symmetric keys use a single 256-bit key for both encryption and decryption (ideal for most data at rest), while asymmetric keys create a public/private key pair used for digital signatures and verification. [[1](https://www.techtarget.com/it-infrastructure/definition/AWS-Key-Management-Service-AWS-KMS), [2](https://www.edureka.co/blog/aws-key-management-service-kms/)]
- **Automatic Key Rotation:** You can enable automatic annual rotation for symmetric customer managed keys without needing to re-encrypt any existing data, as KMS retains old key versions specifically to decrypt legacy ciphertext. [[1](https://aws.amazon.com/kms/faqs/), [2](https://builder.aws.com/content/2gXslT410ZTS9BvYEFTXwZ7DARx/aws-key-management-service)]
- **Auditing and Logging:** Every time a master key is invoked for a cryptographic action, the request is recorded in [AWS CloudTrail](https://aws.amazon.com/cloudtrail/) to support your compliance and forensic requirements. [[1](https://aws.amazon.com/kms/faqs/), [2](https://www.youtube.com/watch?v=8Z0wsE2HoSo)]

---

Integration and Advanced Options

AWS KMS integrates natively with over 100 cloud services like Amazon S3, EBS, and RDS. For high-compliance environments, you can also connect KMS to dedicated [AWS CloudHSM](https://aws.amazon.com/cloudhsm/) clusters or external key managers using the External Key Store (XKS) feature. [[1](https://aws.amazon.com/kms/features/), [2](https://aws.amazon.com/kms/faqs/), [3](https://www.youtube.com/watch?v=8Z0wsE2HoSo)]

