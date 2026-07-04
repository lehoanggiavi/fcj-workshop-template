---
title: "Sharing and Feedback"
date: 2026-04-19
weight: 7
chapter: false
pre: " <b> 7. </b> "
---

During my internship and the process of preparing the report in the form of a **Workshop Website**, I had the opportunity to better understand how a cloud project is presented, implemented, and evaluated. Instead of only writing a traditional text report, building a website required me to think more clearly about content structure, implementation flow, and how others could read or follow the project.

My project is **credit card fraud detection using Machine Learning on AWS**. This topic helped me connect many areas of knowledge: data, Machine Learning, cloud architecture, real-time processing, alerting, logging, and cost optimization.

## 1. Overall evaluation of the program

I consider the internship program a valuable experience because it did not only require learning AWS theory, but also aimed at building a clearly structured personal project.

Through the project, I better understood that a real-world cloud solution does not consist of only a single service. For the Fraud Detection problem, the system needs multiple components working together:

- Amazon S3 to store the dataset, model artifacts, and prediction history.
- Amazon SageMaker to train and deploy the model.
- API Gateway and Lambda to receive and process real-time requests.
- Kinesis to ingest the transaction stream.
- SNS to send alerts when Fraud is detected.
- Firehose to store prediction history in S3.
- CloudWatch to support logging and debugging.

The most valuable point to me is that the program helped me view the project from an end-to-end perspective, from idea to architecture, from data to deployment, and from deployment to reporting.

## 2. Learning and working environment

The internship environment gave me the opportunity to practice proactiveness. While working on the Fraud Detection project, there were many concepts I did not fully understand at first, such as IAM Role, SageMaker Endpoint, real-time inference, or how Hugo renders Markdown into a website.

Having to self-study, note unclear parts, and gradually add them to the report helped me learn in a more practical way. I did not only read definitions, but also had to ask questions:

- Where does this service fit in the pipeline?
- What are the input and output of each step?
- If someone follows the workshop, what do they need to prepare?
- Which images should be captured to prove the deployment step?
- Which resources may incur costs and need cleanup?

These questions helped me understand the nature of the project more clearly instead of merely listing AWS services.

## 3. Relevance to my major and personal direction

The project fits my learning direction because it combines **Machine Learning** and **Cloud Engineering**. Previously, when studying Machine Learning, I often focused on the model, train/test data, and evaluation results. Through this project, I realized that in practice, the model is only one part of the system.

For a model to be used in a real-world system, many other components are needed:

- A place to store input data.
- A way to package the model.
- An endpoint to serve inference.
- An API to receive external requests.
- A real-time processing mechanism.
- Alerts when abnormalities are detected.
- Storage for result history for later analysis.
- Log monitoring and cost control.

This gave me a more complete view of the lifecycle of an ML system on the cloud.

## 4. What I was most satisfied with

What I was most satisfied with is that I built my own project direction instead of only modifying content from the sample template. At first, the template contained many parts that did not match my personal project, especially older content about VPC Endpoint and PrivateLink. After reviewing it, I gradually adjusted the website content to better align with the Fraud Detection pipeline.

I am also satisfied that the report was organized into clear sections:

- Student Information.
- 12-week Worklog.
- Proposal.
- Blog Posts, including Blog 1, Blog 2, and Blog 3 with complete Vietnamese content.
- Events Participated, updated with two FCAJ Community Day events including main content, lessons learned, and supporting images.
- Technical Workshop.
- Self-evaluation.
- Feedback.

Working section by section helped me check progress more easily and avoid writing off-topic content.

## 5. Difficulties encountered

Some main difficulties during the implementation process included:

### 5.1. Understanding and mapping the technical pipeline correctly

The Fraud Detection pipeline includes many AWS services connected together. If I looked at each service separately, it would be easy to write the report as a list without showing the data flow. Therefore, I needed to divide the system into two parts:

- **Training Zone:** data, preprocessing, training, model artifact, and SageMaker Endpoint.
- **Real-time Zone:** API Gateway, Lambda, Kinesis, Lambda Read Features, SageMaker Endpoint, SNS, Firehose, and S3.

This division made the report clearer and easier to follow.

### 5.2. Converting Markdown content into a website

At first, I did not fully understand how Markdown files in the `content/` folder are rendered by Hugo into a website. After checking with Hugo server, I better understood how the folder structure, `_index.vi.md` files, images in `static/images/`, and `/images/...` paths work.

One practical error I encountered was using a Windows-style image path such as:

```text
E:\aws\fcj-workshop-template\static\images\avatar.jpg
```

The correct path in Markdown should be:

```text
/images/avatar.jpg
```

This error helped me better understand how Hugo handles static files.

### 5.3. Organizing practical supporting images

An initial difficulty was deciding which images were truly necessary for each workshop step. If too many images were inserted, the content would become long and hard to follow; if important steps lacked images, readers would have difficulty imagining the deployment results.

Therefore, I chose to add images for steps with clear evidential value, such as the S3 bucket, Data Lake structure, SageMaker Endpoint, API Gateway endpoint, Lambda, Kinesis Data Stream, SNS email alert, and SageMaker cleanup step. For steps that only involve checking code or short configuration descriptions, I kept the content in text form to avoid making the report overly lengthy.

## 6. Suggestions and improvement proposals

From my personal experience, I have several suggestions:

- There should be a clearer checklist for each report stage: Proposal, Worklog, Workshop, Self-evaluation, and Feedback.
- There should be an example showing how to organize images in Hugo, especially the difference between the `static/images/` folder and the `/images/...` path in Markdown.
- There should be a short guidance session on how to run Hugo locally so students can visually check the website before submission.
- Students should be encouraged to clearly state the scope that has been implemented, the scope kept at the description level, and the scope that needs further verification, so the report is more transparent and easier to evaluate.
- For projects using AWS services that may incur costs, such as SageMaker Endpoint or Kinesis, cleanup should be emphasized from the beginning.

## 7. Would I recommend the program to friends?

I would recommend the program to friends who are interested in AWS, cloud engineering, or want a personal project to include in a report or portfolio.

The reason is that the program helps learners not only read documentation, but also build a structured product by themselves. When preparing a report as a workshop website, learners need to think more carefully about objectives, architecture, implementation steps, supporting images, testing, and cleanup.

However, I also think participants need to be prepared for a considerable amount of self-learning, because once they move into a personal project, many parts cannot be followed 100% from the template. This is also the difficult part, but it is the part that helps them learn the most.

## 8. Expectations after the program

After the program, I would like to continue developing the Fraud Detection project in a more practical direction:

1. Expand end-to-end testing with multiple Fraud/Normal transaction scenarios.
2. Add a dashboard or summary metrics to monitor prediction results.
3. Further optimize IAM Role and permission policies according to the principle of least privilege.
4. Improve system observability with CloudWatch Logs/metrics.
5. Develop the English version based on the reviewed Vietnamese version.

## 9. Conclusion

Overall, the internship and report-writing process helped me better understand how to turn a Machine Learning idea into a structured cloud system. The Fraud Detection on AWS project helped me practice both technical thinking and the ability to present a workshop so others can read, understand, and implement it again.

The most important lesson I learned is that a good cloud project is not about using many AWS services, but about connecting those services properly to solve the right problem. In this project, the problem is detecting suspicious fraudulent transactions, sending timely alerts, and storing prediction history for later analysis.
