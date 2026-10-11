An **AWS IAM User** is ==an identity entity created inside your AWS account that represents a specific person or application requiring interaction with AWS resources==. An IAM user consists of a permanent name, a unique set of credentials, and explicitly assigned permissions that dictate exactly what actions they are allowed to perform.

By default, a newly created IAM user possesses **zero permissions** and is completely blocked from accessing your infrastructure until you explicitly attach an access policy [Access control concepts].

---

1. Types of Credentials Natively Managed

To interface with your cloud infrastructure, an IAM user utilizes specific credentials depending on their access path:

- **Console Password:** A standard alphanumeric password combined with Multi-Factor Authentication (MFA) used to log securely into the visual AWS Management Console via a web browser.
- **Access Keys (Access Key ID and Secret Access Key):** Long-lived cryptographic strings used to sign programmatic requests sent via the **AWS CLI**, custom code scripts, or software SDKs.
- **SSH Public Keys:** Used to authenticate secure shell access directly into services like AWS CodeCommit or virtual machine repositories.

---

2. Strategic Identity Design: Users vs. Groups

To prevent security fragmentation, you should never assign access permissions directly to individual IAM users. Instead, implement a **Group-Based Access Model**:

```
[ IAM Policy: AdministratorAccess ] ──> [ IAM Group: DevOps-Team ] ──> [ IAM Users: Alice, Bob, Charlie ]
```

1. **The IAM Group:** A logical collection of multiple IAM users. You attach your permission rules (IAM JSON policies) directly to the Group [Access control concepts].
2. **The IAM User:** Individual developers or applications are added as members inside those groups. They automatically inherit the group's cumulative permission limits [Access control concepts].
3. **The Benefit:** If an engineer leaves the engineering team to join product management, you simply remove their IAM User from the `DevOps-Team` group and add them to the `Product-Managers` group. Their access footprint updates instantly without you editing core infrastructure policy files.

---

3. Structural Security Best Practices

- **Enforce the Principle of Least Privilege (PoLP):** Only grant an IAM user the absolute minimum access scope required to execute their specific job duties [Access control concepts].
- **Mandate Multi-Factor Authentication (MFA):** Require every human IAM user to activate a hardware or virtual MFA device to log into the console, shielding the account from password compromises.
- **Human Users vs. Machine Users (Roles Preferred):**
    - Use IAM Users strictly for **human operators** requiring persistent identities.
    - For applications running _inside_ AWS (like on an EC2 instance), **never** hardcode an IAM User's access keys into your application code. Instead, use an **IAM Role**, which dispenses short-lived, temporary security credentials that rotate automatically, eliminating credential exfiltration risks.