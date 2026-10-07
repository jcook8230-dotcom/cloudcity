**Amazon Athena** is ==an **interactive, serverless query service** that lets you analyze data directly in [Amazon Simple Storage Service (Amazon S3)](https://aws.amazon.com/s3/) using standard **SQL**==. It eliminates the need to manage infrastructure or run complex ETL jobs, charging you purely on a pay-per-query model based on the volume of data read. [[1](https://aws.amazon.com/athena/), [2](https://docs.aws.amazon.com/whitepapers/latest/big-data-analytics-options/amazon-athena.html), [3](https://aws.amazon.com/documentation-overview/athena/)]

---

Core Pricing & Components

|Component / Action|Standard Unit Pricing|Description|
|---|---|---|
|**SQL Data Scanned**|**$5.00 per terabyte (TB)** scanned|Billed per query with a **10 MB minimum** per execution.|
|**DDL Statements**|**Free**|Statements like `CREATE TABLE` or `DROP TABLE` incur no scan fees.|
|**Failed / Cancelled**|**Free** / Partial|Failed queries scanning no data are free; cancelled ones bill what they read.|
|**Provisioned Capacity**|**$0.30 per DPU-hour**|Alternative reservation model for predictable workloads.|

_Note: Storing data in Amazon S3 or cataloging metadata in the [AWS Glue Data Catalog](https://aws.amazon.com/glue/) incurs separate standard service fees._ [[1](https://aws.amazon.com/athena/pricing/)]

---

How Amazon Athena Operates

- **Schema-on-Read:** Projects your table schema onto underlying files at query time rather than requiring upfront data loading.
- **Underlying Engines:** Powered by distributed SQL engines like **Trino and Presto**, supporting ANSI SQL, complex joins, and window functions.
- **File Formats:** Directly queries raw or compressed data formats stored in S3, including **CSV, JSON, ORC, Avro, and Apache Parquet**.
- **Federated Queries:** Extends queries beyond S3 to external stores (like relational databases or [Amazon DynamoDB](https://aws.amazon.com/dynamodb/)) using [AWS Lambda](https://aws.amazon.com/lambda/) data source connectors. [[1](https://aws.amazon.com/blogs/big-data/analyzing-data-in-s3-using-amazon-athena/), [2](https://aws.amazon.com/athena/features/), [3](https://aws.amazon.com/documentation-overview/athena/)]