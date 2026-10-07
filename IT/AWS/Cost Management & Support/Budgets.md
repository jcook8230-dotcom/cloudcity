**AWS Budgets** is ==a cost management tracking service that lets you set custom budgets to track your AWS costs and usage, and automatically alert you when you exceed (or are forecasted to exceed) your defined thresholds==. It functions as a financial guardrail inside the **AWS Billing and Cost Management Console**.

---

Budget Types and Pricing

|Budget Category|Included / Free Allowance|Over-Quota Pricing|
|---|---|---|
|**AWS Budgets (Active)**|**First 200 budgets are free** per account|**$0.02 per day** per additional budget|
|**AWS Budget Actions**|First 5 action executions per month are free|**$0.10 per execution** thereafter|
|**Budget Reports**|Delivered inside standard reports|Standard [Amazon SES](https://aws.amazon.com/ses/) or SNS alert fees apply|

---

How AWS Budgets Operates

- **Budget Tracking Types:**
    - _Cost Budgets:_ Tracks actual or forecasted monetary spend against a specific dollar amount.
    - _Usage Budgets:_ Tracks quantitative consumption metrics (e.g., EC2 instance hours or S3 data data transfer sizes).
    - _RI & Savings Plans Budgets:_ Tracks the utilization and coverage rates of your active Reserved Instances or [AWS Savings Plans](https://aws.amazon.com/savingsplans/).
- **Threshold Triggers:** Allows you to create alerts based on **Actual** spending or **Forecasted** spending. For example, you can trigger an email alert if AWS forecasts that your monthly database spend will cross $500, even if your actual mid-month cost is only $200.
- **Granularity Options:** Budgets can be evaluated on a daily, monthly, quarterly, or annual recurring basis.
- **AWS Budget Actions:** Extends beyond basic alerts to execute automated responses via [AWS Systems Manager](https://aws.amazon.com/systems-manager/) or [AWS IAM](https://aws.amazon.com/iam/). For example, you can configure an action to automatically apply a restrictive IAM policy or shut down specific EC2 instances when a cost threshold is breached.