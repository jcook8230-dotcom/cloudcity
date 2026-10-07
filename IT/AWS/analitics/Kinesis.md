**Amazon Kinesis** is ==a cloud-native platform on AWS designed to **capture, process, and analyze real-time streaming data** at any scale==. It allows you to ingest high-velocity information—such as live clickstreams, application logs, financial feeds, and IoT telemetry—and make it available for processing in milliseconds. [[1](https://aws.amazon.com/kinesis/data-streams/), [2](https://aws.amazon.com/kinesis/data-streams/features/), [3](https://en.wikipedia.org/wiki/Amazon_Kinesis)]

---

Core Kinesis Components

|Service / Capability|Primary Function|Key Technical Details|
|---|---|---|
|**Amazon Kinesis Data Streams (KDS)**|Build custom real-time data processing apps and ingest massive data payloads.|Supports On-Demand and Provisioned capacity modes; records up to 10 MiB.|
|**Amazon Data Firehose** _(formerly Kinesis Data Firehose)_|Load streaming data directly into data lakes, warehouses, and analytics stores.|Fully managed, zero storage layer, delivers straight to S3, Redshift, OpenSearch, or Iceberg.|
|**Amazon Managed Service for Apache Flink** _(formerly Kinesis Data Analytics)_|Analyze and transform streaming data in real time using SQL or Java/Flink.|Serverless execution engine with sub-second latency.|
|**Amazon Kinesis Video Streams**|Securely ingest and store video streams for analytics and machine learning.|Handles massive camera feeds from IoT devices, drones, and security systems.|

---

How Amazon Kinesis Data Streams Operates

- **Capacity Modes:** Choose between **Provisioned Mode** (where you manually manage shards) and **On-Demand Mode** (where AWS automatically scales read/write throughput without shard planning). [[1](https://jayendrapatil.com/aws-kinesis-data-streams-vs-kinesis-firehose/), [2](https://www.youtube.com/watch?v=TYKOHj8owIs&vl=en-US&t=579)]
- **Partition Keys:** Routes incoming records to specific shards within a stream using an application-defined partition key (like a user ID or device ID). [[1](https://aws.amazon.com/kinesis/data-streams/getting-started/)]
- **Data Retention:** Retains immutable stream records anywhere from 1 to 365 days, supporting multiple data replays and parallel downstream consumers. [[1](https://aws.amazon.com/kinesis/data-streams/features/), [2](https://www.youtube.com/watch?v=TYKOHj8owIs&vl=en-US&t=579)]
- **Enhanced Fan-Out:** Gives individual consumer applications their own dedicated read throughput (`2 MB/s` per shard) with ultra-low latency (~70 ms), preventing consumer bottlenecks. [[1](https://aws.amazon.com/kinesis/data-streams/features/), [2](https://jayendrapatil.com/aws-kinesis-data-streams-vs-kinesis-firehose/)]

---

Integration Architecture

Kinesis integrates natively with [AWS Lambda](https://aws.amazon.com/lambda/), [Amazon S3](https://aws.amazon.com/s3/), [Amazon Redshift](https://aws.amazon.com/redshift/), and [Amazon DynamoDB](https://aws.amazon.com/dynamodb/) to build complete end-to-end event-driven data pipelines. For deeper implementation guides, see the official [Amazon Kinesis Documentation](https://aws.amazon.com/kinesis/). [[1](https://aws.amazon.com/kinesis/data-streams/features/), [2](https://en.wikipedia.org/wiki/Amazon_Kinesis)]