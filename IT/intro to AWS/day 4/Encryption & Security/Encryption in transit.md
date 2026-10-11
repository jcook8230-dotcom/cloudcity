**Encryption in transit** (also called encryption in motion) is ==the security practice of protecting your data while it is actively traveling across a network==.

While encryption at rest protects data sitting on a physical disk, encryption in transit prevents bad actors from intercepting, eavesdropping on, or tampering with your files as they travel between a user and a server, or between different backend services.

---

🌐 The Core Protocol: TLS/SSL

The standard protocol used to secure data in transit across the web is **Transport Layer Security (TLS)** (the modern, secure successor to Secure Sockets Layer, or SSL).

- **HTTPS:** When TLS is applied to web traffic, HTTP becomes **HTTPS**, ensuring that all data sent between a user's web browser and your application is encrypted.
- **Cryptographic Handshake:** Before data is exchanged, the client and server perform a handshake to verify the server's identity using a **Digital Certificate** and negotiate a unique symmetric key to encrypt the session's traffic.

---

🛡️ How AWS Implements Encryption in Transit

AWS provides several tools and services to seamlessly manage certificates and secure data boundaries:

- **AWS Certificate Manager (ACM):** A service that lets you easily provision, manage, and deploy public and private TLS/SSL certificates for use with AWS services. ACM handles the renewal of these certificates automatically so they never accidentally expire.
- **Elastic Load Balancing (ELB):** You can bind an ACM TLS certificate directly to an external Application Load Balancer. The load balancer terminates the secure HTTPS connection from the public internet, decrypts the traffic, and passes it safely to your backend EC2 instances.
- **Amazon CloudFront:** Since CloudFront acts as a Content Delivery Network (CDN) at the edge of the AWS network, it enforces HTTPS connections from users worldwide, securing data right at the closest edge location.
- **Virtual Private Cloud (VPC) Endpoints:** When your private EC2 instances need to communicate with services like Amazon S3 or DynamoDB, traffic normally loops out over the public internet. By using a VPC Endpoint, that traffic stays entirely within the private AWS network isolation, heavily mitigating interception risks.

---

🔀 At Rest vs. In Transit: Quick Comparison

|Attribute|Encryption at Rest|Encryption in Transit|
|---|---|---|
|**Primary Goal**|Protects static data against physical theft or drive exposure.|Protects moving data against network sniffing and MITM attacks.|
|**Primary AWS Tool**|**AWS KMS** (Key Management Service)|**AWS ACM** (Certificate Manager)|
|**Common Protocols**|AES-256 cryptographic standards.|TLS 1.2 / TLS 1.3 protocols.|