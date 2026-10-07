
**AWS CodeCommit** is ==a fully managed source control service that hosts secure, private [Git](https://git-scm.com/) repositories in the cloud==. It eliminates the need to operate your own hardware or patch self-hosted version control servers while keeping your source code tightly integrated with the AWS ecosystem. [[1](https://docs.aws.amazon.com/codecommit/latest/userguide/welcome.html), [2](https://www.youtube.com/watch?v=Aa34xTlhW7g&t=210)]

---

Core Pricing & Structure

|Metric / Feature|Pricing Policy|Description|
|---|---|---|
|**Active Users**|**First 5 active users free per month**|Billed per active user per month beyond the first 5.|
|**Storage & Requests**|Included in active user fee|Covers repository storage and Git requests within standard limits.|
|**Availability (SLA)**|**99.9% uptime SLA**|Maintained across 29 global AWS regions.|

---

How AWS CodeCommit Operates

- **Availability Status:** Following a temporary restriction period for new customer sign-ups in 2024, AWS CodeCommit returned to full **General Availability (GA)**, allowing new accounts to create repositories immediately via the console, CLI, or API. [[1](https://aws.amazon.com/blogs/devops/aws-codecommit-returns-to-general-availability/)]
- **Local Git Workflow:** Functions like any standard Git provider; you run `git clone`, `git add`, `git commit`, and `git push` from your local machine using standard Git commands. [[1](https://www.youtube.com/watch?v=Aa34xTlhW7g&t=210)]
- **Security and Access Control:** Integrates natively with [AWS IAM](https://aws.amazon.com/iam/) for fine-grained repository permissions and uses [AWS Key Management Service (AWS KMS)](https://aws.amazon.com/kms/) to encrypt all data at rest and in transit. [[1](https://www.youtube.com/watch?v=Aa34xTlhW7g&t=210)]
- **Advanced Features:** Supports branch protections, pull requests, approval rules, and includes Git Large File Storage (**Git LFS**) capabilities. [[1](https://aws.amazon.com/blogs/devops/aws-codecommit-returns-to-general-availability/)]
- **Ecosystem Integration:** Hooks directly into continuous integration tools like [AWS CodePipeline](https://aws.amazon.com/codepipeline/) and [AWS CodeBuild](https://aws.amazon.com/codebuild/) to automate deployments upon every push.
    
    [[1](https://www.youtube.com/watch?v=Aa34xTlhW7g&t=210)]