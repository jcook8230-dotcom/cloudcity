**AWS CodeDeploy** is ==a fully managed deployment service that automates software releases to compute services such as [Amazon EC2](https://aws.amazon.com/ec2/), [Amazon ECS](https://aws.amazon.com/ecs/), [AWS Lambda](https://aws.amazon.com/lambda/), and on-premises servers==. It removes error-prone manual steps by coordinating application updates and minimizing downtime during production changes. [[1](https://docs.aws.amazon.com/whitepapers/latest/overview-deployment-options/aws-codedeploy.html), [2](https://aws.amazon.com/codedeploy/features/)]

---

Core Deployment Pricing & Targets

|Target Platform / Feature|Pricing Basis|Description|
|---|---|---|
|**AWS Compute Targets (EC2, ECS, Lambda)**|**Free**|No additional charge for code deployments to native AWS compute targets (pay only for underlying resources).|
|**On-Premises Servers**|**$0.02 per instance update**|Billed per successful update instance for non-AWS/hybrid infrastructure.|
|**Storage & Logs**|**Standard S3/CloudWatch rates**|Separate fees for storing revision bundles in [Amazon S3](https://aws.amazon.com/s3/) or logging events.|

---

How AWS CodeDeploy Operates

- **The `appspec.yml` File:** Relies on an application specification file stored in your source revision that defines the deployment instructions, file copy destinations, and lifecycle event hooks. [[1](https://builder.aws.com/content/3JcNEZHVafBQH273jpdGUYTUlUc/aws-codedeploy-a-simple-introduction-to-application-deployment), [2](https://aws.amazon.com/codedeploy/features/)]
- **Deployment Groups:** Organizes your target instances or functions into logical deployment groups (such as `Staging` or `Production`) based on instance tags or Auto Scaling groups. [[1](https://www.pubnub.com/learn/glossary/aws-codedeploy/), [2](https://docs.aws.amazon.com/whitepapers/latest/overview-deployment-options/aws-codedeploy.html)]
- **Deployment Strategies:**
    
    - _In-place:_ Updates the application on existing instances incrementally or all at once.
    - _Blue/Green:_ Provisions a new environment, shifts traffic gradually using canary or linear rules, and retires the old version only after verifying health. [[1](https://aws.amazon.com/codedeploy/features/), [2](https://www.youtube.com/watch?v=tyb7y04c8Xg&vl=en), [3](https://www.youtube.com/watch?v=_c-izSXhHIc)]
    
- **Automated Rollbacks:** Continuously monitors deployment health events and can automatically halt and roll back updates to a previous stable revision if error thresholds are breached. [[1](https://aws.amazon.com/documentation-overview/codedeploy/), [2](https://www.pubnub.com/learn/glossary/aws-codedeploy/)]

---

Ecosystem Integration

CodeDeploy integrates seamlessly into full CI/CD workflows by connecting directly with [AWS CodePipeline](https://aws.amazon.com/codepipeline/) for orchestration and [AWS CodeBuild](https://aws.amazon.com/codebuild/) for artifact creation. [[1](https://docs.aws.amazon.com/whitepapers/latest/overview-deployment-options/aws-codedeploy.html), [2](https://aws.amazon.com/codedeploy/features/)]