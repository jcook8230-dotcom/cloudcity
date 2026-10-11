In cloud security and software architecture, **Access Control** is ==the foundational framework that dictates who can access your system, what resources they can interact with, and what specific actions they are permitted to perform==.

Access control operates as a sequential two-step security gate: **Authentication** followed by **Authorization**.

```
[ Incoming Request ] ──> [ Authentication: Who are you? ] ──> [ Authorization: What can you do? ] ──> [ Access Granted/Denied ]
```

---

1. The Two Pillars: Authentication vs. Authorization

- **Authentication (AuthN):** The process of **verifying an identity**. It answers the question, _"Who are you?"_ Security systems verify identities using credentials such as usernames/passwords, API keys, digital certificates, or Multi-Factor Authentication (MFA) tokens.
- **Authorization (AuthZ):** The process of **verifying permissions**. It answers the question, _"Now that I know who you are, what are you allowed to do?"_ This layer evaluates the access rules attached to that identity to permit or reject a specific action.

---

2. Primary Access Control Frameworks

Modern architectures rely on three primary methodologies to organize and enforce authorization logic:

Role-Based Access Control (RBAC)

Permissions are assigned to specific operational roles rather than individual users. Users are then assigned to one or more roles.

- **How it works:** A user belongs to the `Billing-Admin` group. That group has access to financial dashboards. If the user changes departments, you simply remove them from that group.
- **Best Used For:** Coarse-grained, structural organization permissions based on job functions.

Attribute-Based Access Control (ABAC)

An advanced, dynamic model that evaluates permissions in real-time based on attributes (tags or characteristics) associated with the user, the resource, and the current environment.

- **How it works:** An access rule states: _"Allow engineers to modify databases **only if** the User's Department matches the Resource's Department Tag, **and** the current time is between 9:00 AM and 5:00 PM."_
- **Best Used For:** High-scale environments requiring fine-grained, context-aware security boundaries without creating hundreds of individual roles.

Discretionary Access Control (DAC) vs. Mandatory Access Control (MAC)

- **DAC (Owner-Controlled):** The creator or owner of a resource has full discretion to pass access rights along to others. This is how traditional file systems and legacy cloud Access Control Lists (ACLs) operate [Objects, Object ownership].
- **MAC (System-Enforced):** A centralized authority assigns strict security clearances (e.g., Public, Secret, Top Secret). Users cannot alter permissions; the system matches user clearance levels strictly to resource classification levels to permit access.

---

3. Access Control Layers Compared

To secure a cloud architecture, access control is enforced at two distinct boundaries—either directly on the identity performing the work, or on the resource holding the data:

|Control Type|Definition|Cloud Implementation Example|Best Use Case|
|---|---|---|---|
|**Identity-Based**|Policies are attached directly to a **user, group, or role** to dictate their global permissions.|AWS IAM Policies [IAM Policy for S3 Bucket]|Managing what actions a developer or microservice can perform across the entire platform.|
|**Resource-Based**|Policies are attached directly to a **specific storage or compute asset** to dictate who can enter.|S3 Bucket Policies [Bucket policies]|Securing sensitive data containers regardless of who is trying to access them [Bucket policies].|

---

4. Core Security Principles to Live By

- **The Principle of Least Privilege (PoLP):** Users and applications should only be granted the absolute minimum levels of access necessary to complete their specific job functions, and nothing more. This mitigates the blast radius if a credential is compromised.
- **The Explicit Deny Rule:** In modern secure evaluation engines, **an explicit Deny always overrules an Allow** [Bucket policies]. If a user is globally authorized to read a database, but a local resource policy explicitly denies their specific IP address, the connection is instantly dropped [Bucket policies].