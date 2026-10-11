An **AWS IAM Group** is ==a collection of IAM users== [IAM users]. Groups allow you to specify permissions for multiple users simultaneously, making it significantly easier to manage and audit access across your organization [Access control concepts, IAM users].

Instead of attaching individual permission policies to every single developer or application account, you attach the policies directly to the **IAM Group** [Access control concepts, IAM users]. Any user added to that group instantly inherits those exact permissions [IAM users].

---

1. Group-Based Permission Architecture

Implementing groups eliminates security fragmentation and enforces consistency across your team roles:

```
                  ┌──> [ Group: Security-Auditors ] ──> Attach Policy: SecurityAudit ──> Inherited by: Dave, Ellen
                  │
[ IAM Policies ] ─┼──> [ Group: Developers ] ────────> Attach Policy: AmazonEC2Full  ──> Inherited by: Alice, Bob
                  │
                  └──> [ Group: Billing-Admins ] ─────> Attach Policy: AWSBillingReadOnly ──> Inherited by: Charlie
```

- **Centralized Modification:** If your development team suddenly needs access to a new service (like Amazon Aurora) [Amazon Aurora], you append that single permission rule to the `Developers` group policy. All 50 developers inside that group instantly receive the new capability without you touching 50 individual user files.
- **Seamless Offboarding and Onboarding:** When a new engineer joins the company, you create their **IAM User** identity and drop them into the `Developers` group [IAM users]. They are fully configured to work immediately. If an engineer changes departments, you simply pull them out of one group and place them into another; their access privileges transition instantly [IAM users].
    

---

2. Strict Structural Characteristics of Groups

To model your identity structure correctly, you must operate within several explicit IAM rules:

- **Not a True Identity:** An IAM Group cannot be identified as a `Principal` inside an S3 Bucket Policy or a trust policy [Bucket policies]. Policies are inherited by the users _inside_ the group, but the group itself cannot "log in" or sign API requests [Bucket policies, IAM users].
- **No Nesting Allowed:** IAM Groups cannot contain other groups. A group can only contain individual **IAM Users** [IAM users]. You cannot make a master group called `Engineering` and nest a subgroup called `DevOps` inside it.
- **Multi-Group Membership:** An individual IAM user can belong to **multiple groups concurrently** (up to 10 groups by default). For example, a senior engineer might belong to both the `Developers` group and the `Security-Auditors` group, accumulating the permissions of both.
- **Default Baseline:** New groups contain **zero permissions** by default. They block all interactions until a JSON IAM Policy is explicitly attached to them [Access control concepts, IAM users].

---

3. Essential Security Best Practices

4. **Align Groups to Job Functions (RBAC):** Build your groups to mirror actual job functions within your company (e.g., `sysadmins`, `database-operators`, `billing-viewers`, `interns`) [Access control concepts].
5. **Enforce Least Privilege at the Group Level:** Do not hand out broad administrative privileges to a group just to make configuration easier. Use narrow, job-specific managed policies [Access control concepts].
6. **Audit Memberships Regularly:** Periodically review group rosters to ensure that developers who have shifted projects or left the organization are promptly pruned from highly privileged groups.