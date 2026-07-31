---
title : "Blog 3"
date : "2026-07-27"
weight : 3
chapter : false
pre : " <b> 3.3. </b> "
---

# WHAT IS AMAZON EVENTBRIDGE? BUILDING EVENT-DRIVEN APPLICATIONS ON AWS

Amazon EventBridge is a serverless service that connects application components together by generating and processing events. It is the foundation for building event-driven architecture — a design style in which components communicate by emitting and responding to events rather than calling each other directly, making systems more flexible and easier to scale.

![Blog 3](/images/3-BlogsPosted/3.3-Blog3/image3.png)

### Key points to know

- EventBridge provides two main mechanisms for processing and forwarding events: Event bus and Pipes.
- An event bus acts as a router, receiving events from multiple sources (custom-built applications, AWS services, third-party software) and delivering them to multiple destinations, optionally transforming the data before delivery.
- Pipes are suited for point-to-point integration: each pipe receives events from a single source and delivers them to a single destination, but supports more advanced data transformation and enrichment.
- Pipes and event buses are often used together: a pipe can receive data from a DynamoDB Stream and send it to an event bus, which then distributes it to multiple destinations according to configured rules.
- EventBridge also includes EventBridge Scheduler — a serverless scheduler that lets you create, run, and manage tasks on a schedule (cron or rate expression) or as one-time tasks, with configurable flexible time windows and retry limits.

In essence, EventBridge solves a problem commonly faced when building microservice systems: how components can "know" about events happening elsewhere without calling each other's APIs directly. Instead of writing complex back-and-forth call logic, a service simply publishes an event to the event bus, and interested services register rules to receive the exact event types they need. This approach makes it easy to add or remove components without affecting the rest of the system — well suited to projects that need scalability and easy long-term maintenance.

Post's link on group:https://www.facebook.com/groups/awsstudygroupfcj/permalink/2229202854511341/?rdid=wj3xkTX7M7viFBap#

---

### References

- [What Is Amazon EventBridge? – AWS Documentation](https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-what-is.html)
- [Amazon EventBridge Event Buses – AWS Documentation](https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-event-bus.html)
- [Amazon EventBridge Pipes – AWS Documentation](https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-pipes.html)