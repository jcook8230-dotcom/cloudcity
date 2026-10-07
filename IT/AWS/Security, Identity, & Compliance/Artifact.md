**AWS Artifact** is a no-cost, self-service audit and compliance portal built into the AWS Management Console that ==provides on-demand access to official security and compliance reports and select legal agreements==. [[1](https://aws.amazon.com/blogs/security/introducing-aws-artifact-speeding-access-to-compliance-reports/), [2](https://trustedinstitute.com/concept/aws-cloud-practitioner/security-and-compliance/aws-artifact/)]

---

Core Portal Components & Pricing

|Feature / Category|Pricing|Description|
|---|---|---|
|**AWS Artifact Reports**|**Free**|Download third-party auditor-issued reports (SOC, ISO, PCI, FedRAMP).|
|**AWS Artifact Agreements**|**Free**|Review, accept, and manage legal/regulatory terms (like a HIPAA BAA).|
|**Third-Party ISV Reports**|**Free**|Access independent software vendor compliance data via AWS Marketplace.|
|**Assurance Assistant**|**Free**|AI-powered capability to generate responses to compliance questions.|

---

How AWS Artifact Operates

- **Artifact Reports:** Provides auditor-verified evidence proving that AWS infrastructure complies with international standards. It includes SOC 1, SOC 2, ISO/IEC 27001, PCI-DSS, and FedRAMP documents. Some confidential files require accepting an online Non-Disclosure Agreement (NDA) before downloading, which generates a unique account-traceable watermark on the PDF. [[1](https://repost.aws/knowledge-center/download-share-artifact-documents), [2](https://www.youtube.com/watch?v=MopzlZBsz5E&t=239), [3](https://trustedinstitute.com/concept/aws-cloud-practitioner/security-and-compliance/aws-artifact/), [4](https://www.youtube.com/watch?v=QihkofOW-Tg)]
- **Artifact Agreements:** Enables organizations to execute compliance contracts directly online. For example, healthcare businesses handling protected health information can review and accept the **Business Associate Addendum (BAA)** for HIPAA compliance, either for a single account or enterprise-wide via [AWS Organizations](https://aws.amazon.com/organizations/). [[1](https://aws.amazon.com/artifact/faq/), [2](https://www.youtube.com/watch?v=MopzlZBsz5E&t=239), [3](https://trustedinstitute.com/concept/aws-cloud-practitioner/security-and-compliance/aws-artifact/)]
- **Customer Compliance Guides (CCGs):** Lightweight reference documents available in the portal that map security configuration recommendations for over 100 AWS services to specific regulatory frameworks like PCI-DSS or HIPAA. [[1](https://aws.amazon.com/blogs/security/customer-compliance-guides-now-available-on-aws-artifact/)]
- **The Shared Responsibility Distinction:** AWS Artifact validates the security _of_ the cloud (AWS's physical data centers, host infrastructure, and managed services). It does not certify that your specific application code, identity management, or resource configurations are compliant. [[1](https://trustedinstitute.com/concept/aws-cloud-practitioner/security-and-compliance/aws-artifact/), [2](https://www.youtube.com/watch?v=MopzlZBsz5E&t=239), [3](https://www.youtube.com/watch?v=QihkofOW-Tg)]