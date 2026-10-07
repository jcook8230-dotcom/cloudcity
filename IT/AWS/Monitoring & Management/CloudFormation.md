**AWS CloudFormation** is a native Infrastructure as Code (IaC) service that ==lets you model, provision, and manage collections of related AWS and third-party resources using declarative text files written in **JSON** or **YAML**==. Instead of manually configuring cloud components via the management console, you define your target architecture in a single template file and let AWS automate the deployment. [[1](https://aws.amazon.com/cloudformation/pricing/), [2](https://docs.aws.amazon.com/prescriptive-guidance/latest/choose-iac-tool/cloudformation.html), [3](https://builder.aws.com/content/3KAn4uaMufTiQfLegU847sfZb1f/infrastructure-as-code-why-use-aws-cloudformation), [4](https://www.quora.com/What-is-AWS-CloudFormation-and-why-is-it-used)]

---

Core Pricing & Components

|Component|Pricing|Description|
|---|---|---|
|**AWS Resource Provisioning**|**Free** (Pay only for underlying resources)|No additional charge for using CloudFormation with standard `AWS::*` or `Alexa::*` namespaces.|
|**Third-Party Registry Extensions**|**$0.0009 per operation** (after 1,000 free/mo)|Fees apply for handler actions on private or third-party resource providers.|
|**Custom Hooks**|**$0.0009 per operation** + duration charges|Cost per invocation for authoring and running non-native compliance hooks.|

---

How AWS CloudFormation Operates

- **Templates:** Reusable text files in JSON or YAML that act as the single source of truth for your infrastructure configuration, declaring parameters, conditions, resources, and outputs. [[1](https://docs.aws.amazon.com/prescriptive-guidance/latest/choose-iac-tool/cloudformation.html), [2](https://docs.aws.amazon.com/whitepapers/latest/develop-deploy-dotnet-apps-on-aws/infrastructure-as-code.html)]
- **Stacks:** Logical units where CloudFormation groups and provisions the resources defined in your template, managing them as a single lifecycle entity. [[1](https://docs.aws.amazon.com/whitepapers/latest/develop-deploy-dotnet-apps-on-aws/infrastructure-as-code.html), [2](https://medium.com/@code.chandrashekhar/aws-cloudformation-infrastructure-as-code-made-simple-f92fc3517ec8)]
- **Change Sets:** Pre-deployment preview mechanism that generates a summary of proposed modifications to a running stack so you can verify resource replacements or deletions before applying changes. [[1](https://docs.aws.amazon.com/prescriptive-guidance/latest/choose-iac-tool/cloudformation.html), [2](https://medium.com/@code.chandrashekhar/aws-cloudformation-infrastructure-as-code-made-simple-f92fc3517ec8)]
- **Automatic Rollbacks:** Built-in safeguard that cancels an operation and restores the environment to its last stable configuration if a deployment or update encounters an error.
    
    [[1](https://docs.aws.amazon.com/prescriptive-guidance/latest/choose-iac-tool/cloudformation.html), [2](https://medium.com/@code.chandrashekhar/aws-cloudformation-infrastructure-as-code-made-simple-f92fc3517ec8)]
- **Drift Detection:** Identifies unmanaged or manual configuration changes made outside of your templates, helping maintain infrastructure consistency. [[1](https://docs.aws.amazon.com/prescriptive-guidance/latest/choose-iac-tool/cloudformation.html), [2](https://www.quora.com/What-is-AWS-CloudFormation-and-why-is-it-used)]