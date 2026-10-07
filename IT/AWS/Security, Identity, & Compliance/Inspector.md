**Amazon Inspector** is ==an automated vulnerability management service that continually scans your AWS workloads, container registries, and application code repositories for software vulnerabilities and unintended network exposure==. It provides near real-time discovery and assessment without requiring manual scheduling. [[1](https://aws.amazon.com/inspector/), [2](https://docs.aws.amazon.com/inspector/latest/user/what-is-inspector.html)]

---

Core Scan Types & Metrics

|Workload / Resource|Coverage & Assessment Focus|Pricing Model (US East / Baseline)|
|---|---|---|
|**Amazon EC2**|OS packages, programming language dependencies, network exposure, and CIS Benchmarks|Prorated hourly (~**$0.00174 per instance-hour** for standard)|
|**Amazon ECR**|Enhanced continual container scanning for OS and language packages mapped to running ECS/EKS pods|Per initial push scan (~**$0.09/image**) + rescans|
|**AWS Lambda**|Standard package scanning and optional code analysis for layers and dependencies|Prorated hourly (~**$0.000417 per function-hour** standard)|
|**Code Security**|Static Application Security Testing (SAST) and Software Composition Analysis (SCA) via GitHub/GitLab integration|Per repo scan / CI-CD assessment (~**$0.03/image or artifact**)|

_Note: New accounts receive a **15-day free trial** to evaluate automated discovery and continuous scanning across supported compute types._ [[1](https://aws.amazon.com/inspector/pricing/), [2](https://aws.amazon.com/inspector/faqs/)]

---

How Amazon Inspector Operates

- **Automated Discovery:** Automatically identifies eligible resources across your [AWS Organizations](https://aws.amazon.com/organizations/) environment through a delegated administrator account, eliminating manual target configurations. [[1](https://docs.aws.amazon.com/inspector/latest/user/what-is-inspector.html), [2](https://aws.amazon.com/documentation-overview/inspector/)]
- **Hybrid EC2 Scanning:** Relies on the widespread [AWS Systems Manager (SSM) Agent](https://aws.amazon.com/systems-manager/) for inventory collection while gracefully falling back to agentless EBS snapshots when agents are absent. [[1](https://aws.amazon.com/inspector/features/), [2](https://aws.amazon.com/inspector/faqs/)]
- **Contextual Risk Scoring:** Calculates an explicit severity score by combining standard Common Vulnerabilities and Exposures (CVE) metadata with live environmental factors like exploitability and active network reachability. [[1](https://aws.amazon.com/inspector/features/)]
- **Workflow Automation:** Publishes findings instantly to [Amazon EventBridge](https://aws.amazon.com/eventbridge/) and [AWS Security Hub](https://aws.amazon.com/security-hub/) to trigger automated ticketing or remediation via AWS Lambda. [[1](https://docs.aws.amazon.com/inspector/latest/user/what-is-inspector.html), [2](https://aws.amazon.com/inspector/features/)]