An **AWS IAM Policy** is ==a formal, resource-managing document written in **JSON** (JavaScript Object Notation) that explicitly defines permissions within your AWS ecosystem==. Policies do not grant access on their own; instead, they are attached to identities (IAM Users, Groups, or Roles) or resources (such as S3 Buckets) to dictate **who can perform what actions on which resources** under specific conditions [Bucket policies, IAM groups, IAM users].

By default, everything in AWS is completely blocked (**Implicit Deny**) until an IAM policy explicitly permits an action [Access control concepts].

---

1. Anatomy of an IAM Policy Document

Every IAM policy follows a strict JSON structure containing one or more rule declarations:

json

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "DynamoDBReadAccess",
      "Effect": "Allow",
      "Action": [
        "dynamodb:GetItem",
        "dynamodb:Query"
      ],
      "Resource": "arn:aws:dynamodb:us-east-1:123456789012:table/Orders",
      "Condition": {
        "IpAddress": {
          "aws:SourceIp": "203.0.113.0/24"
        }
      }
    }
  ]
}
```

Use code with caution.

- **Version:** The language framework version. Always specify `"2012-10-17"` [Bucket policies].
- **Statement:** The core block containing the actual permission rule arrays [Bucket policies].
- **Sid (Statement ID):** An optional, descriptive nickname for the rule block [Bucket policies].
- **Effect:** Dictates whether the policy will **`Allow`** or **`Deny`** the specific request [Bucket policies].
- **Action:** The precise API operations or service calls being targeted (e.g., `ec2:RunInstances`, `s3:GetObject`) [Bucket policies].
- **Resource:** The exact AWS assets the actions can touch, defined using an **Amazon Resource Name (ARN)** (e.g., `arn:aws:s3:::my-bucket/*`) [Bucket policies].
- **Condition (Optional):** Extra operational restrictions that must be met for the policy to take effect (e.g., restricting access to a corporate IP range or enforcing Multi-Factor Authentication).

---

2. The 3 Policy Forms Compared

AWS categorizes policies based on how they are authored, managed, and attached across your infrastructure:

|Policy Type|Who Manages It?|Reusable?|Best Use Case|
|---|---|---|---|
|**AWS Managed**|**AWS** (Created, patched, and updated by Amazon).|**Yes** (Can attach to multiple groups or users).|Turnkey setups for common roles (e.g., `AmazonS3ReadOnlyAccess`).|
|**Customer Managed**|**You** (Created and updated inside your account).|**Yes** (Can attach to multiple groups or users).|Corporate baseline architectures with precise, custom job-function paths.|
|**Inline**|**You** (Embedded strictly inside one specific identity).|**No** (Strict 1-to-1 link with its parent object).|Ensuring a unique user or service account never accidentally gets modified.|

---

3. Identity-Based vs. Resource-Based Policies

To enforce tight data containment, policies operate from two distinct architectural perspectives:

- **Identity-Based Policies:** Attached directly to an IAM User, Group, or Role [Bucket policies, Access control concepts]. They specify what that _identity_ is allowed to do globally across the AWS environment [Access control concepts].
- **Resource-Based Policies:** Attached directly to a _storage or compute asset_ itself (e.g., S3 Bucket Policies, KMS Key Policies, SQS Queue Policies) [Bucket policies, Access control concepts]. They specify **who (Principal)** has permission to enter and modify that specific asset [Bucket policies, Access control concepts].

---

4. Evaluation Logic: The Absolute Rule of Deny

When a user or application makes a request to AWS, the evaluation engine parses all applicable identity and resource policies simultaneously using a definitive structural logic:

```
[ Default State: Implicit Deny ] ──> [ Check for Explicit Deny ] ─┬─(Yes)─> [ Request Blocked ]
                                                                  │
                                                                  └─(No)──> [ Check for Explicit Allow ] ─┬─(Yes)─> [ Access Granted ]
                                                                                                          │
                                                                                                          └─(No)──> [ Request Blocked ]
```

1. **Explicit Deny Overrules Everything:** If any policy anywhere in the evaluation loop contains an explicit `"Effect": "Deny"`, **the request is instantly blocked**, overriding any "Allow" rules that might exist elsewhere [Bucket policies, Access control concepts].
2. **No Match Means Blocked:** If no explicit "Allow" matches the incoming request, the user falls back into the default baseline state and is denied access [Access control concepts].