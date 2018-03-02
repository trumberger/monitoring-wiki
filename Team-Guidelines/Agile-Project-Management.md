# Overview

The ESS Monitoring team follows the Agile approach to software development which emphasizes incremental delivery, frequent inspection, team collaboration, continual planning, and continual learning.    We follow the Scrum framework for the specific roles, artifacts, and events within the team.

## Agile

The principles originally outlined in the [Agile Manifesto](http://agilemanifesto.org/) are first and foremost a mindset / cultural change to how the team organizes and operates to deliver value to end users.  Specifically, Agile values:
- **Individuals and interactions** over processes and tools
- **Working software** over comprehensive documentation
- **Customer collaboration** over contract negotiation
- **Responding to change** over following a plan

These values have become increasingly important in the era of increasingly complex systems that must be always-on and constantly improving.  A good starting point to Agile can be found on the [VSTS Agile site.](https://www.visualstudio.com/agile/)

## Scrum
[Scrum](https://www.visualstudio.com/learn/what-is-scrum/) is a popular Agile framework that defines specific artifacts, practices, and roles for self-organizing teams. One of the core aspects of scrum is a pre-defined lifecyle or iteration (usually called a sprint) in which the team collaborates closely to get work done and then inspects the work that was completed.  Scrum also defines a number of artifacts (e.g. product backlog), events (sprint planning, daily standup, etc), and roles (product owner, scrum master, etc).  The below descriptions of roles, events, and artifacts for the ESS Monitoring team are largely taken from the [Scrum Guide](https://www.scrumguides.org/scrum-guide.html).
### Scrum Lifecycle

<IMG src="https://www.visualstudio.com/wp-content/uploads/2017/04/agile-scrum-lifecycle-diagram.png" alt="Scrum Lifecycle Diagram"/>

### Scrum Values and Principles

Scrum consists of three core principles and seven values.

**Principles**
1. Transparency - transparency across the team is essential to scrum in order to make work visible across the team, create shared understanding, and optimize processes.
2. Inspection - scrum focuses on frequent inspection of the backlog and work being performed, accomplished via regular events like sprint planning, retros, demos, etc.
3. Adaptation -adaptation is the natural response to inspection, allowing teams to course correct and make changes as new information becomes available.

Scrum also defines fives core values: **commitment, courage, focus, openness, and respect** which inform how the team should collaborate and hold eachother accountable.

## ESS Monitoring Team

### Roles

|Roles |Who |What |
| --------- | ----------------- | -------------------------------- |
| Product Manager (or PO) | Niels Nijweide | The Product Manager is responsible for maximizing the value of the product resulting from the work of the devops team.  The are the sole person responsible for managing the product backlog.
| Dev Lead | Duncan Millard | Responsible for quality and completeness of the work the team builds.  Mentoring team as a hands on servant leader
| Architect | Duncan Millard and Niels Nijweide | Responsible for defining the architecture for the solution and is the lead advisor about technical approaches undertaken and products to be used
| Site Reliability Engineer | Tino Donderwinkell | Incorporates aspects of software engineering into operations to create ultra-scalable and highly reliable software systems.
| Release Manager | Tino Donderwinkell |  Responsible for the releases of code and artifacts into production environments.  Devops places a lot of focus on Infrastructure as code and continuous delivery
| PMO / Scrum Master | Tyler Rumberger | Scrum master is responsible for promoting and supporting Scrum within the team.  They are a servant-leader for the team and help empower them and remove obstacles.  The "PMO" refers to driving program governance and ensuring visibility to leadership.
| Devops Team | Dimitrie Bogdan Lascar, Cosmin Mladen, Catalin Irimia, Bogdan Petrescu | Self-organizing team that is responsible for delivering potentially releasable increments of software (i.e. customer value) and living the values of agile, scrum, and devops. |

### Key Artifacts

- The **Product Backlog** consists of all of the features, functions, requirements, enhancements, and fixes that need to be delivered for the product.  The Product Manager (or Product Owner in Scrum terms) is responsible for the availability, fidelity, and prioritization of the product backlog.  The ESS Monitoring team utilizes regular backlog refinement sessions to ensure Epics, Features, and User stories are clearly defined for the team with appropriate acceptance criteria and detail.
- The **Sprint Backlog** consists of all of the backlog items selected for a sprint as well as the plan for delivering increment to achieve the sprint goal.

### Team Events

The ESS Monitoring team uses a **2-week sprint cycle** which informs the schedule defined below.
| Event | Objective | Cadence | Attendees
| --- | --- | --- | ---
|Sprint Planning | Control input of planned work into the system - Establish sprint goal with the team, agree on what work will be accomplished in the coming sprint (committed user stories for the sprint backlog), define HOW the committed work will be accomplished (tasks and ownership) | Once at the start of each sprint | Full team
| Sprint Review / Demo | Inspect the work performed in the previous iteration and establish continuous improvement plans for the next sprint | Once at the end of each sprint | Full team
| Sprint Retrospective | Retrospective to identify what went well, what didn’t in the previous sprint, and what areas the team wants to improve in the next sprint. | Once at the end of each sprint | Full team
| Backlog Refinement | Refine product backlog (flesh out user stories and acceptance criteria) and adjust priority of backlog items. | Once a week (1 hr) | PM and Scrum Master, Dev lead optional
| Daily standup | Team briefly meets to share: what has been accomplished so far, what are you working on next, any blockers/obstacles | Daily | Full team
| Live site incident review | Control analysis and learning cycle from Live Site incidents; controls input of Live Site changes (people, process, tools, services) into Sprint Planning | Once a week (1 hr) | SRE, Dev lead, DRI |

