A **Bucket Policy** is ==a resource-based **AWS Identity and Access Management (IAM) policy document written in JSON** that you attach directly to an Amazon S3 bucket== [Buckets]. It allows you to grant or restrict access permissions to the bucket and the objects inside it, making it one of the most powerful tools for enforcing data governance and security boundaries [Buckets].

While standard IAM policies are attached to _users, groups, or roles_ to dictate what they can do, a Bucket Policy is attached to the _storage container itself_ to dictate **who can interact with that specific bucket**.

---

Anatomy of a Bucket Policy JSON

Every bucket policy is structured using a standard set of structural JSON elements:

json

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowPublicReadForWebsite",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::my-corporate-website-bucket/*"
    }
  ]
}
```

Use code with caution.

- **Version:** The IAM policy language version (always use `"2012-10-17"`).
- **Statement:** A container array holding one or more individual rule statements.
- **Sid (Statement ID):** An optional, human-readable label or description for the rule.
- **Effect:** Dictates whether the rule should **`Allow`** or **`Deny`** the requested action.
- **Principal:** Specifies _who_ the rule applies to (e.g., a specific IAM user account, an external AWS account, a federated role, or `*` meaning everyone/public).
- **Action:** The specific S3 operations being permitted or blocked (e.g., `s3:GetObject` to download files, `s3:PutObject` to upload files, or `s3:ListBucket` to look inside).
- **Resource:** The exact bucket or path within the bucket being targeted, expressed as an **Amazon Resource Name (ARN)** (e.g., `arn:aws:s3:::bucket-name/*`).

---

Common Production Use Cases

1. Enforcing Server-Side Encryption (Cost & Compliance Control)

You can write an explicit `Deny` policy that automatically rejects any file upload request (`s3:PutObject`) if the incoming request payload doesn't explicitly include the headers mandating data encryption [Encryption]:

json

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "DenyUnencryptedUploads",
      "Effect": "Deny",
      "Principal": "*",
      "Action": "s3:PutObject",
      "Resource": "arn:aws:s3:::my-secure-data-bucket/*",
      "Condition": {
        "StringNotEquals": {
          "s3:x-amz-server-side-encryption": "AES256"
        }
      }
    }
  ]
}
```

Use code with caution.

2. Restricting Access to a Specific VPC Endpoint

To prevent data exfiltration, you can lock a bucket down so that it _only_ accepts connections originating from a dedicated **VPC Endpoint** inside your private enterprise network [VPC endpoints]. Anyone attempting to access the bucket over the public internet is instantly blocked:

json

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "RestrictToVpceOnly",
      "Effect": "Deny",
      "Principal": "*",
      "Action": "s3:*",
      "Resource": [
        "arn:aws:s3:::my-private-data-bucket",
        "arn:aws:s3:::my-private-data-bucket/*"
      ],
      "Condition": {
        "StringNotEquals": {
          "aws:sourceVpce": "vpce-0123456789abcdef0"
        }
      }
    }
  ]
}
```

Use code with caution.

3. Locking Down Access to CloudFront (Origin Access Control)

When hosting a website, you often want users to access files strictly through your global **CloudFront CDN** for speed and web application firewall security [CloudFront]. A bucket policy using **Origin Access Control (OAC)** allows you to grant read access _only_ to your specific CloudFront distribution ARN, closing off direct public access to your underlying S3 files [CloudFront].

---

IAM Policies vs. Bucket Policies: When to Use Which

|Access Layer|Managed IAM User Policy|S3 Bucket Policy|
|---|---|---|
|**Attachment**|Attached to an **IAM identity** (User, Group, Role).|Attached directly to the **S3 Bucket** [Buckets].|
|**Control Style**|Centralized asset control ("What can _this user_ do across AWS?").|Localized data containment ("Who can access _this specific bucket_?").|
|**Cross-Account**|Cannot grant access to users in _other_ AWS accounts.|**Can grant cross-account access** to external organizations natively.|

---

⚠️ The Explicit Deny Golden Rule

In the AWS evaluation logic, **an explicit Deny always wins over an Allow**. If an IAM user has a policy that explicitly grants them full administrative rights to everything in S3, but your Bucket Policy has a rule that explicitly blocks their IP address or account from accessing that bucket, **they will be completely blocked**.

Be exceptionally careful when writing `Deny` rules with a wildcard principal (`*`), as you can accidentally lock your own root or administrative accounts out of a bucket if your conditions are not carefully structured.