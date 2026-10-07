**AWS Cost Explorer** is ==a free, built-in tool in the [AWS Billing and Cost Management Console](https://console.aws.amazon.com/) that lets you visualize, understand, and manage your actual AWS costs and usage over time==. It provides an interactive interface to view historical data, analyze top spending trends, and forecast future expenses based on your real-world usage patterns. [[1](https://aws.amazon.com/aws-cost-management/aws-cost-explorer/), [2](https://aws.amazon.com/aws-cost-management/aws-cost-explorer/features/), [3](https://www.youtube.com/watch?v=AToSIYOKgLg&t=37), [4](https://costgoat.com/pricing/aws-cost-explorer)]

---

Core Pricing & Access Tiers

|Feature / Interface|Pricing|Description|
|---|---|---|
|**Console Interface**|**Free**|View graphs, charts, and pre-configured reports directly in the AWS web portal.|
|**Cost Explorer API**|**$0.01 per request**|Programmatic queries to pull data into custom internal apps (paginated pages count separately).|
|**Hourly Granularity Add-on**|**$0.01 per 1,000 usage records**|Optional paid add-on to track detailed hourly usage for EC2 and other services.|

---

How AWS Cost Explorer Operates

- **Historical Data Range:** Displays up to **13 months of past data** alongside the current month-to-date spending once enabled. [[1](https://docs.aws.amazon.com/cost-management/latest/userguide/ce-what-is.html)]
- **Cost Forecasting:** Projects your expected expenses for the next 3 days/months up to 18 months ahead based on your trailing usage patterns. [[1](https://aws.amazon.com/aws-cost-management/aws-cost-explorer/faqs/)]
- **Filtering and Grouping:** Allows you to break down costs by dimensions like **AWS service**, **Region**, **linked account**, or active **cost allocation tags**. [[1](https://www.youtube.com/watch?v=T2IFij8RNTo&t=277)]
- **Natural Language Analysis:** Integrates with **Amazon Q Developer** so you can ask plain text questions (e.g., "What were my highest-cost services last quarter?") to generate instant answers and automatically update visual charts. [[1](https://aws.amazon.com/aws-cost-management/aws-cost-explorer/)]
- **Cost Comparison Tool:** Automatically detects significant spending variations between any two selected months to spotlight major cost drivers like usage changes, credits, or refunds. [[1](https://aws.amazon.com/about-aws/whats-new/2025/05/aws-cost-explorer-new-cost-comparison-feature/)]