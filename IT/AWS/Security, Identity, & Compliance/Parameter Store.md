**SSM Parameter Store** is ==a feature of [AWS Systems Manager](https://aws.amazon.com/systems-manager/) that provides secure, hierarchical storage for configuration data, database connection strings, passwords, and license codes==. It lets you separate your configuration data from your application code and manage secrets centrally.

---

Parameter Tiers and Pricing

|Tier|Monthly Storage Fee|Request Pricing|Key Limits & Features|
|---|---|---|---|
|**Standard Tier**|**Free**|**Free** (No API request charges)|Up to 10,000 parameters per region; max size **4 KB** per parameter.|
|**Advanced Tier**|**$0.05 per parameter/month**|**$0.05 per 10,000 requests** (after standard allowances)|Up to 100,000 parameters; max size **8 KB**; supports advanced parameter policies.|

_Note: Switching a parameter from Standard to Advanced is irreversible once you exceed Standard capacity limits or apply Advanced-only policies._

---

How SSM Parameter Store Operates

- **Hierarchical Organization:** Organizes data using path-based naming conventions (e.g., `/my-application/production/database-url`), making it simple to manage configurations across different environments and services.
- **Encrypted Secure Strings:** Integrates natively with [AWS KMS](https://aws.amazon.com/kms/) to encrypt sensitive data like passwords and API keys at rest using either an account default key or a customer-managed key.
- **Parameter Policies (Advanced only):** Allows you to assign policies to parameters, such as setting an expiration date for temporary credentials, scheduling forced rotations, or triggering notifications when a parameter changes.
- **Automatic Versioning:** Tracks every modification to a parameter, allowing you to easily roll back your application to a previous configuration version if an update causes an issue.

---

Integration Architecture

Parameter Store integrates directly with AWS compute and deployment services, including **Amazon EC2**, **AWS Lambda**, and **Amazon ECS**, allowing applications to fetch config data dynamically via the AWS SDK or SSM Agent. For automated setup, parameters can be provisioned natively inside [AWS CloudFormation](https://aws.amazon.com/cloudformation/) templates.