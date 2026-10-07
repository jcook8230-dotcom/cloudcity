**AWS X-Ray** is ==a distributed tracing service that helps developers analyze and debug production, distributed applications, such as those built using a microservices architecture==. It provides an end-to-end view of requests as they travel through your application, allowing you to map underlying components, identify performance bottlenecks, and troubleshoot the root causes of errors.

---

Core Components & Pricing

|Component / Action|Free Tier (Per Month)|Standard Unit Pricing (Beyond Free Tier)|Description|
|---|---|---|---|
|**Trace Ingestion**|**100,000 traces**|**$1.00 per 1 million traces**|Charges based on the volume of traces sent to and stored by X-Ray.|
|**Trace Retrieval**|**1,000,000 traces**|**$0.50 per 1 million traces**|Charges for fetching and viewing trace data via the console or APIs.|
|**Trace Insights**|N/A|**$1.00 per 1 million traces**|Fees for running automated anomaly detection and root-cause analysis.|

---

How AWS X-Ray Operates

- **Segments & Subsegments:** Your application sends data to X-Ray in chunks called **segments**, which represent the work done by a compute resource (like an EC2 instance or Lambda function). Segments can break down further into **subsegments** to track downstream remote calls, database queries, or local function execution blocks.
- **Tracing Header (`X-Amzn-Trace-Id`):** Automatically injects a unique tracing identifier into incoming HTTP request headers. As the request navigates through various services, this header is passed along, allowing X-Ray to stitch separate service logs into a single coherent timeline.
- **Service Maps:** Generates a visual topology graph that maps relationships between your application's components in real time. It uses color-coded indicators to illustrate the percentage of successful requests versus errors (`4xx`) and faults (`5xx`).
- **Sampling Rules:** Allows you to control costs by defining custom sampling algorithms (e.g., record 5% of all standard requests, but 100% of requests heading to a specific critical checkout API endpoint).

---

Integration Architecture

AWS X-Ray integrates natively with computing platforms like **AWS Lambda**, **Amazon ECS/EKS**, **Amazon EC2**, and **AWS App Runner**. It also couples directly with routing layers such as **Application Load Balancers (ALB)** and **Amazon API Gateway** to initiate traces right at the ingress edge of your architecture.