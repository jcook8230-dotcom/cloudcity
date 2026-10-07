**Amazon Rekognition** is ==a fully managed, deep learning-based computer vision service that extracts rich visual insights, detects objects and scenes, and identifies faces or inappropriate content from images and videos without requiring machine learning expertise==. It works via simple API calls, scaling dynamically to process massive media archives stored in [Amazon S3](https://aws.amazon.com/s3/) or live streams via [Amazon Kinesis Video Streams](https://aws.amazon.com/kinesis/video-streams/). [[1](https://www.metaltoad.com/blog/unlock-powerful-image-and-video-analysis-with-aws-rekognition-meta-toad), [2](https://www.youtube.com/watch?v=67rxQj7DqQ0), [3](https://oneuptime.com/blog/post/2026-02-12-amazon-rekognition-video-analysis/view), [4](https://flypix.ai/amazon-rekognition-tool-review/)]

---

Core Pricing & Operations Structure

|Feature / Service|Standard Unit Pricing (Baseline)|Description|
|---|---|---|
|**Rekognition Image APIs**|**$0.001 per image** (tiers scale down to $0.0004 for high volume)|Synchronous analysis of JPEG/PNG files for labels, faces, and text.|
|**Rekognition Video APIs**|**$0.10 per minute** of video processed|Asynchronous analysis of stored video or Kinesis live streams.|
|**Face Metadata Storage**|**$0.01 per 1,000 faces/month**|Storage for face vector objects used in facial recognition collections.|
|**Custom Labels**|**$1.00 – $4.00 per hour** + training time|Train and host proprietary classifiers for unique business assets.|
|**Face Liveness**|**$0.010 – $0.015 per check**|Biometric verification to prevent identity spoofing.|

_Note: New accounts receive a [Free Tier allowance](https://aws.amazon.com/rekognition/pricing/) covering 5,000 images per month and 1,000 minutes of video analysis per month during the first 12 months._ [[1](https://wring.co/blog/aws-rekognition-pricing-guide)]

---

Key Capabilities & Analysis Types

- **Object, Scene, and Label Detection:** Identifies thousands of common items, landscape styles, activities, and dominant image qualities, returning clear confidence scores and bounding box coordinates. [[1](https://aws.amazon.com/rekognition/image-features/), [2](https://www.youtube.com/watch?v=67rxQj7DqQ0)]
- **Facial Analysis & Search:** Detects faces in frames, estimates demographic attributes (such as age ranges and emotions), and matches vectors against internal secure databases for identity verification. [[1](https://www.metaltoad.com/blog/unlock-powerful-image-and-video-analysis-with-aws-rekognition-meta-toad), [2](https://www.youtube.com/watch?v=67rxQj7DqQ0)]
- **Content Moderation:** Automatically flags explicit, unsafe, or unwanted content in images and video streams to help platforms stay compliant with community guidelines. [[1](https://aws.amazon.com/rekognition/), [2](https://www.youtube.com/watch?v=67rxQj7DqQ0)]
- **Text Detection (OCR):** Extracts printed and handwritten words from product labels, road signs, and social media imagery. [[1](https://flypix.ai/amazon-rekognition-tool-review/), [2](https://www.youtube.com/watch?v=67rxQj7DqQ0)]
- **Custom Labels:** Allows organizations to train models using small sets of proprietary images (as few as a couple of hundred samples) to detect custom assets like brand logos or specialized factory defects.
    
    [[1](https://aws.amazon.com/rekognition/), [2](https://aws.amazon.com/blogs/machine-learning/aws-computer-vision-and-amazon-rekognition-aws-recognized-as-an-idc-marketscape-leader-in-asia-pacific-excluding-japan-up-to-38-price-cut-and-major-new-features/)]