What is product-market fit?

What is a scaleup? 
A venture-funded later-stage company with product-market fits which are primarily investing in growth, essentially a startup that made it passed the early stages and is doing well and is focused on scaling as fast as possible.

pg18

What is the difference between a organization in a company being a cost center vs profit center?
Profit center is an org which produces revenue (Think Google Ads Organization) while a cost center is one that does not directly generate revenue but are still needed for the company to run smoothly (think engineering team implementing GDPR compliance)

What are the main tradeoffs working at a cost center vs profit center?
- Cost center jobs get cut before profit
- Cost centers are harder to get promoted so attrition is higher 
- Easier to get promoted in profit centers

What is a chaos test?
- A test where a process randomly kills services in a system to identify how service going down effects others so they can be made more independent
(Page 202)

What are snapshot tests?
- Tests that compare the output of a test to a pre-recorded output. Most frequently used in web and mobile development where the snapshot is an image of a screen. The test then compares how closely the snapshot is to the output of the test
(Page 202)

What are app size/bundle size tests?
For mobile/web apps, tests the size of an app or the initially loaded bundle can be a focus. Teams can monitor the size and set alerts for when a threshold is exceeded
(Page 203)

What are smoke tests?
Testing simple aspects of an app to find something obviously wrong with the product. Comes from the idea of smoke testing a circuit board by plugging it into power. If the board smokes we know its bad and has issues. An example is, does the app launch without crashing?
(Page 203)

What are performance tests?
Testing the performance of a app/system.
For example, after a PR merged into production does it effect latency of a backend service
(Page 201)

What are load tests?
Tests that ensure a system performs adequately under specific load.
There are 2 main types:
- Testing an existing system using some kind of testing infastructure
- Batching existing production requests. Production requests are delayed on purpose, after enough batching all requests are sent at an increased rate to production systems.
- Testing smaller version of infrastructure, instead of testing 10x load on existing system test the normal load on 1/10th of the system
(Page 201)

What is a multi-tenancy system?

What is weak/strong consistency?

What is write through cache?

What is idempotency?

What is a two-door decision?
A decision that can be easily reversed implying it has little risk. 
Examples:
- A/B testing a new feature using a feature flag
- Naming variables in internal code
- Choosing a linter
(Page 363)

What is a one-door decision?
A decision that once taken is difficult to reverse or even sometimes permanent. Although, most software decisions are irreversible reversable decisions become one-way when reversing is too expensive for an organization to do.
Examples:
- Selecting a programming language or framework
- Switching between a micro-services or monolith architecture 
- Cloud vs on-premises 
Page(363)

What is the main difference between one-door vs two-door decisions?
Two-door are easily reversable so they have little to no risk
Page(363)


What are RFCs?
(Requests For Comment)
Design documents used to get feedback on a design of a project and the why behind the decisions made of the design. It generally is made before or at the beginning of a project but can also be done after a project is complete to help others understand why the project was designed in the way it was.
(Page 207)

What are architecture documents?
Documents that are for recording decisions made with little intent for feedback
Popular kinds are:
- ADR
- C4 Model
- Arc42
(Page 209)

What is a project kickoff?
When all project stakeholders meet to confirm they understand the goals and approach of the project and endorse the high-level plan
(Page 226)

What is an engineering kickoff?
Comes after a project kickoff and aligns the engineering team and relevant engineering stakeholders on the "how" of a project.
(Page 227)

What is a PRD?
(Product Requirements Document)
A document written for a project that describes a project's "why" and "what". While engineering is involved it is not about engineering, rather it is about aligning all product, engineering, design, data science, and business stakeholders.
(Page 226)

What is Trunk based development?

(Page 244)

What is a stakeholder?
People and groups with an interest in a project's outcome
(Page 257)

What is a strategic stakeholder?
People or teams who you want to keep in the loop about a project, who can often help unblock upstream dependencies.
(Page 259)

What are upstream dependencies?
Your team's project dependencies that y'all rely on to complete your project
Page(259)

What are downstream dependencies?
The projects that rely on your project as a dependency for their completion
Page(259)

What is a north star?
An ambiguous generally ambitious (possibility unreachable) goal for an organization to keep the mission of the org on track and motivated
(Page 292)

What is a KPI?
(Key Performance Indicator)
A quantifiable measure for progress in an area. Most north star metrics are captured in KPIs.
Example, uptime, the amount of time a service is fully operational
(Page 292)

What are OKRs?
(Objectives and Key Results)
A popular approach for setting and measuring goals at tech companies, introduced by Google in 1999. They are set on multiple levels in an organization and set 2 main components:
- Objective: a high level goal that is qualitative, meaning not necessarily measurable
- Key results: measurable outcomes that help determine progress toward achieving the objective
(Page 293)

What is a SWOT analysis document?

(Page 298)



[Uber Article](https://www.uber.com/blog/multitenancy-microservice-architecture/)
(Page 204)

What is PII?
Personal identifiable information, user information that might be protected by compliance 

What are KPIs?
(Key performance indicators)
 a type of performance measurement. KPIs evaluate the success of an organization or of a particular activity in which it engages

What are the main Microsoft levels?
- all levels for SWE go from 59 to 80
- SDE
- SDE II
- Senior SDE
- Principle SDE
- Partner
- Distinguished Engineer
- Technical Fellow
****