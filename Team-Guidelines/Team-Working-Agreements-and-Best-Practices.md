## Taxonomy
The team backlog follows the standard VSTS agile work item hierarchy of **Epic - Feature - User Story - Task**.  These categories can be fluid as the team learns over time or estimates the work required for certain work items.  For example a loosely defined user story that is added to the backlog may be refined and turned into a feature with several user stories over time.
- In general, work items that are at the top of the backlog (e.g. 1 - 2 sprints out) should be more defined.
- All work items should be linked to a parent, i.e. there should be no child (epic and below) work items without a parent.
- https://www.visualstudio.com/learn/scale-agile-large-teams/

|Work item|Description|
|---|---|
|Epic | Large scale initiatives or themes that span multiple releases, broken down into features|
|Features | Represent new functionality that is released to the customer, e.g. release unit (think what you would put into release notes)
|User Stories | Incremental value team must deliver to create a feature (can be delivered in single sprint)
|Tasks | Individual tasks required to complete a story|

## User Stories
User stories are a way of describing requirements in agile.  They are user-centric (written from the perspective of the end user) and clearly define the **problem statement** but do not define the solution or the "how" behind achieving the story.  Most importantly, user stories are intended to spark a conversation between all members of the team in order to create a shared understanding and context behind the user story.

As the core unit of both the product and sprint backlog, the **product manager** is typically responsible for creating user stores that clearly define the problem statement (who, what, why) and give the devops team enough context to define HOW they will solve this problem (i.e. the solution).  Although the product manager is accountable for the overall clarity and priority of user stories in the product backlog - ANYONE on the team is encouraged to create a user story.  If you have an idea for a new feature or a change we should make - **share it!**

The preferred user story structure used by the team is:

>As a [user / persona]
>I want [task / action]
>so that [goal]

Intention of the user story is to capture the answer to three key questions:
1. **Who** is the user / persona facing the problem?
2. **What** specific task / thing are they trying to accomplish?
3. **Why**? What underlying outcome our goal do they want to achieve?

In some cases there will be technical user stories, architectural / enabler work, or other miscellaneous items that don't fit neatly into this template.  There's no need to force these types of stories into the above format - just make sure the user story is clearly defined and include enough level of detail for the team to understand the context and desired outcome.

## Acceptance Criteria
Where User Stories define the **problem**, acceptance criteria help define / refine user stories with specific details and considerations.  They also help the team know when a user story is done beyond the teams common definition of done.  In the early stages of the team, our acceptance criteria will be more prescriptive and detailed.  But, our goal is to ensure AC do not specify the HOW behind a user story or get deep into solutioning as this should be developed by the team, not the Product Manager.

## Team Definition of Ready
The Definition of Ready are the criteria that a user story must meet in order to be considered for inclusion in a sprint.  User stories that are discussed during Sprint Planning for inclusion in the next sprint must meet this criteria in order to be considered by the team.  This helps ensure the work is clearly defined before starting work so that the team can avoid churn / rework.

**A Product Backlog Item is considered "Ready" when:**
1. Story is described in accordance with the user story template (As a...) or as a clearly defined Non-Functional Requirement (NFR) or technical user story.
2. Story has been prioritized (stack ranked) by the Product Manager
3. Story has clearly defined and unambiguous acceptance criteria
4. Story has a baseline estimate (S - XL) agreed on my the Dev Lead, SRE, and Product Manager
5. Assumptions for the story are clearly documented
6. Any pre-requisite documentation, work instructions, or manual test instructions are available to the team and clearly defined
7. Any required automated test criteria are clearly defined

## Team Definition of Done
The Definition of Done is the criteria necessary in order to consider a User Story done or complete.  This ensures all team members understand what is required in order for a user story to be completed within a sprint.

**A Product Backlog Item is considered "Done" when:**
1. Solution builds successfully
2. Code written and merged into master branch 
3. Unit Tests implemented on all features to an appropriate code coverage 
4. All regression tests run and pass 
5. All acceptance criteria met 
6. Code has been peer reviewed and comments addressed
7. User Story moved to Resolved state 
8. Remaining hours for tasks set to zero and tasks closed. 
9. No open Sev1 or Sev2 bugs 
10. Deploys successfully into the automated Staging environment release pipeline
11. Static Code Analysis is run with results no worse than the baseline
12. Any related documentation (work instructions, wiki, manual steps, etc) are updated
13. Work items that modify source code are linked to associate commit

## Estimation
Currently, the team uses a simple t-shirt sizing approach to estimation ranging from Small (S) to Extra Large (XL).  Each size is associated with a Story Point value ranging from 1 for Small to 4 for Large.  A few points to keep in mind:
- Estimating is about relative effort
- Estimates should be a team sport, not just set by Product Manager - intended to start a conversation
- Estimates are a SWAG, not a commitment  
- Estimates help us better understand our team velocity, which aids in sprint planning and allows us to track improvement over time


