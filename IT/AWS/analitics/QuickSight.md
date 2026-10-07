**Amazon QuickSight** is ==a fully managed cloud business intelligence (BI) service that lets you build interactive dashboards, generate AI-driven data stories, and share reports across your organization==. It connects directly to cloud data sources and scales automatically without requiring you to manage underlying servers or clusters. [[1](https://aws.amazon.com/quick/quicksight/), [2](https://aws.amazon.com/documentation-overview/quicksight/)]

---

Core Pricing & User Tiers

|User Role / Plan|Pricing (Enterprise)|Core Capabilities|
|---|---|---|
|**Enterprise Reader**|**$3.00 / user / month**|View interactive dashboards, receive scheduled emails, and access mobile app reports.|
|**Enterprise Reader Pro**|**$20.00 / user / month**|Reader features plus natural-language Q&A and AI executive summaries via Amazon Q.|
|**Enterprise Author**|**$24.00 / user / month**|Connect to data sources, build and publish custom dashboards, and apply row-level security.|
|**Enterprise Author Pro**|**$40.00 – $50.00 / mo**|Author features plus full generative dashboard creation and automated data stories.|
|**Reader Capacity Pricing**|**$250.00 / month**|Bulk session pricing (500 sessions/mo) ideal for customer-facing or embedded analytics.|

---

How Amazon QuickSight Operates

- **SPICE Engine:** Relies on **SPICE (Super-fast, Parallel, In-memory Calculation Engine)** to store and query imported data at high speeds, reducing direct strain on your primary transactional databases. [[1](https://aws.amazon.com/documentation-overview/quicksight/)]
- **Data Connectivity:** Links natively to AWS storage and query tools like [Amazon Simple Storage Service (Amazon S3)](https://aws.amazon.com/s3/), [Amazon Redshift](https://aws.amazon.com/redshift/), and [Amazon Athena](https://aws.amazon.com/athena/), alongside third-party databases via JDBC or direct connectors. [[1](https://www.snowflake.com/en/developers/guides/quickstart-generative-bi-quicksight/), [2](https://saasrat.com/products/amazon-quicksight)]
- **Generative BI & Amazon Q:** Allows users to generate multi-sheet analyses and visualizations using plain conversational text prompts instead of manual drag-and-drop authoring. [[1](https://aws.amazon.com/blogs/machine-learning/generate-dashboards-from-natural-language-prompts-in-amazon-quick/)]
- **Embedded Analytics:** Enables SaaS providers to white-label and embed interactive dashboards directly into custom web applications or customer portals. [[1](https://saasrat.com/products/amazon-quicksight)]