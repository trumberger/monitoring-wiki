
1. Pick work item(s) in VSTS
2. Create branch from master and give it an appropriate name, e.g. dumil_task_1234
   - Intention is that the branch is short-lived, 1-2 days max. Especially important if you’re doing arm templates. 
3. Complete work, committing as often as appropriate to that branch
4. PR it into master, ensuring you link your work items (not something I’ve covered with the team yet)
5. Address any code review comments and just update your branch with any new / changed / deleted files… do not abandon your PR, it will automatically update when you sync your branch to VSTS
6. When all review comments are addressed and your PR is approved, you can complete it. Make sure to do a squash merge and delete your local branch. You can set “Autocomplete” if you like, so that it automatically completes once it’s been approved. Just remember to tick the squash merge and delete branch options too.
1. Importance of useful comment history particularly in main squash merge

https://code.visualstudio.com/docs/editor/versioncontrol#_git-support

https://docs.microsoft.com/en-us/vsts/git/gitquickstart?view=vsts&tabs=visual-studio

## To do
- The workflow used for the project
- Branches reserved for specific purposes
- Clear expectation on who is responsible for resolving merge conflicts between the pull request and the base branch
- Indication of who should merge a pull request and when
- Indication of how to decide the base branch for a pull request
- Format requirements for commit messages and pull requests
- Code standards and best practices that must be followed for a pull request to be merged
- Code reviews / peers

## Core Team vs. Contributor



## Resources
https://www.atlassian.com/git/tutorials/comparing-workflows

https://medium.com/@ahecimo/selecting-the-right-git-workflow-f77081eef5c2

https://docs.microsoft.com/en-us/contribute/
