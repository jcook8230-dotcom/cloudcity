**AWS Trusted Advisor** is an automated cloud optimization tool that evaluates your AWS environment against corporate operational standards and delivers real-time recommendations across five core categories: ==**Cost Optimization**, **Security**, **Fault Tolerance**, **Performance**, and **Service Limits**==. It provides clear guidance to help you optimize infrastructure, lower expenditures, and close security vulnerabilities.

---

Support Tier Access & Features

|Metric / Capability|Basic & Developer Support|Business & Enterprise Support|
|---|---|---|
|**Available Checks**|**Core checks only** (~7 security and performance checks)|**Full check catalog** (200+ comprehensive checks)|
|**Pricing**|**Free** (Included automatically)|**Included with Support contract** (Based on AWS monthly spend)|
|**API/Automation Access**|No|Yes (Via AWS Support API & Amazon EventBridge)|
|**Trusted Advisor Priority**|No|Yes (Aggregated, expert-reviewed findings for large scale teams)|

---

The Five Recommendation Categories

- **Cost Optimization:** Identifies idle resources, unassociated Elastic IP addresses, underutilized EC2 instances, and detached Amazon EBS volumes to stop you from paying for capacity you aren't using.
- **Security:** Reviews configurations to enforce standard security postures. It flags publicly open S3 buckets, unrestricted ports (like SSH 22 or RDP 3389) open to `0.0.0.0/0`, absent Multi-Factor Authentication (MFA) on root accounts, and exposed IAM access keys.

- **Fault Tolerance:** Evaluates application resilience to maximize uptime. It highlights missing Amazon Route 53 health checks, single points of failure, unconfigured Multi-AZ deployments for Amazon RDS, and missing EBS snapshot backups.
- **Performance:** Targets efficiency bottlenecks. It alerts you to overutilized EC2 instances, misconfigured Amazon CloudFront distributions, high-density DNS record loads, and storage volumes facing IOPS throttling.
- **Service Limits (Service Quotas):** Tracks your infrastructure volume against account caps. It monitors usage for resources like VPCs, EC2 instances, and Elastic Load Balancers, signaling an alert when you cross **80% of your service allocation limit**.

---

Management and Enterprise Scaling

For multi-account architectures, AWS Trusted Advisor integrates directly with **AWS Organizations**. This allows enterprise infrastructure teams to aggregate recommendations from hundreds of member accounts into a single organizational dashboard, preventing configuration drift across the entire business.