**Amazon DynamoDB** is ==a fully managed, serverless, **NoSQL database service** designed to deliver fast, highly predictable **single-digit millisecond performance** at any scale==. Unlike traditional relational databases that store data in rigid rows and columns, DynamoDB uses a flexible key-value and document data model that dynamically handles massive operational scale.

Because it is serverless, you do not provision or manage underlying database server instances. It automatically handles data partitioning, hardware provisioning, security patches, and horizontal scaling.

---

1. Core Architectural Concepts

To model data effectively inside DynamoDB, you must understand its three core structural components:

- **Tables:** A collection of data records. Unlike relational tables, a DynamoDB table does not require a fixed, predefined schema for non-key attributes. Two items in the same table can possess entirely different columns or data types.
- **Items:** An individual data record within a table (similar to a row in a relational database or a document in MongoDB). Each item can handle up to **400 KB** of data.
- **Attributes:** The individual data elements attached to an item (similar to fields or columns). Attributes can be scalar types (strings, numbers, booleans) or nested complex data structures (lists, maps, JSON).

The Crucial Primary Key

Every table must be assigned a **Primary Key** when it is created. This key is used to index and locate data across physical storage nodes:

- **Partition Key (PK):** A single mandatory attribute. DynamoDB passes the PK's value through an internal hashing algorithm to determine which physical storage partition the data belongs to.
- **Sort Key (SK) / Composite Key:** An optional secondary key used in tandem with the Partition Key. When paired, multiple items can share the same PK but must possess unique SK values. This creates a one-to-many relationship layout, physically grouping data together on disk for ultra-fast sorted queries.

---

2. Secondary Indexes: Queries Beyond the Primary Key

By default, you can only look up data instantly using the primary key attributes. To run fast lookups on alternate columns without executing an expensive full table scan, DynamoDB utilizes two types of secondary indexes:

|Attribute|Local Secondary Index (LSI)|Global Secondary Index (GSI)|
|---|---|---|
|**Partition Key Type**|Must use the **same Partition Key** as the base table.|Can use a **completely different Partition Key** and Sort Key.|
|**Sort Key Type**|Must use a different Sort Key than the base table.|Can utilize any attribute as a new Sort Key.|
|**Creation Timing**|Can **only** be created when the table is first built.|Can be added, modified, or deleted at any time dynamically.|
|**Capacity Management**|Shares the throughput capacity of the main table.|Requires its own independently provisioned read/write capacity.|

---

3. Read and Write Capacity Modes Compared

DynamoDB allows you to choose how you are billed for your operational database throughput:

- **On-Demand Capacity Mode:** A completely serverless, pay-as-you-go billing engine. It automatically scales up or down instantly to absorb sharp traffic spikes with zero performance degradation. Best for unpredictable or highly volatile application traffic pipelines.
- **Provisioned Capacity Mode:** You explicitly define the maximum number of **Read Capacity Units (RCUs)** and **Write Capacity Units (WCUs)** your application is permitted to consume per second. This is best for predictable, stable, 24/7 production traffic workloads where you want to minimize running costs by using Auto Scaling rules.

---

4. Advanced Production Capabilities

- **DynamoDB Streams:** A time-ordered sequence of real-time mutations (inserts, updates, deletes) occurring inside your table. When a change happens, the stream can instantly trigger an **AWS Lambda function** to perform downstream microservice work (e.g., sending a confirmation email when a new user item is added) [Lambda].
- **Global Tables:** A fully managed, multi-region, active-active database replication framework. You can deploy identical copies of your DynamoDB table across multiple geographic AWS Regions. Changes written to a table in London are automatically replicated to tables in Tokyo and Virginia within seconds, providing ultra-low latency local access for international users and robust disaster recovery safety.
- **Time to Live (TTL):** An automated cleanup setting where you specify a timestamp attribute on your items. Once the current clock passes that timestamp, DynamoDB automatically deletes the item from your table within 48 hours for **free**, ensuring your table space doesn't accumulate bloat or drive up storage costs.