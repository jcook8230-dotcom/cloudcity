**Amazon EBS** (Elastic Block Store) ==provides high-performance, **persistent block storage volumes** designed for use with Amazon EC2 instances==. Think of an EBS volume as a virtual hard drive in the cloud that you can mount onto a running server.

Unlike local instance storage, EBS volumes are detached from the physical lifecycle of an EC2 instance. If your instance is stopped, rebooted, or terminated, the data on your EBS volume **remains completely intact** and can be reattached to a different instance.

Core Characteristics of EBS

- **Replication Within an AZ:** EBS automatically replicates its data across multiple physical servers within a single Availability Zone (AZ) to prevent data loss from a single hardware failure.
- **Elastic Tuning:** You can dynamically increase volume size, change volume types, or adjust performance (IOPS and throughput) on-the-fly without detaching the volume or interrupting your running applications.
- **Point-in-Time Snapshots:** You can back up your data by taking snapshots of your EBS volumes, which are stored incrementally in Amazon S3. These snapshots can be used to restore volumes or copy data across AWS Regions.
- **Built-in Encryption:** EBS supports seamless data-at-rest and data-in-transit encryption using AWS Key Management Service (KMS) with zero performance impact.

---

EBS Volume Types Compared

AWS categorizes EBS volumes into Solid-State Drives (SSD) for transactional workloads and Hard Disk Drives (HDD) for large throughput workloads.

|Volume Type|Volume Code|Primary Metric|Target Workloads & Use Cases|
|---|---|---|---|
|**General Purpose SSD**|**gp3** / gp2|Balanced IOPS / MB/s|System boot volumes, virtual desktops, dev/test environments, and low-latency apps.|
|**Provisioned IOPS SSD**|**io2** / io1|Ultra-low latency IOPS|High-performance, I/O-intensive relational databases (SQL Server, Oracle, PostgreSQL).|
|**Throughput Optimized HDD**|**st1**|High Throughput (MB/s)|Large streaming workloads, big data analytics, log processing, and data warehousing.|
|**Cold HDD**|**sc1**|Lowest Cost per GB|Infrequently accessed data, large file storage, and backup retention pools.|
![[Pasted image 20261010163723.png]]