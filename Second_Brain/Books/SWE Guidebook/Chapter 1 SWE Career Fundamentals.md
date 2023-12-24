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

## Key Take Aways:

1. Own your own career - set goals, share your work/success, and try to get feedback
2. Be seen as someone who gets things done - when you make impact try to measure the business impact and share it
3. Keep a work log - record key work each week including important code changes, code reviews, design documents, discussion, planning, helping out others, postmortems, and anything else which takes time and has impact.
4. Understand the team's/manager's goals - ask them what are the biggest challenges the team/manager are facing in the coming weeks/months - there may be opportunities for you to help
5. Figure out what is important to your team, what is rewarded? How is impact measured?
6. Ask manager/tenured teammates about teams goals & how they align with the company's goals
7. Ask key-role people with influence about the team's/company's goals - could be product manager, skip manager, or business stakeholders
8. Figure out how performance reviews work and how to get the most out of them, ask mentors about it maxing it
9. In addition to work logs, record your wins - if you successful complete something record it and also screenshot positive feedback related to it
10. Share your progress from worklogs/wins to your manager in 1:1s because they often do not hear all the work you do
11. Help others, do code reviews, pair programming, or help unblock people when you have power to do so - make a teams calendar event to help capture you helping other or capture messages
12. Ask for feedback a good amount of time before performance reviews so you have time to improve on any area you are lacking
13. Ask for feedback about how you did and how you can improve for the following events: facilitating meeting, leading project, reviewing code (too harsh or not specific), resolving an outage, proposing a new initiative
14. Interact with others outside your team, whether it be data scientists, product managers, etc... 
15. Be interested in all aspects of your product
16. Talk to people who use your product, if you're a platform team connect with the engineers who use it, be welcoming to answer questions given by them 
17. Figure out if my team/company is a ship fast decent quality vs ship slower high quality
18. For the first 3 months keep a learning journal, write down 3 things you learn and 3 things you do not know but want to learn each week
19. Make Anki deck for all things you learn at msft
20. Learn from your manager what big projects your team is working on, what the priority level of each is to the team's/company's success
21. Do not take code review comments personally
22. Read as much code as you write - lots of code reviews, it can be good to review code on a sister team or on a internal technology our team uses, or open source projects 
23. Create a cheatsheet for company internal tools, and useful links for docs you can reference
24. Create a cheatsheet for common classes/modules your team uses or works with and write descriptions so you can reference them in the future
25. Learn to debug the CI/CD 
26. Learn and understand production logs/dashboards
27. When you ask for feedback try to make sure it is actionable if someone says something vague ask for clarification so you can take action to improve on it
28. Be detailed but concise when reporting on your work and the challenges you faced and how you overcame them
29. Block time to do deep work kind of as a high priority meeting so you do not get distracted but avoid overdoing it
30. Read the [Google Code Review Guide](https://slab.com/library/examples/google-code-review/)
31. Draw a map of the teams that our team works with and our relationship to those teams - lookup good tips for this bottom of page 177
	1. Overtime (years) introduce yourself to at least one senior person on each adjacent team and try to learn something new about the teams and build relationships
32. Read through the docs of what you work on from the users perspective 

## Mentorship
Approach a possible mentor with the following:
"You're someone I look up to. Can I set up a time to talk about areas I'd like to grow in and how you could potentially help, as a mentor?"
See Page 172 for topics to bring up at the meeting

## Getting stuff done
1. There are a lot of things you can work on always know what your #1 priority is and make sure it gets delivered on time even if you have to delay other things
2. Learn to say no to make sure you #1 priority gets done, but say no in a way like this: "yes I would like to help BUT x"
3. If you need help resolving blockers check out the cheatsheet on pafe 98
4. Try to break a task/project into as many sub-tasks as possible without getting too granular at the coding level - prioritize the sub tasks which will get stuff shipped quick so you can quickly test your project end to end and find out if you're on the right track


## Promotion
- must show impact of work so seek high impact tasks
- learn how promotions work and what are the requirements
- who are the parties that decide whether you get promoted
- "Its not enough to do good work, you need to work with other and publish your work so other are aware of it"
- Try to set goals with your manager and get it in writing so you can follow up with them later
- If you start chasing promotion let other know you are trying to get promoted
- Do not over focus on getting promoted tot he point that everyone thinks youre only self-interested

# Programming 

## Language Proficiency
- learn everything deeply
- learn best practices and understand why they are best
- go under the hood and learn how memory management, garbage collection, code compilation, and what matters for performance
- learn more advanced parts of language like generics, parallel execution/threading, and additional language features
- additional questions on page 122

## Debugging
- Learn your IDE's debugger and know it well
- Pair/shadow everyone on your team at least once to try to get insights in how other debug and maybe see some features you are not aware of or uses of known features

## Refactoring
- Refactoring is important and a separate skill on its own, keep an eye out on possible places for refactor and do them in the future and make a list of them, a refactor backlog
- don't refactor without consulting teammates about possible refactor areas
- Learn your IDE's refactoring capabilities

## Software Tools
- learn more advanced git, rebasing, cherry pick


## Senior Engineer Goals
- Short iterations - break problems down into small chunks so you can ship to prod everyday
- Be an unblocker - grow a network with other teams and workers in the company you can leverage to help unblock yourself or your teammates
- Become product minded


35 pages a day
Goal pages 331-330


Further Readings:
- For giving good feedback and speaking better
	- Radical Candor
	- Crucial Conversations
- Domain Driven Development
	- Learning Domain-Driven Design by Vlad
	- Domain-Driven Design Eric Evans
