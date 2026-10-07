**AWS CodePipeline** is ==a fully managed continuous delivery and workflow orchestration service that automates the build, test, and deploy phases of your release process every time there is a code change==. It coordinates your software delivery workflow across native AWS services and third-party tools so that updates move from source repositories to production consistently. [[1](https://docs.aws.amazon.com/whitepapers/latest/cicd_for_5g_networks_on_aws/cicd-on-aws.html), [2](https://aws.amazon.com/what-is/ci-cd-pipeline/), [3](https://thecloudguru.medium.com/github-actions-vs-aws-codepipeline-which-one-should-you-choose-in-2025-ba0019486aca)]

---

Core Pipeline Types & Pricing

|Pipeline Type|Pricing Model|Key Features|
|---|---|---|
|**V1-Type Pipeline**|**$1.00 per active pipeline/month** (Free for the first 30 days; 1 free active pipeline/month)|Standard stage and action-level configurations; no charge if no new code runs through it.|
|**V2-Type Pipeline**|**$0.002 per action execution minute** (100 free minutes/month included)|Advanced entry conditions, pull request/branch filters, and pipeline-level variables.|

_Note: Storing and accessing artifacts in [Amazon S3](https://aws.amazon.com/s3/) or triggering actions via external services incurs standard separate fees._ [[1](https://aws.amazon.com/codepipeline/pricing/)]

---

How AWS CodePipeline Operates

- **Stages and Actions:** You break your release workflow into logical stages, such as **Source**, **Build**, **Test**, and **Deploy**. Each stage contains specific actions that must pass before the code moves forward. [[1](https://docs.aws.amazon.com/whitepapers/latest/cicd_for_5g_networks_on_aws/cicd-on-aws.html), [2](https://www.youtube.com/watch?v=E-YanBx38Cs), [3](https://aws.amazon.com/what-is/ci-cd-pipeline/)]
- **Source Stage Integrations:** Connects to code repositories and storage buckets like [AWS CodeCommit](https://aws.amazon.com/codecommit/), [GitHub](https://github.com/), GitLab, Bitbucket, or Amazon S3 to detect fresh code pushes or tag updates. [[1](https://aws.amazon.com/codepipeline/features/), [2](https://www.youtube.com/watch?v=8cCdnJe8s44), [3](https://www.youtube.com/watch?v=E-YanBx38Cs)]
- **Build and Test Integration:** Passes code artifacts directly to compilation and testing tools like [AWS CodeBuild](https://aws.amazon.com/codebuild/pricing/) or Jenkins to validate software quality. [[1](https://aws.amazon.com/codepipeline/features/), [2](https://www.youtube.com/watch?v=E-YanBx38Cs), [3](https://builder.aws.com/content/3JlaoWiEzshe0qvVFeb0aqVQktK/build-a-cicd-pipeline-with-aws-codepipeline)]
- **Deployment Stage:** Pushes verified application packages out to targets like [AWS CodeDeploy](https://aws.amazon.com/codedeploy/), [Amazon ECS](https://aws.amazon.com/ecs/), [AWS Lambda](https://aws.amazon.com/lambda/), or [AWS CloudFormation](https://aws.amazon.com/cloudformation/). [[1](https://aws.amazon.com/codepipeline/features/)]
- **Manual Approval Gates:** Lets you insert human verification checkpoints before code transitions into sensitive production environments. [[1](https://docs.aws.amazon.com/whitepapers/latest/cicd_for_5g_networks_on_aws/cicd-on-aws.html), [2](https://www.youtube.com/watch?v=E-YanBx38Cs)]