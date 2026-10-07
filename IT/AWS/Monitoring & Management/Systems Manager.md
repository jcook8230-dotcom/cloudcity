**AWS Systems Manager (SSM)** ==provides a unified platform to view and control your infrastructure, allowing you to automate operational tasks and manage software compliance across Amazon EC2 instances, on-premises servers, and virtual machines in hybrid environments==. Its **Automation** and **Patch Manager** features eliminate the need for manual script execution or direct server access. [[1](https://aws.amazon.com/systems-manager/faq/), [2](https://aws.amazon.com/marketplace/pp/prodview-owx3kiwhmq2qo), [3](https://www.capterra.com/p/234696/AWS-Systems-Manager/)]

---

Core Automation & Patching Components

|Feature / Tool|Pricing Model|Core Purpose|
|---|---|---|
|**Patch Manager**|**Free** (For standard AWS managed nodes)|Automates OS and software patch scanning and installation.|
|**Quick Setup Patch Policy**|**Free** (Pay for underlying S3/logs)|Centrally configures patch compliance across accounts and regions.|
|**Automation Runbooks**|**Free tier** (100k steps/mo, nominal fees beyond)|Orchestrates complex IT workflows, AMI updates, and remediation.|
|**Run Command**|**Free**|Remotely executes administrative commands at scale.|

---

How Patch Manager Operates

- **Patch Baselines:** Define rules for which security and bug-fix updates are approved or rejected automatically for different operating systems. [[1](https://aws.amazon.com/blogs/mt/patching-your-windows-ec2-instances-using-aws-systems-manager-patch-manager/)]
- **Maintenance Windows:** Schedule patching operations during low-traffic periods to minimize application disruption. [[1](https://aws.amazon.com/marketplace/pp/prodview-owx3kiwhmq2qo)]
- **Compliance Dashboard:** Aggregates real-time data showing which instances are compliant, missing critical updates, or failing patch installation. [[1](https://aws.amazon.com/blogs/mt/patching-your-windows-ec2-instances-using-aws-systems-manager-patch-manager/)]
- **Quick Setup:** Deploys automated daily scanning and weekly installation routines across an entire [AWS Organizations](https://aws.amazon.com/organizations/) hierarchy using automated [AWS CloudFormation StackSets](https://aws.amazon.com/cloudformation/). [[1](https://aws.amazon.com/video/watch/6d5ece9fe39/), [2](https://aws.amazon.com/de/video/watch/6d5ece9fe39/)]

---

How Systems Manager Automation Operates

- **Runbooks:** Declarative JSON or YAML templates containing sequential or branching steps to perform routine infrastructure maintenance.
- **Event-Driven Remediations:** Integrate with [Amazon EventBridge](https://aws.amazon.com/eventbridge/) and [Amazon Inspector](https://aws.amazon.com/inspector/) to automatically trigger runbooks when security vulnerabilities or operational anomalies are detected.
- **Rate Controls:** Limit concurrency and specify error thresholds so updates roll out safely across a small percentage of your server fleet before affecting production. [[1](https://docs.aws.amazon.com/systems-manager/latest/userguide/patch-manager.html), [2](https://aws.amazon.com/blogs/mt/patching-your-windows-ec2-instances-using-aws-systems-manager-patch-manager/), [3](https://aws.amazon.com/blogs/mt/automate-vulnerability-management-and-remediation-in-aws-using-amazon-inspector-and-aws-systems-manager-part-1/)]