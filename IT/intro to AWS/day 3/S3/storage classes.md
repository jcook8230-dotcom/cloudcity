**Amazon S3 storage classes** are distinct data tiers designed to optimize your costs based on the data's access frequency, availability requirements, and retention lifecycles. Instead of paying a single premium rate for all data, you match your files to the appropriate storage tier based on how often you need to query or retrieve them.

Every object uploaded to an S3 bucket is assigned a specific storage class, which can be modified manually or automated using **S3 Lifecycle Policies** [Buckets].

---

The 6 Core S3 Storage Classes

1. S3 Standard

The default tier for frequently accessed data. It delivers low latency and high throughput.

- **Best Use Cases:** Active websites, dynamic mobile applications, content distribution networks, and frequently updated big data analytics pipelines.
- **Availability:** Replicated across a minimum of **three physical Availability Zones** within an AWS region.

2. S3 Intelligent-Tiering

An automation engine that **automatically optimizes your storage costs**. It monitors your data's access patterns. If an object is not accessed for 30 consecutive days, it shifts it to an infrequent tier; if it is accessed again, it immediately moves it back to the frequent tier with **zero retrieval fees** or operational overhead.

- **Best Use Cases:** Workloads with completely unpredictable or shifting access patterns, or long-term data lakes where you aren't sure which files are popular.

3. S3 Standard-Infrequent Access (S3 Standard-IA)

Designed for data that is accessed less frequently but requires **instant access** when requested. It offers a lower per-gigabyte storage cost than S3 Standard, but charges a small fee per gigabyte of data retrieved.

- **Best Use Cases:** Critical backups, disaster recovery data repositories, and older corporate documentation that is rarely opened but must load immediately upon request.

4. S3 One Zone-Infrequent Access (S3 One Zone-IA)

Similar to Standard-IA, but stores data within a **single physical Availability Zone** instead of three. This reduces storage costs by an additional 20% compared to Standard-IA, but introduces data loss risk if that specific physical data center experiences a catastrophic failure.

- **Best Use Cases:** Non-critical secondary backups, easily reproducible data, or regional data replicas that are already backed up elsewhere.

5. S3 Glacier Flexible Retrieval (Formerly S3 Glacier)

A low-cost archival tier for data that does not require instant access. Data is stored securely, but retrieval times can range from a few minutes to several hours.

- **Best Use Cases:** Legacy corporate backup retention, digital media archives, and long-term regulatory compliance logs.
- **Retrieval Times:** Supports **Expedited** (1–5 minutes), **Standard** (3–5 hours), or **Bulk** (5–12 hours) retrievals.

6. S3 Glacier Deep Archive

The **lowest-cost storage tier in all of AWS**. It is engineered explicitly for long-term digital preservation of data that is accessed maybe once or twice a year.

- **Best Use Cases:** Strict regulatory compliance data (e.g., healthcare records, financial tax audits) that must be retained for 7–10 years but is rarely touched.
- **Retrieval Times:** Standard retrieval takes up to **12 hours**, while bulk retrieval takes up to **48 hours**.

---

Storage Tiers Metrics Comparison

|Storage Class|Minimum Retention Period|Data Retrieval Fee|Availability Zones|Minimum Object Size|
|---|---|---|---|---|
|**S3 Standard**|None|**None**|≥ 3 AZs|None|
|**S3 Intelligent-Tiering**|None|**None**|≥ 3 AZs|None|
|**S3 Standard-IA**|30 Days|**Per GB Retreated**|≥ 3 AZs|128 KB|
|**S3 One Zone-IA**|30 Days|**Per GB Retreated**|**1 AZ Only**|128 KB|
|**S3 Glacier Flexible**|90 Days|**Per GB Retreated**|≥ 3 AZs|None|
|**S3 Glacier Deep Archive**|180 Days|**Per GB Retreated**|≥ 3 AZs|None|

---

Important Cost Pitfalls to Avoid

- **Minimum Retention Rules:** Archival classes impose mandatory storage clocks. If you move an object to **Glacier Deep Archive** and delete it 10 days later, AWS will still bill you for the remaining **170 days** of storage capacity as an early deletion penalty.
- **Object Sizing Floor:** Infrequent Access classes enforce a minimum billing size of **128 KB**. If you use a lifecycle policy to push millions of tiny 1 KB text files into S3 Standard-IA, AWS will bill _every single file_ as if it is a full 128 KB, which can drastically increase your bill instead of lowering it.![[Pasted image 20261010173531.png]]