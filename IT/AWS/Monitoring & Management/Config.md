**AWS Config** is ==a fully managed cloud service that enables you to assess, audit, and evaluate the configurations of your AWS resources by continuously tracking changes and verifying adherence to internal policies and external regulations==. It answers "what does each resource look like and how has it changed over time", serving as the foundational engine for compliance-as-code frameworks across your organization. [[1](https://aws.amazon.com/config/), [2](https://aws.amazon.com/blogs/mt/unlock-the-power-of-aws-config-centralized-compliance-and-resource-management/), [3](https://www.youtube.com/watch?v=J6VGVBlW9rM), [4](https://www.youtube.com/watch?v=gyTOHxRxKmU&t=207)]

---

Core Pricing & Components

|Component / Action|Standard Unit Pricing|Description|
|---|---|---|
|**Configuration Items (CIs)**|**$0.003 per item recorded**|Billed for every recorded point-in-time state change of a resource.|
|**Config Rule Evaluations**|**$0.001 per evaluation**|Charged per rule check in detective or proactive evaluation modes.|
|**Conformance Pack Evaluations**|**$0.001 per evaluation**|Fees for evaluating bundled rule packs aligned to frameworks like CIS or NIST.|
|**History & Snapshots**|**Standard S3/SNS rates**|Durable delivery of historical configuration ledgers to a custom storage bucket.|

_Note: For official service updates and comprehensive integration tutorials, consult the [Official AWS Config Documentation](https://aws.amazon.com/config/)._

---

How AWS Config Operates

- **Configuration Recorder:** Captures the initial state and streams ongoing modifications of supported resource types into timestamped Configuration Items (CIs). [[1](https://aws.amazon.com/blogs/mt/unlock-the-power-of-aws-config-centralized-compliance-and-resource-management/), [2](https://www.youtube.com/watch?v=J6VGVBlW9rM), [3](https://www.youtube.com/watch?v=t3tCfEySDxI&t=549)]
- **Config Rules:** Continuously evaluate resource settings against desired configurations using pre-built **AWS Managed Rules** or **Custom Rules** authored via AWS Lambda or CloudFormation Guard. [[1](https://aws.amazon.com/blogs/mt/unlock-the-power-of-aws-config-centralized-compliance-and-resource-management/), [2](https://www.youtube.com/watch?v=J6VGVBlW9rM), [3](https://www.youtube.com/watch?v=t3tCfEySDxI&t=549)]
- **Conformance Packs:** Bundle groups of compliance rules and automated remediation actions into a single template that can be deployed across an entire [AWS Organizations](https://aws.amazon.com/organizations/) hierarchy. [[1](https://aws.amazon.com/blogs/mt/unlock-the-power-of-aws-config-centralized-compliance-and-resource-management/), [2](https://www.youtube.com/watch?v=J6VGVBlW9rM)]
- **Automated Remediation:** Integrates with [AWS Systems Manager](https://aws.amazon.com/systems-manager/) automation documents to automatically correct non-compliant resource states (such as revoking an overly permissive security group). [[1](https://www.youtube.com/watch?v=J6VGVBlW9rM)]
- **Advanced Queries:** Empowers security teams to run ad-hoc, SQL-like property searches across multi-account, multi-region resource inventories without executing individual API calls. [[1](https://aws.amazon.com/config/features/), [2](https://www.youtube.com/watch?v=t3tCfEySDxI&t=549)]