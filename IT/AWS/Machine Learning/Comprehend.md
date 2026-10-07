**Amazon Comprehend** is ==a fully managed Natural Language Processing (NLP) service that uses machine learning to extract structure, meaning, and insights from unstructured text==. It eliminates the need to build, train, or host custom language models from scratch by providing pre-trained APIs that parse sentiment, entities, language, and syntax instantly. [[1](https://www.youtube.com/watch?v=tsPkMcA88GA), [2](https://www.youtube.com/watch?v=jR-ZQRglcfY), [3](https://medium.com/@nuwan.thuduwage/amazon-comprehend-service-unlocking-insights-from-unstructured-text-with-managed-nlp-on-aws-14960d24903e)]

---

Core Capabilities & Pricing Structure

|Feature / Capability|Standard Unit Pricing (Baseline)|Description|
|---|---|---|
|**Standard NLP APIs**|**$0.0001 per unit** (~$1.00 per 1M characters, 300-char min)|Detects sentiment, key phrases, dominant language, and syntax.|
|**PII Detection & Redaction**|**$0.000002 to $0.0001 per unit**|Identifies and masks Personally Identifiable Information (PII).|
|**Custom Models**|**$3.00/hour training** + $0.50/mo storage + endpoint fees|Trains custom entity recognizers or text classifiers on proprietary business data.|
|**Medical Analysis**|**$0.01 per unit** (Comprehend Medical)|HIPAA-eligible extraction of medical entities and ontology mapping.|

_Note: The AWS Free Tier covers **50,000 units of text (5 million characters) per API per month** for the first 12 months on standard features._ [[1](https://aws.amazon.com/comprehend/pricing/)]

---

How Amazon Comprehend Operates

- **Sentiment Analysis:** Categorizes text into `Positive`, `Negative`, `Neutral`, or `Mixed` alongside explicit confidence scores for each state. [[1](https://k21academy.com/ai-ml/amazon-comprehend/), [2](https://www.scaler.com/topics/aws/amazon-comprehend/)]
- **Entity & Key Phrase Recognition:** Identifies named items like people, locations, dates, and commercial products, while extracting major contextual phrases. [[1](https://www.bdrshield.com/blog/what-is-aws-comprehend-natural-language-processing-in-aws/), [2](https://medium.com/@nuwan.thuduwage/amazon-comprehend-service-unlocking-insights-from-unstructured-text-with-managed-nlp-on-aws-14960d24903e)]
- **PII Governance:** Scans logs, customer feedback, and forms to flag or redact sensitive information (such as credit card numbers and addresses) to satisfy data compliance mandates. [[1](https://www.scaler.com/topics/aws/amazon-comprehend/), [2](https://k21academy.com/ai-ml/amazon-comprehend/)]
- **Real-Time vs. Batch Workloads:** Supports synchronous JSON API calls for immediate text responses (like live chat or ticket routing) and asynchronous Amazon S3 batch jobs for processing millions of archived documents.
    
    [[1](https://k21academy.com/ai-ml/amazon-comprehend/), [2](https://medium.com/@nuwan.thuduwage/amazon-comprehend-service-unlocking-insights-from-unstructured-text-with-managed-nlp-on-aws-14960d24903e)]