**Amazon Lex** is ==a fully managed artificial intelligence service with advanced natural language models designed to build, publish, and deploy conversational voice and text chatbots into applications==. [[1](https://aws.amazon.com/lex/), [2](https://docs.aws.amazon.com/lexv2/latest/dg/what-is.html)]

---

Core Pricing & Interaction Tiers

|Interaction / Component|Standard Unit Price|Description|
|---|---|---|
|**Text Request**|**$0.00075 per request**|Billed for every typed user input processed by the bot.|
|**Speech Request**|**$0.00400 per request**|Billed for every spoken user input processed in request-response mode.|
|**Streaming Voice**|**$0.0065 per 15-second interval**|Billed for active listening time in continuous back-and-forth voice streams.|
|**Chatbot Designer**|**$0.50 per training minute**|Cost to automatically extract intents and slot types from contact center transcripts.|

_Note: Support for original Amazon Lex V1 concluded in 2025; active architectures rely entirely on Amazon Lex V2._ [[1](https://www.cekura.ai/blogs/amazon-lex-pricing), [2](https://www.voiceflow.com/blog/amazon-lex)]

---

How Amazon Lex Operates

- **Intents and Utterances:** You define the user's goal as an _intent_ (e.g., `BookTrip`) and supply sample phrases or _utterances_ that map to that goal.
    
- **Dialog Management:** Lex automatically prompts users for missing information (_slots_) required to fulfill the active intent.
- **Generative AI Assistance:** Features like assisted slot resolution use integrated foundation models via [Amazon Bedrock](https://aws.amazon.com/bedrock/) to handle varied, unstructured user responses gracefully without manual training tuning.
- **Fulfillment Integration:** Connects directly with [AWS Lambda](https://aws.amazon.com/lambda/) to run custom business logic, query databases, or call external APIs. [[1](https://aws.amazon.com/blogs/machine-learning/building-better-bots/), [2](https://www.youtube.com/watch?v=QEqZILuy8q8&t=57), [3](https://www.geeksforgeeks.org/cloud-computing/what-is-amazon-lex/), [4](https://aws-periodic-table.team-skynet.io/services/lex)]

---

Ecosystem Integration

Amazon Lex integrates natively with [Amazon Connect](https://aws.amazon.com/config/) for cloud contact center voice routing, [Amazon DynamoDB](https://aws.amazon.com/dynamodb/) for data retrieval, and [Amazon CloudWatch](https://aws.amazon.com/cloudwatch/) for monitoring interaction logs. [[1](https://docs.aws.amazon.com/lexv2/latest/dg/what-is.html), [2](https://aws.amazon.com/lex/), [3](https://aws.amazon.com/lex/faqs/), [4](https://www.geeksforgeeks.org/cloud-computing/what-is-amazon-lex/), [5](https://www.voiceflow.com/blog/amazon-lex)]