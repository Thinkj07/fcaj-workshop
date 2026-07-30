---
title : "Blog 3"
date : "2026-07-27"
weight : 1
chapter : false
pre : " <b> 3.3. </b> "
---

# WHAT IS AMAZON EVENTBRIDGE? BUILDING EVENT-DRIVEN APPLICATIONS ON AWS

Amazon EventBridge is a serverless event bus service that makes it easy to connect applications using data from your own applications, integrated Software-as-a-Service (SaaS) applications, and AWS services. EventBridge simplifies building event-driven applications by automatically routing events from sources to targets without managing infrastructure.

![Kiến trúc VPC](/images/5-Workshop/5.3-vpc/vpc_archi2.png)

### Key Takeaways

- **Event-Driven Architecture**: EventBridge enables decoupling of system components, allowing services to communicate asynchronously through events.
- **Event Buses & Event Pipes**:
  - **Event Bus**: Ingests and routes events to multiple targets based on flexible filtering rules.
  - **EventBridge Pipes**: Creates point-to-point integrations directly from event sources (such as SQS, DynamoDB Streams, Kinesis) to targets without requiring custom glue code.
- **EventBridge Scheduler**: Allows scheduling recurring tasks or one-time invocations at specific future timestamps with high accuracy, supporting millions of concurrent schedules.
- **Rich Integrations**: Provides out-of-the-box integration with over 200 AWS services and dozens of major SaaS partners (Zendesk, Datadog, PagerDuty, etc.).
- **Filtering & Transformation**: Enables event filtering and payload transformation on the fly before delivering events to targets, reducing processing overhead on consumer services.

Adopting EventBridge makes system architectures more resilient, easier to scale, and simpler to maintain while significantly reducing the boilerplate code needed to connect services.

---

### References

- [What is Amazon EventBridge? – AWS Documentation](https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-what-is.html)
- [Amazon EventBridge Features](https://aws.amazon.com/eventbridge/features/)