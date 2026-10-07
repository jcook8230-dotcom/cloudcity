**AWS CodeBuild** is ==a fully managed continuous integration (CI) service that automatically compiles source code, runs tests, and packages software artifacts in the cloud without requiring you to provision or manage physical build servers==. It spins up fresh, isolated container environments for every job, ensuring repeatable and consistent builds. [[1](https://aws.amazon.com/codebuild/faqs/), [2](https://www.youtube.com/watch?v=aGLXfb21Khs&t=27), [3](https://www.youtube.com/watch?v=nKZtS3dgF2k&t=83)]

---

Core Compute Options & Pricing

|Compute Mode / Type|Pricing Basis|Free Tier Allowance|Description|
|---|---|---|---|
|**On-Demand EC2 (Small)**|**~$0.005 per minute**|**100 build minutes/month** (`general1.small`)|Standard container runtime for general builds.|
|**On-Demand EC2 (Larger)**|Varies by vCPU/memory tier|None|High-memory or GPU instance configurations for heavy compiling or ML.|
|**AWS Lambda Compute**|**Pay-per-second billing**|**6,000 build seconds/month** (1GB size)|Short-lived, ultra-fast start-up builds with zero queue waiting.|

_Note: Storing output packages in [Amazon S3](https://aws.amazon.com/s3/) or streaming logs to [Amazon CloudWatch](https://aws.amazon.com/cloudwatch/) incurs separate standard service fees._ [[1](https://aws.amazon.com/codebuild/pricing/)]

---

How AWS CodeBuild Operates

- **Source Retrieval:** Pulls project files dynamically from integrated repositories like [AWS CodeCommit](https://aws.amazon.com/codecommit/), GitHub, Bitbucket, or Amazon S3. [[1](https://aws.amazon.com/codebuild/faqs/)]
- **The `buildspec.yml` File:** Relies on a declarative YAML recipe stored in your repository root that explicitly outlines sequential phases—`install`, `pre_build`, `build`, and `post_build`. [[1](https://www.youtube.com/watch?v=aGLXfb21Khs&t=27)]
- **Execution Containers:** Runs commands inside ephemeral Docker containers using pre-configured runtimes for Python, Node.js, Java, Go, and Android, or via custom Docker images hosted in [Amazon ECR](https://aws.amazon.com/ecr/). [[1](https://aws.amazon.com/blogs/aws/aws-codebuild-fully-managed-build-service/), [2](https://www.youtube.com/watch?v=aGLXfb21Khs&t=27)]
- **Artifact Delivery:** Uploads compiled binaries, zip archives, or container images directly into designated target buckets or registries, then mathematically secures data at rest via [AWS KMS](https://aws.amazon.com/kms/). [[1](https://aws.plainenglish.io/aws-codebuild-in-plain-english-your-automated-build-and-test-lab-in-the-cloud-b1027a4f5dc3)]