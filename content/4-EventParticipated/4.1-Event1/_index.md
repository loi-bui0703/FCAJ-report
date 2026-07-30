---
title: "Event 1"
date: 2026-07-25
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---

# Event Report: “FCAJ X Agentic AI Build Week – Show Up. Build. Pitch. Win!”

### Event Objectives

* Create a hands-on and competitive environment where developers, data engineers, and students build autonomous Agentic AI applications for real business problems.
* Share AWS cloud-native architectures and practical lessons from the award-winning teams of Agentic AI Build Week.
* Encourage innovative mental models, continuous learning, and effective teamwork in the AI Agent era.

### Speakers & Team Representatives

* **Joseph Marazota:** Head of Technology at AWS.
* **Nguyen Gia Hung:** Head of Solution Architect at AWS Vietnam and Founder of First Cloud AI Journey (FCAJ).
* **One Team — First Place, AWS Track:** Represented by Chung and team members.
* **Signal Scout — Second Place, AWS Track:** Hoang Hieu, Quoc Hao, Minh Quan (Willer), Cong Minh, Duy Khiem, and Tuan Luc.
* **Plan B Team:** Long, Vi, Phat, An, and Nghia.
* **3K Team:** Nguyen Huy, Huynh An Khuong, Hoang Huynh Duc, Ngo Khoi, and Dang Nguyen Phuoc Loc.
* **Six Pillars Team:** Viet, Nguyen Van Linh, Nguyen, Minh Nhat, and Phuoc Huyen.

### Key Highlights

#### Opening keynote: Reframing the mental model for the AI Agent era

Joseph Marazota explained how AI Agents are changing software release velocity. Processes that once required an entire quarter or several weeks can now be completed within minutes. This change challenges engineers to reconsider traditional product-development lifecycles and actively question legacy assumptions.

Young engineers can benefit from not being constrained by mainframe or on-premises mental models. However, faster delivery does not remove human responsibility. Even advanced AI systems and Amazon's large-scale robotics operations still require people to evaluate recommendations, approve important actions, and ensure safety and accuracy through **Human-in-the-Loop** controls.

#### AI-powered conversational ordering: KFC Agent by One Team

One Team began with a real failure case: a drive-through AI ordering system that misunderstood conversational context and produced unreasonable orders. The team designed an Agent that works inside familiar messaging applications such as Zalo or WhatsApp, eliminating the need to download another application or create a new account.

The solution used **Amazon Bedrock AgentCore** to preserve session memory and customer preferences. **AWS WAF** protected the public infrastructure, while TinyFish collected current menu information from KFC's official website for storage in an AWS database. The team estimated an operating cost of approximately **$0.006 per order**, representing a 75% reduction compared with a traditional processing model.

#### Multi-Agent competitor intelligence: Signal Scout

Signal Scout presented a platform that gathers scattered public market signals, connects financial and company information, and forecasts possible ROI when a business considers a competitor's strategy.

The architecture followed an **Agent-to-Agent (A2A)** model. A Supervisor Agent coordinated specialized sub-agents for crawling, analysis, and validation. The crawler dynamically selected Apify for static pages or TinyFish for dynamic sources. A validation loop scored data quality and retried retrieval up to two times before escalating unresolved cases for human review.

Replacing several third-party components with AWS-native browser and web tools reduced the estimated monthly operating cost from **$94 to $35** while supporting data-residency requirements.

#### Automated architecture diagramming and infrastructure generation: Plan B

Plan B addressed a common bottleneck for Solutions Architects: producing architecture diagrams, cost estimates, and deployment plans under tight deadlines. Their AI-native workflow transformed natural-language requirements or documents into:

**Requirement input → policy and constraint analysis → Draw.io architecture diagram → cost estimation → Terraform or CloudFormation code → AWS deployment**

The workflow used official AWS architecture icons and a validation script that rejected services included in an enterprise blacklist. This demonstrated that generated infrastructure must remain subject to organizational policy and technical validation.

#### Real-time crowd-flow monitoring: Sheper by 3K Team

The 3K Team designed Sheper to reduce congestion at airports, supermarkets, and large events. Video was streamed through **Amazon Kinesis Video Streams** and processed on **AWS Fargate**. YOLOv8 or YOLOv11 detected people, while ByteTrack assigned tracking identifiers and supported confidence scoring.

Operators could define custom monitoring zones and evaluate movement density in real time. A Bedrock Agent then summarized the observations and produced staffing recommendations, helping operators respond before congestion became severe.

#### Anti-money-laundering detection: Adaptive Workflow Engine by Six Pillars

The Six Pillars team focused on the high false-positive rate of suspicious-transaction alerts in banking and fintech. Their solution used a three-layer architecture:

1. **Fast Detection:** Kinesis Data Streams ingested transactions, Lambda performed feature engineering, and XGBoost filtered obvious low-risk activity.
2. **Deep Investigation:** AWS Step Functions coordinated KYC, money-flow, and sanctions sub-agents. An OpenSearch vector database supported RAG-based retrieval of legal precedents and structured evidence.
3. **Decision and Human Review:** Two LLMs cross-validated results, while Bedrock Guardrails reduced hallucination risk. Only genuinely high-risk cases were escalated to a human-operated dashboard.

### Comparative Analysis

| Criteria | Traditional or Manual Approach | Agentic AI Architecture on AWS |
|---|---|---|
| F&B ordering | Manual staff or basic AI can misunderstand context and hallucinate. | Messaging Agent with Bedrock session memory; estimated $0.006 per order and 75% lower processing cost. |
| Competitor intelligence | Slow manual research with operating costs of $94 or more per month. | Supervisor, crawler, analysis, and validation Agents; reduced to approximately $35 per month with AWS-native tools. |
| Architecture design and estimation | Solutions Architects manually draw diagrams and calculate costs in spreadsheets. | Natural language generates Draw.io diagrams, cost estimates, IaC, and deployment workflows. |
| Crowd monitoring | CCTV is reviewed after congestion has already occurred. | Kinesis Video, YOLO, ByteTrack, and Bedrock provide real-time analysis and proactive recommendations. |
| AML detection | 90–95% false positives, approximately three hours per case, and $20–$25 per manual review. | XGBoost filtering, Step Functions and RAG investigation, dual-LLM validation, Guardrails, and targeted human escalation. |

### Key Takeaways

#### Design thinking

* Begin with a specific business problem and user pain point instead of building a generic application only to demonstrate technical complexity.
* Under a 24–48-hour deadline, define clear in-scope and out-of-scope boundaries and prioritize a stable MVP.
* Measure cloud operating costs and consider data-residency or compliance requirements when selecting managed and third-party services.

#### Technical architecture

* The Supervisor and specialized Sub-agent pattern can divide complex workflows without creating a single oversized Agent.
* Hallucination risk should be controlled through validation loops, dual-model cross-checking, Bedrock Guardrails, evidence, and human approval.
* Kinesis streaming services can connect real-time video or transaction data with computer-vision and machine-learning models.
* Generated architecture and IaC still require policy checks, security controls, and technical validation before deployment.

#### Personal development

* Time-constrained building develops resilience, prioritization, and incident-response skills that cannot be learned from theory alone.
* Low-ego collaboration, active listening, and clear responsibility across frontend, backend, AI, business, and pitching roles are essential to completing an ambitious project.

### Applying to Work

* Apply a Supervisor–Sub-agent workflow to personal projects when a task can be divided into retrieval, analysis, validation, and action.
* Strengthen CI/CD practices through clean Git history, disciplined `.env` management, secret scanning, and explicit approval before production deployment.
* Manage infrastructure with Terraform or CloudFormation so environments can be reviewed, versioned, and reproduced consistently.
* Build a stable and visually demonstrable MVP, then prepare fallback plans for network disruption, service limits, or exhausted AI-token budgets.
* Add measurable business outcomes, cost estimates, and validation evidence to technical proposals rather than presenting architecture alone.

### Event Experience

#### Open and practical knowledge sharing

The speakers and teams shared both achievements and difficult moments, including accidental `.env` exposure, network latency, depleted AI-token budgets, and unexpected SageMaker costs. These examples made the technical lessons more realistic and showed how teams recovered under pressure.

#### Diverse networking opportunities

The event connected students and engineers from different universities and disciplines, including AI, security, software engineering, and business. The discussions demonstrated how complementary skills contribute to a stronger product and presentation.

#### Inspiration to challenge personal limits

Seeing production-quality prototypes built within 24–48 hours reduced the psychological barrier to joining a Hackathon. The event encouraged me to focus on learning through participation instead of waiting until I felt fully prepared.

#### Lessons learned

Technology is a means, while practical value is the goal. A sophisticated architecture is useful only when it addresses the correct user or business problem. Failures during testing are opportunities to develop adaptability, and strong results in the AI era depend on clear roles, continuous learning, and collaborative growth.

#### Some event photos

![Bui Huu Loi attending FCAJ X Agentic AI Build Week on 25 July 2026](/images/events/fcaj-agentic-ai-build-week-2026-07-25.png)

<!-- EVENT 1 ADDITIONAL PHOTO: Insert another permitted team-presentation or networking photo below this comment.
Suggested file: static/images/events/fcaj-agentic-ai-build-week-additional.jpg
-->

> Overall, FCAJ X Agentic AI Build Week showed me how business-first thinking, Agentic AI architecture, cost awareness, validation controls, and low-ego teamwork can turn an ambitious idea into a practical prototype under intense time pressure.
