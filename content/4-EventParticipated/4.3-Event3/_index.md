---
title: "Event 3"
date: 2026-07-22
weight: 3
chapter: false
pre: " <b> 4.3. </b> "
---

# Summary Report: “AWS Tech Meetup and Community Knowledge Sharing”

### Event Objectives

* Explain the relationship between service-level commitments, monitoring, and customer experience.
* Share a structured preparation approach for AWS Certified Cloud Practitioner CLF-C02.
* Introduce AI-assisted application-security review and its role in DevSecOps.
* Create an opportunity for learners to exchange operational and security experiences.

### Speakers

* **Nguyen Huynh Son:** Infrastructure Support Engineer at Endava, Ex-Infrastructure Reliability Engineer at SPS, Member of AWS Student Builder Group HUFLIT.
* **Ngo Le Tan Huy:** Speaker sharing the AWS Cloud Practitioner certification roadmap.
* **Nguyen Tuan Thinh:** DevOps/DevSecOps/Cloud Engineer at Styl Solutions, Member of First Cloud AI Journey.

### Key Highlights

#### Monitoring what users experience

The monitoring session challenged the assumption that healthy infrastructure proves a healthy application. CPU, memory, load-balancer targets, and health endpoints can remain normal while users fail to complete a login or transaction because of a downstream dependency.

#### Actionable alerting

The proposed monitoring hierarchy moved from cloud infrastructure and application signals toward business actions and customer outcomes. Alarms should identify an owner, notification path, investigation procedure, and expected response.

#### AWS Certified Cloud Practitioner preparation

The certification session organized CLF-C02 study around the official domains and Shared Responsibility Model. A useful technique was to analyze why each incorrect answer is unsuitable rather than memorizing only the correct choice.

#### AI-assisted application security

The security session explored AI support for architecture review, code review, and application testing. Generated findings and fixes still require reproducible evidence, authorization checks, business-logic review, and human approval.

### Key Takeaways

#### Operational thinking

* Monitor user journeys and business outcomes alongside infrastructure health.
* Connect each alarm to a clear owner and response procedure.
* Use the Shared Responsibility Model to determine what AWS operates and what the workload team must configure.
* Preserve evidence so incidents and security findings can be reproduced.

#### Security mindset

* Shift security review toward design, source code, dependencies, infrastructure, and deployment pipelines.
* AI can accelerate review but does not replace expert judgment.
* Authentication, authorization, and business logic still require careful human analysis.

### Applying to Work

* Add an application-level success indicator to the project monitoring plan.
* Keep security checks in the pull-request and CI/CD pipeline path.
* Document manual approval points that protect production deployment.
* Record why automated findings are accepted, rejected, or require further review.

### Event Experience

#### Learning from speakers

The event connected operations, certification knowledge, and application security. This combination helped me see how AWS service knowledge must be translated into user outcomes and operational responsibilities.

#### Technical demonstrations and examples

The example of green infrastructure metrics alongside failed user logins clearly demonstrated the limits of infrastructure-only monitoring. The security examples also showed why automated output must be validated.

#### Networking and discussions

Community discussion helped me identify gaps in my own monitoring and security assumptions. I gained useful study and troubleshooting approaches that can be applied beyond this event.

#### Lessons learned

The most important lesson was that system health should be evaluated from the user’s perspective. Reliable cloud engineering also requires ownership, evidence, and security controls throughout the development lifecycle.



> Overall, the meetup strengthened my understanding of user-centered monitoring, shared cloud responsibility, certification reasoning, and evidence-based application security.
