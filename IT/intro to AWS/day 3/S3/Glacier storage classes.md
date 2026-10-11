**Amazon S3 Glacier storage classes** are ==secure, durable, and extremely low-cost cloud storage tiers engineered specifically for **data archiving and long-term digital preservation**== [Storage classes]. They are the cheapest storage classes available on AWS, allowing you to store massive amounts of data for fractions of a penny per gigabyte [Storage classes].

Because these tiers are designed for cold storage, they trade instant data access for dramatic cost reductions [Storage classes].

---

The 3 S3 Glacier T3 Tiers Compared

AWS offers three distinct Glacier classes, categorized by how quickly you need your data back when a recovery event occurs:

1. S3 Glacier Instant Retrieval

- **Performance:** Delivers **millisecond retrieval**, identical to S3 Standard [Standard].
- **Best Use Cases:** Medical images, research data, or media assets that are rarely accessed (once or twice a year) but must display instantly to an end-user when requested.
- **Minimum Retention:** 90 days.

2. S3 Glacier Flexible Retrieval (Formerly S3 Glacier)

- **Performance:** Asynchronous retrieval. Data cannot be read instantly [Storage classes]. You must request a restoration job which takes **minutes to hours** [Storage classes].
- **Best Use Cases:** Standard corporate backups, monthly system log retention, and offline media masters.
- **Retrieval Options:**
    - _Expedited:_ 1–5 minutes [Storage classes]
    - _Standard:_ 3–5 hours [Storage classes]
    - _Bulk:_ 5–12 hours (Free retrieval tier) [Storage classes]
- **Minimum Retention:** 90 days [Storage classes].

3. S3 Glacier Deep Archive

- **Performance:** The **lowest-cost tier across all of AWS** [Storage classes]. It requires hours to restore data [Storage classes].
- **Best Use Cases:** Regulatory compliance archives (e.g., healthcare records, financial audits, legal data) that you are legally required to keep for 7–10 years but may never actually read [Storage classes].
- **Retrieval Options:**
    - _Standard:_ Up to 12 hours [Storage classes]
    - _Bulk:_ Up to 48 hours [Storage classes]
- **Minimum Retention:** 180 days [Storage classes].

---

Cost and Structural Breakdown

|Metric|Glacier Instant Retrieval|Glacier Flexible Retrieval|Glacier Deep Archive|
|---|---|---|---|
|**Retrieval Speed**|Milliseconds|1 Minute to 12 Hours [Storage classes]|12 to 48 Hours [Storage classes]|
|**Relative Cost/GB**|$ (Cheap)|\((VeryCheap)\|{}\) (Utterly Fractions of a Cent)||
|**Minimum Storage Time**|90 Days|90 Days [Storage classes]|180 Days [Storage classes]|
|**Retrieval Cost**|Per GB fee applies|Per GB fee applies (except Bulk)|Per GB fee applies [Storage classes]|

---

⚠️ Critical Pitfalls to Avoid in Glacier

Archiving data blindly in Glacier can sometimes lead to unexpected charges if you miss the core guardrails:

- **Early Deletion Fees:** If you push data into **Glacier Deep Archive** and delete or overwrite it 20 days later, AWS will still bill you for the remaining **160 days** as a penalty [Storage classes].

- **Retrieval Math:** While storing data in Glacier is incredibly cheap, downloading it is expensive. If you frequently pull large datasets out of Flexible or Instant Retrieval, your **retrieval fees** can easily eclipse your monthly storage savings [Storage classes].