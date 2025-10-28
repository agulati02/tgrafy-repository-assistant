# TGRAFY (v0.1.0)

### Introduction
**TGRAFY** is an AI assistant for reviewing your code and addressing developer comments, with an aim to speed up the process and reduce release timelines. In its current state, TGRAFY supports reviewing pull requests and having a two-way conversation with the PR contributors in the discussions tab. It will review your code for the below parameters:

<ul>
  <li>Performance Bottlenecks</li>
  <li>Security practices</li>
  <li>Code quality</li>
</ul>

### Installation
You can hire TGRAFY as a GitHub app, and install it [here](https://github.com/apps/tgrafy). It is recommended to go through the [installation steps](https://example.com) and [user guide](https://example.com), to get TGRAFY to do exactly what you need 😃. 

### What powers TGRAFY?
Our little helper is powered by a decoupled AWS-native application, that leverages a serverless design for resource and cost optimization.

**1. High-level System Design (HLSD)**

<img src="./assets/tgrafy-to-be.drawio-2.svg" alt="High Level System Design" />

**2. Walkthrough & Rationale**

When installed, TGRAFY subscribes to the below events in the repository:

<ul>
  <li>Discussion comment</li>
  <li>Issue comment</li>
  <li>Pull request</li>
  <li>Pull request review</li>
  <li>Pull request review comment</li>
</ul>

The subscription is powered by GitHub's webhook call to TGRAFY, which is handled by an AWS Lambda function. Since, these webhook calls are configured with a 10-second timeout, it is not feasible on a single Lambda to handle the review process. The webhook handler returns an initial response (a greeting comment in case of reviewer assignment) and pushes the event to a task queue, which is implemented as a standard SQS queue.

The SQS message triggers a review handler Lambda, which is responsible for prompting the LLM (Claude Sonnet 3.5 in the current state) with the repository context, and publish the review to the PR discussion thread.

### Source Code
TGRAFY's source code is distributed accross the below two repositories:

- Webhook Handler [🔗](https://github.com/agulati02/webhook-handler-lambda)
- Review Handler [🔗](https://example.com)

<br/>

🖋️ **Author:** Anurag Gulati [🔗](https://github.com/agulati02)

