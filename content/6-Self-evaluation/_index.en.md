---
title: "Self-evaluation"
date: 2026-04-19
weight: 6
chapter: false
pre: " <b> 6. </b> "
---

During my internship at **AWS** in the **Cloud Engineering** role, I focused on carrying out my personal project: **building a credit card fraud detection system using Machine Learning on AWS**.

The project required not only Machine Learning knowledge, but also the ability to design cloud architecture, organize data, deploy AWS services, and write workshop documentation so that others can follow the implementation steps.

The main tasks I completed include:

- Analyzing the credit card transaction fraud detection problem.
- Designing a pipeline consisting of a **Training Zone** and a **Real-time Zone**.
- Using Amazon S3 as a Data Lake to store the dataset, model artifacts, and prediction results.
- Presenting the process of training a Random Forest model with Amazon SageMaker.
- Building a real-time flow with API Gateway, Lambda, Kinesis, SageMaker Endpoint, SNS, Firehose, and CloudWatch.
- Writing the report in the form of a Hugo Workshop Website, including worklog, proposal, workshop, blog, events, self-evaluation, and feedback.
- Adding supporting images from the AWS Console for key steps such as S3, SageMaker, API Gateway, Lambda, Kinesis, SNS, and cleanup.

Through the implementation process, I evaluated myself based on the following criteria:

| No. | Criteria | Rating | Comments |
| --- | --- | --- | --- |
| 1 | **Professional knowledge** | Good | I was able to apply knowledge of Python, Machine Learning, and AWS to a practical problem. The report demonstrates the roles of data, model, endpoint, real-time processing, alerting, and logging in an ML system on the cloud. |
| 2 | **Ability to learn** | Good | I proactively learned the AWS services needed for the project, such as S3, SageMaker, Lambda, Kinesis, SNS, Firehose, and CloudWatch. Concepts such as IAM Role, SageMaker Endpoint, and real-time inference were included in the report in the correct usage context. |
| 3 | **Proactiveness** | Good | I proactively built my own project direction instead of relying only on the sample template. When the template content was no longer suitable, I reviewed and adjusted it to align with the Fraud Detection pipeline. |
| 4 | **Sense of responsibility** | Good | I completed the main sections of the report according to the required structure, including student information, worklog, proposal, workshop, blog, events, self-evaluation, and feedback. The content was reviewed multiple times to ensure consistency with the actual project. |
| 5 | **Work discipline** | Fair | I maintained progress by working on the report section by section and reviewing the content after each edit. The point I need to improve is better time management to reduce pressure during the final completion stage. |
| 6 | **Communication and presentation ability** | Good | I presented the content in an easy-to-follow way, clearly separating objectives, architecture, services used, implementation steps, supporting images, and expected results. |
| 7 | **Teamwork / communication** | Fair | During the project and report process, I listened to feedback, adjusted content when it went off track, and prioritized checking each section before moving on. I can improve further by communicating earlier when facing complex technical issues. |
| 8 | **Problem-solving thinking** | Good | I knew how to divide the large problem into smaller parts: data, training, deployment, real-time pipeline, alerting, history storage, and cleanup. When the website did not match the project or image paths were incorrect, I identified the causes and fixed them according to the Hugo structure. |
| 9 | **Tool usage ability** | Good | I became familiar with the Hugo Workshop Template, Markdown, the `content/` and `static/images/` folder structures, and how Markdown content is rendered into a website. I also practiced working directly in the AWS Console to create resources and check deployment results. |
| 10 | **Contribution to the personal project** | Good | I built a personalized project direction based on the Fraud Detection problem and used multiple AWS services instead of copying the original sample template. The report clearly presents the pipeline, objectives, risks, costs, and future development direction. |
| 11 | **Ability to self-evaluate and improve** | Good | I reviewed the content many times, updated supporting images, corrected sections that did not match the project, and clarified cleanup steps to make the report more consistent. |
| 12 | **Overall evaluation** | Good | Overall, I achieved the main goal of building a workshop website report for the Fraud Detection on AWS project. The content demonstrates the architecture, deployment process, operational evidence, and lessons learned during the internship. |

## Strengths achieved

- Better understanding of how a Machine Learning system on AWS can be divided into multiple components: data, training, inference, real-time stream, alerting, and result storage.
- Ability to design architecture at a high level before going into each implementation step.
- Ability to organize a report in a workshop structure so readers can follow the implementation process.
- Awareness of avoiding direct copying from the sample template and instead adjusting the content to fit the personal project.
- Ability to organize supporting images in Hugo using the `static/images/` folder and `/images/...` paths.
- Ability to check the website with Hugo build to ensure the content displays correctly.

## Areas for improvement

- I need to continue practicing more deeply with the AWS Console to perform deployment steps more confidently.
- I need to perform more detailed end-to-end testing: sending sample transactions, receiving predictions, checking SNS alerts, and verifying results written to S3.
- I need to manage AWS costs more carefully, especially with SageMaker Real-time Endpoint and real-time services.
- I need to continue improving my English expression when mapping content from the Vietnamese version to the English version.

## Next improvement plan

In the next stage, I will focus on the following tasks:

1. Review the English version to ensure it closely follows the Vietnamese version.
2. Test the sample request flow and prediction response again to improve the reliability of the demo section.
3. Review IAM Role, costs, and cleanup steps to make the report more rigorous.
4. Check the Hugo website after each edit to ensure the content displays correctly.

## Self-evaluation conclusion

Through the internship, I realized that I made clear progress in connecting Machine Learning knowledge with the AWS cloud environment. The Fraud Detection project helped me understand that a real-world ML system does not stop at training a model, but also needs to consider input data, endpoint deployment, real-time processing, alerting, history storage, logging, IAM security, and operational costs.

I evaluate my overall result as **Good**. The report demonstrates the content foundation, main architecture, supporting images, and important lessons learned during the Fraud Detection on AWS project.
