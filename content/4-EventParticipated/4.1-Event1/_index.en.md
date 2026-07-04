---
title: "Event 1 - FCAJ Community Day - Conference Call"
date: 2026-04-19
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---

## 1. Event information

- **Event name:** FCAJ Community Day - Conference Call
- **Time:** Saturday 23 May
- **Location:** Bitexco Financial Tower
- **Participation role:** Guest

## 2. Supporting image or video

![Proof of participation in FCAJ Community Day - Conference Call](/images/event_1.jpg)

## 3. Main program content

The **FCAJ Community Day - Conference Call** event focused on topics related to AI, cloud computing, multi-agent systems, and product-building experiences in real-world technology environments. The program included multiple short sharing sessions, with each session exploring a different aspect of applying technology to learning, research, and product development.

### 09:00 - 09:30 AM: Context Is Everything: Making AI Actually Work for You

The opening session focused on the role of **context** in using AI effectively. The main content included:

- Why AI can produce poor results when appropriate context is missing.
- What context really means during interactions with AI.
- The evolution from single prompts to memory and the concept of a **Second AI Brain**.
- How to provide better context to improve output quality.
- Suggestions for students when starting to learn, experiment, and build products with AI.

### 09:30 - 10:00 AM: 36 hrs with LotusHacks – Building UTMorpho from Idea to Reality

This sharing session presented the journey of building **UTMorpho** during LotusHacks. Key highlights included:

- Why the team joined LotusHacks.
- The brainstorming process from zero to forming an idea.
- How the team identified the problem and shaped the UTMorpho product.
- The experience of developing a product during a 36-hour sprint.
- Difficulties, failures, and turning points during the work process.
- An overview demo of the product and lessons learned after the competition.

### 10:00 - 10:40 AM: From Edge To Origin: CloudFront as Your Foundation

This session focused on **Amazon CloudFront** and its role in building a content delivery foundation, optimizing performance, and improving application security. The content included:

- Applying Amazon CloudFront to many different types of workloads.
- Cost optimization with Amazon CloudFront.
- Security capabilities when deploying CloudFront.
- Improving system reliability.
- Enhancing access performance for end users.

### 10:40 - 10:55 AM: Friendly AI Assistant with Amazon Quick

This sharing session introduced capabilities for building friendly AI assistants and supporting data analysis through tools in the Amazon Quick ecosystem. The main content included:

- **Quick Chat Agent**: an AI assistant that supports data exploration and insight analysis.
- **Quick Flows**: creating intelligent workflows in natural language without programming.
- **Quick Spaces**: a collaboration space that turns personal insights into team knowledge.
- **Quick Sight**: building dashboards and reports from raw data using natural language.

### 10:55 - 11:00 AM: Break

A short break during the program.

### 11:00 - 11:30 AM: Non-Determinism of "Deterministic" LLM Settings

This session explored an important issue when working with Large Language Models: even when the configuration appears deterministic, results may still vary. The content included:

- How LLMs choose the next token.
- The common assumption that `temperature = 0` guarantees fully deterministic results.
- The reality that inference optimizations can still create differences.
- The practical impact of this non-determinism in AI applications.
- Several approaches to reduce risk when deploying systems that use LLMs.

### 11:30 - 12:00 PM: Enterprise-Grade Multi-Agent System: The Case of Startup Credit Scoring

The final session presented an approach to building an enterprise-grade **multi-agent** system through a startup credit scoring example. The main content included:

- The mismatch between traditional banking systems and startup data.
- When to use a single agent and when a multi-agent system is needed.
- The thinking model of a multi-agent system.
- The blueprint of a **Virtual Credit Committee**.
- Guardrails and compliance in financial AI systems.
- Operational ROI and deployment roadmap.
- Future development directions.

## 4. Lessons learned and personal contribution

After participating in the event, I gained several lessons directly related to my learning direction and AWS internship project.

First, the session on **context in AI** helped me better understand that AI output quality depends not only on the model, but also heavily on how context, background data, and specific goals are provided. This is directly related to building a Machine Learning system on AWS: if input data, transaction features, and the processing workflow are not clearly designed, it is very difficult for the model to produce reliable predictions.

Second, the content about **Amazon CloudFront** gave me an additional perspective on optimizing performance, reliability, and security for systems serving users across different regions. Although my internship project focuses on Fraud Detection, CloudFront knowledge is still useful when designing systems with APIs, dashboards, or content that needs to be delivered reliably to end users.

Third, the session on **LLM non-determinism** helped me become more aware of risks when deploying AI in real-world environments. For systems that require strict output control, especially in the financial domain, designing logging mechanisms, testing, guardrails, and evaluation processes is very important.

Finally, the sharing session about **multi-agent systems in credit scoring** gave me many connections to the credit card fraud detection problem. An AI system in finance not only needs to make accurate predictions, but also needs explainability, risk control, and alignment with operational requirements. These are points I can reference when continuing to improve the architecture and future development direction of the Fraud Detection project on AWS.

Regarding my personal contribution, I participated in the event as a guest, recorded the main content of each session, and connected the lessons learned to my current internship project. The knowledge about AI context, CloudFront, LLM reliability, and multi-agent systems will be used to add practical perspectives to the report, especially in the sections on system architecture, operational optimization, and expansion direction.
