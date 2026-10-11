In cloud architecture and system design, **database backups** are the cornerstone of disaster recovery, data protection, and regulatory compliance. They ensure that if a server fails, database files become corrupted, or an application bug executes a destructive deletion, your data can be restored back to a healthy state.

AWS handles backups differently depending on whether you are utilizing a fully managed database service like **Amazon RDS** or self-managing databases on **Amazon EC2** [Amazon RDS].

---

1. Fully Managed Backups: Amazon RDS

When running relational database engines (like PostgreSQL, MySQL, MariaDB, Oracle, or SQL Server) via Amazon RDS, AWS completely automates your backup pipeline through two concurrent mechanisms [Amazon RDS, PostgreSQL]:

Automated Backups & Point-in-Time Recovery (PITR)

RDS continuously captures your database's transaction logs and updates a storage record daily during a user-defined backup window [Amazon RDS].

- **The Power of PITR:** This allows you to restore your database to **any specific second** within your retention window (e.g., _"Restore the database back to exactly 10:04:15 AM this morning"_), effectively reversing accidental database deletions or system corruption [Amazon RDS, Amazon Aurora].
- **Retention Limit:** You can configure the retention period from **1 to 35 days** [Amazon RDS]. When the retention window closes, old automated backups are deleted automatically by the system [Amazon RDS].
- **Lifecycle Boundary:** If you delete an Amazon RDS database instance, all associated automated backups are **permanently deleted** along with it [Amazon RDS].

Manual Database Snapshots

Snapshots are storage backups triggered explicitly by a user, script, or automated backup schedule [Amazon RDS].

- **Indefinite Retention:** Unlike automated backups, manual snapshots are retained **indefinitely** and are never deleted automatically by AWS [Amazon RDS].
- **Lifecycle Independence:** Manual snapshots **persist completely** even if you destroy the underlying database instance, making them vital for final system archiving [Amazon RDS].

---

2. Managed vs. Manual Backup Lifecycles

|Backup Attribute|Automated Backups (RDS)|Manual Snapshots (RDS)|
|---|---|---|
|**Trigger Mechanism**|Scheduled automatically by AWS during a daily window [Amazon RDS].|Triggered manually via the AWS Console, CLI, or API [Amazon RDS].|
|**Retention Window**|**1 to 35 days maximum** (System purges old logs) [Amazon RDS].|Retained **indefinitely** until you explicitly delete them [Amazon RDS].|
|**Recovery Precision**|**Point-in-Time Recovery** (granular down to the exact second) [Amazon RDS].|Restores strictly back to the minute the snapshot took place [Amazon RDS].|
|**Deletion Behavior**|Erased automatically if the RDS instance is terminated [Amazon RDS].|**Saved completely** even if the parent instance is deleted [Amazon RDS].|

---

3. Serverless Backups: Amazon DynamoDB

For NoSQL architectures utilizing **Amazon DynamoDB**, backups are designed to operate with zero performance impact on live database traffic [DynamoDB]:

- **Continuous Backups (PITR):** Once enabled, DynamoDB automatically backs up your data continuously with a rolling **35-day retention window** [DynamoDB]. You can restore the table back to any point-in-time within those 35 days down to the second [DynamoDB].
- **On-Demand Backups:** Allows you to create full backups of your tables at any time for long-term archiving, which persist until manually deleted [DynamoDB].

---

4. Self-Managed Backups: Databases on EC2

If you run a database natively on a raw virtual machine instance (**Amazon EC2**), you are entirely responsible for your own backup strategy [PostgreSQL, Oracle]:

- **EBS Snapshots:** You back up your data by taking point-in-time snapshots of the underlying **Amazon EBS storage volumes** [EBS]. These snapshots are stored incrementally inside Amazon S3 [EBS].
    
- **Application-Consistent Backups:** To ensure data integrity, you must handle flushing database caches to disk or freezing database write operations (`FLUSH TABLES WITH READ LOCK` in MySQL) _before_ triggering the EBS snapshot. Failing to do so can result in a corrupted backup because the database engine was in the middle of a transaction when the block drive snapshot occurred.
- **Native Tooling:** Alternatively, you must run traditional automated script pipelines utilizing native utilities like `pg_dump` for PostgreSQL or `mysqldump` for MySQL, saving the raw output files into an **Amazon S3 bucket** [PostgreSQL, SQL Server].