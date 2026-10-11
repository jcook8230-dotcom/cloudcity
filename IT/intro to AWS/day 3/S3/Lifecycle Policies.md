**S3 Lifecycle Policies** are ==automation rules attached directly to an Amazon S3 bucket that manage your objects over time== [Buckets]. Instead of manually auditing and deleting files, a lifecycle policy automatically transitions data to cheaper storage tiers or permanently deletes it based on the object's age or specific metadata tags [Buckets, Storage classes].

They are the primary mechanism used to control cloud costs and enforce corporate data retention regulations.

---

The 2 Primary Types of Lifecycle Actions

A lifecycle policy executes two distinct types of automated behaviors:

1. Transition Actions

These actions define when to move your objects between different **S3 Storage Classes** to optimize costs as the data ages [Storage classes].

- **Example Pipeline:** Automatically shift an object from **S3 Standard** to **S3 Standard-Infrequent Access (IA)** after 30 days of inactivity, then move it down to **S3 Glacier Deep Archive** after 90 days [Storage classes].

2. Expiration Actions

These actions dictate when objects should be permanently deleted or cleaned up.

- **Example Pipeline:** Automatically purge temporary application logs or test data exactly 14 days after creation, or permanently delete compliance documents after 7 years.

---

Structural Behavior: Current vs. Noncurrent Versions

If you have **S3 Versioning** enabled on your bucket, lifecycle policies expand to handle historical files independently from live files [Versioning]:

|Object State|Lifecycle Target|Practical Automation Strategy|
|---|---|---|
|**Current Version**|The live, active file.|Transition to cold storage tiers or schedule a soft delete (which inserts a Delete Marker) [Versioning].|
|**Noncurrent Version**|Older variants hidden underneath [Versioning].|Move historical data to **S3 Glacier** quickly [Storage classes, Versioning]. Permanently delete them after a short window (e.g., 60 days) to prevent cost inflation [Versioning].|

---

Anatomy of a Lifecycle Rule Configuration

When building a lifecycle rule, you define exactly which files are affected using scope filters:

- **Prefix Filters:** Targets objects in a specific mock folder path (e.g., applying the rule _only_ to files starting with `logs/` or `tmp/`).
- **Object Tag Filters:** Targets objects stamped with specific key-value metadata tags (e.g., applying a 7-year retention rule only to files tagged with `Status: Compliance`).
- **Size Filters:** Restricts transitions based on minimum or maximum file sizes (crucial for preventing the 128 KB storage floor cost trap of Infrequent Access tiers) [Storage classes].

---

Sample Lifecycle Timeline

```
[ Object Created ] ──(Day 30)──> [ Transition to Standard-IA ] ──(Day 90)──> [ Transition to Glacier ] ──(Day 365)──> [ Permanent Expiration ]
```

⚠️ Common Design Traps to Avoid

- **The Glacier Retention Floor:** If a lifecycle rule transitions an object to **S3 Glacier Deep Archive** and then expires (deletes) it 30 days later, AWS will still bill you for the remaining **150 days** of storage as an early deletion penalty [Storage classes]. Match your expiration dates to meet minimum retention limits.
- **Multipart Upload Leftovers:** When an application or user uploads a massive file to S3, it breaks it into chunks using a multipart upload. If the upload gets interrupted or fails halfway through, those uploaded chunks stay hidden in the bucket, accumulating standard storage costs indefinitely. Always include the **"Abort Incomplete Multipart Uploads"** action in your lifecycle policies to purge these fragments after a few days.