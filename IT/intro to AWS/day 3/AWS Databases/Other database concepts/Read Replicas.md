**Read Replicas** are ==an architectural feature used to horizontally scale the performance of read-heavy databases== [Amazon RDS, MySQL]. By offloading search and read queries from your primary database instance, they free up the main database to focus exclusively on processing transactional writes [Amazon RDS, MySQL].

In managed cloud environments like **Amazon RDS**, a read replica operates as an active, independent copy of your database instance [Amazon RDS].

---

How Read Replicas Work

When you deploy a read replica, AWS provisions a duplicate database instance using a snapshot of your primary node [Amazon RDS]. From that point forward, the two instances interact through a continuous data pipeline:

```
[ Application Write Traffic ] 
              │
              ▼
┌────────────── Primary Instance ──────────────┐
│  Processes: INSERT, UPDATE, DELETE requests  │
└──────────────────────┬───────────────────────┘
                       │
                       │ (Asynchronous Replication)
                       ▼
┌────────────── Read Replica 1 ────────────────┐ ◄─── [ App Read / Search Traffic ]
│  Processes: SELECT queries, reporting, APIs  │
└──────────────────────┬───────────────────────┘
                       │
                       ▼
┌────────────── Read Replica 2 ────────────────┐ ◄─── [ App Read / Analytics Traffic ]
│  Processes: Heavy business intelligence jobs │
└──────────────────────────────────────────────┘
```

1. **Asynchronous Replication:** Every time your application writes or updates a record on the **Primary Instance**, that modification is copied over a private network pipe to the **Read Replicas** [Amazon RDS]. Because this replication happens **asynchronously** (in the background), the primary database doesn't wait for the replicas to confirm the change before completing your user's write request [Amazon RDS].
2. **Traffic Splitting:** You update your application's database configuration file to route heavy search traffic, analytics pipelines, or mobile app API reads directly to the Read Replicas.

---

Read Replicas vs. Multi-AZ (Standby Replicas)

A common point of confusion is mixing up a Read Replica (performance scaling) with a Multi-AZ Standby Replica (disaster recovery) [Amazon RDS, Multi-AZ]:

|Architectural Attribute|Read Replicas|Multi-AZ Standby Replicas|
|---|---|---|
|**Primary Objective**|**Horizontal Scaling** (Boosts query performance) [Amazon RDS, MySQL].|**High Availability** (Disaster recovery protection) [Multi-AZ].|
|**Replication Mode**|**Asynchronous** (Can experience a brief replication lag) [Amazon RDS, MySQL].|**Synchronous** (Real-time, instantaneous mirroring) [Amazon RDS, Multi-AZ].|
|**Database Access**|**Active Read-Only.** Accessible by your code [Amazon RDS].|**Passive.** Inaccessible until a failover occurs [Amazon RDS, Multi-AZ].|
|**Quantity Limit**|Scale out up to **15 replicas** per database [Amazon Aurora, MySQL].|Strictly **one standby node** per standard deployment [Amazon RDS, Multi-AZ].|
|**Failover Role**|Can be promoted to a primary writer manually or via custom code.|**Automated Failover.** Changes DNS target inside 60–120 seconds [Amazon RDS, Multi-AZ].|

---

Key Operational Capabilities

- **Replication Lag:** Because data transfers asynchronously, replicas can briefly fall behind the primary instance during massive write bursts [MySQL, Multi-AZ]. This time window is known as _Replication Lag_. If your code writes data to the primary instance and immediately tries to read it from a replica a millisecond later, it may encounter "stale data" until the replica updates.
- **Engine-Level Sharing (Amazon Aurora):** In **Amazon Aurora**, replicas do not copy data over the network [Amazon Aurora]. Instead, up to 15 reader replicas **share the exact same underlying storage grid** as the primary writer node [Amazon Aurora]. This completely eliminates replication lag, meaning your readers see updates almost instantly [Amazon Aurora].
- **Promoting a Replica:** If you want to migrate a database to a new region, or if you are running a massive integration test, you can explicitly "Promote" a read replica. This severs the replication link, turns off its read-only restriction, and transforms the replica into a standalone, fully independent read-write database.