---
title: "Week 8 Worklog"
date: 2026-07-20
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Week 8 Objectives:

* Securely manage sensitive configuration data (API Keys, DB Credentials) using AWS Systems Manager Parameter Store.
* Understand the mindset and workflow of Continuous Integration/Continuous Deployment (CI/CD).
* Automate the code/server deployment process whenever changes are pushed to the repository (GitHub Actions / AWS CodePipeline).

### Tasks to Implement This Week:
| Day | Tasks | Start Date | Completion Date | Reference Documentation |
| --- | ----- | ---------- | --------------- | ----------------------- |
| Mon | - Learn about the risks of hardcoding secrets (API Keys, Credentials) in source code <br> - Learn about the AWS Systems Manager (SSM) Parameter Store service | 20/07/2026 | 20/07/2026 | |
| Tue | - **Hands-on practice:** Store parameters (`SecureString`) in Parameter Store and retrieve them directly from an application/Lambda using SDK | 21/07/2026 | 21/07/2026 | <https://cloudjourney.awsstudygroup.com/> |
| Wed, Thu | - Learn an overview of CI/CD Pipelines in software projects <br> - **Hands-on practice:** Set up a simple Workflow with GitHub Actions (or AWS CodePipeline) to automatically test and deploy source code to S3 / App Runner on every `git push` | 22/07/2026 | 23/07/2026 | <https://cloudjourney.awsstudygroup.com/> |
| Fri, Sat | - **Hands-on practice:** Test code changes, verify the automated Build & Deploy process, and inspect build logs | 24/07/2026 | 25/07/2026 | <https://cloudjourney.awsstudygroup.com/> |


### Week 8 Achievements:

* Completely decoupled sensitive configuration and credentials from source code using SSM Parameter Store.
* Gained a deep understanding of automated software delivery workflows in real-world scenarios (CI/CD).
* Successfully built an automated pipeline to update cloud applications immediately whenever new code is pushed.