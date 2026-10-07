**Amazon Polly** is a fully managed AWS cloud service that ==converts plain text or **Speech Synthesis Markup Language (SSML)** into lifelike spoken audio==. It provides over **100 male and female voices** across more than **40 languages and language variants**, enabling developers to build speech-enabled applications with high fidelity and low latency. [[1](https://aws.amazon.com/polly/), [2](https://www.anygen.io/showcase/amazon-polly/index.html)]

---

Core Voice Engines & Pricing

|Engine Type|Unit Price (Per 1M Characters)|Description & Focus|
|---|---|---|
|**Standard**|**$4.00**|Baseline concatenative synthesis option for lower-cost requirements.|
|**Neural (NTTS)**|**$16.00**|Advanced deep learning models providing natural, conversational phrasing.|
|**Generative**|**$30.00**|Billion-parameter transformer model supporting expressive, colloquial, and real-time streaming.|
|**Long-Form**|**$100.00**|Specialized engine engineered for extended narrative style and long-form document reading.|

_Note: Amazon Polly features a free tier allowance (e.g., **5 million characters per month** for Standard and **1 million characters per month** for Neural for the first 12 months)._ [[1](https://texttolab.com/blog/is-amazon-polly-free)]

---

Key Features & Capabilities

- **Bidirectional Streaming API:** Allows real-time text-to-speech generation where clients can stream text (such as tokens from an [Amazon Bedrock](https://aws.amazon.com/bedrock/) LLM) and receive audio chunks simultaneously. [[1](https://aws.amazon.com/blogs/machine-learning/introducing-amazon-polly-bidirectional-streaming-real-time-speech-synthesis-for-conversational-ai/)]
- **Speech Marks:** Generates time-stamped metadata—including sentence boundaries, word timings, and visemes (mouth shapes)—to power synchronized animations or karaoke-style word highlighting in media apps.
    
    [[1](https://www.amazonaws.cn/en/polly/), [2](https://aws.amazon.com/what-is/text-to-voice-software/)]
- **Custom Lexicons & SSML:** Enables developers to control pronunciation, volume, pitch, speaking rate, and special handling of acronyms or abbreviations without incurring extra character costs for the markup tags themselves. [[1](https://www.amazonaws.cn/en/polly/), [2](https://www.anygen.io/showcase/amazon-polly/index.html)]
- **Ecosystem Integration:** Connects natively with [Amazon S3](https://aws.amazon.com/s3/) for audio file storage, [AWS Lambda](https://aws.amazon.com/lambda/) for serverless workflows, and [Amazon Connect](https://aws.amazon.com/config/) for call center IVR prompts. [[1](https://www.amazonaws.cn/en/polly/), [2](https://www.youtube.com/watch?v=XUd5M_mQaA0&t=84)]