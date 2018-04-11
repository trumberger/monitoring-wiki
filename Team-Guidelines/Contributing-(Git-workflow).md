## Overview
The Monitoring team uses the git source control system within Visual Studio to coordinate code changes across the team.  The basic git workflow as well as the branch strategy and branch details can be found below.  Our git workflow and continuous delivery strategy are currently evolving, so please feel free to suggest changes / updates here. 

You can find more resources on using git with Visual Studio Team Services and Visual Studio Code below:
- [Git - Visual Studio Code](https://code.visualstudio.com/docs/editor/versioncontrol#_git-support)
- [Git - Visual Studio Team Services](https://docs.microsoft.com/en-us/vsts/git/tutorial/gitworkflow?view=vsts)

## Basic Git Worfklow
1. Select a work item from the backlog in VSTS
2. Create branch from `master` for the changes you plan to make and give it an appropriate name - a good format to use is: `[alias]_[work item type]_[work item id#]` for example `dunmil_task_892`
   - **NOTE:** The intention is that these branches are short-lived, typically 1-2 days max. This is especially important if you are working on ARM templates
   - You can create a new branch directly within a work item or link a work item to a branch using the Development field on the right-hand side
 ![image.png](.attachments/image-e2e2365f-0481-4f4e-8d16-a0e9268a6974.png)
3. Complete your work on the newly created branch, committing your changes as often as appropriate to the branch
   - It's a good practice to sync any changes made by other team members to your branch frequently using git `pull` in order to avoid merge conflicts down the road
4. Once you've completed your work, create a **Pull Request (PR)** so that others can review your changes before merging them into `master`.
   - Make sure you link the appropriate work item(s) to the Pull Request so that reviewers have visibility into the work that was done
   - Make sure you provide **useful comment history**, for all of your commits, but particularly during pull requests.
5. Address any code review comments and update your branch with any new / changed / deleted files… **do not** abandon your PR, it will automatically update when you sync your branch to VSTS
6. When all review comments are addressed and your PR is approved, you can complete the pull request. Make to check the option to do a `squash merge` and to `delete XYZ branch after merging` when completing the merge. You can also choose to set  “Autocomplete” if you like, so that the pull request will automatically complete once it has been approved and all branch policies are met. Just remember to tick the squash merge and delete branch options too.
   - Again, ensure you provide a **useful comment history** - this is especially important for the main squash merge!

## Branch Strategy

The team operates using a [Trunk-based development](https://trunkbaseddevelopment.com) source-control branching model.  The one-line summary for this model:
> A source-control branching model, where developers collaborate on code in a single branch called ‘trunk’ [often named `master` in git nomenclature], resist any pressure to create other long-lived development branches by employing documented techniques. They therefore avoid merge hell, do not break the build, and live happily ever after. 

Trunk-based development is a key enabler of continuous delivery that uses short-lived feature branches to avoid merge issues and ensure that the codebase in `master` is always in a releasable state and that any issues that break `master` are addressed immediately by the team.

### Monitoring Branches

| Branch Name | Description | Policies |
|---|---|---|
|master | details | policies|
|production | details| polices |

<!--- Hidden
## To do
- The workflow used for the project
- Branches reserved for specific purposes
- Clear expectation on who is responsible for resolving merge conflicts between the pull request and the base branch
- Indication of who should merge a pull request and when
- Indication of how to decide the base branch for a pull request
- Format requirements for commit messages and pull requests
- Code standards and best practices that must be followed for a pull request to be merged
- Code reviews / peers
-->

