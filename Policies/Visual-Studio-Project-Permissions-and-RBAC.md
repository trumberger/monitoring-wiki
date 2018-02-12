This section describes the Visual Studio permissions, policies and access controls used within the **Monitoring Project**

## Monitoring Roles
**Visual Studio Group Name:**  Monitoring Collaborators
**Summary:** People within Microsoft that want to contribute to the monitoring platform. They need to have read access to WIKI / Code / work and able to create separate branches and pull requests.  NOT able to trigger deployments.
**Permissions**  

| Group Name | Monitoring Collaborators |
| -- | -- |
| Summary | People within Microsoft |

View release definition
View releases
	• Build permissions
		○ View build definition
		○ View builds
	• Work > Area Permissions: Monitoring
		○ Edit work items in this node
		○ View permissions for this node
		○ View work items in this node
	• Git repo permissions: Monitoring
		○ Contribute
		○ Contribute to pull requests
		○ Create branch
		○ Create tag
		○ Manage notes
		○ Read
	• Git branch permissions
		○ Master
			§ Contribute
		○ Production
			§ NONE
	• Branch Policies
		○ Master
			§ NONE
		○ Production
			§ Check for linked work items on pull requests (optional - warning)
			§ Required Reviewers: Niels Nijweide

Read-only. Internal and external (customers) users that can download code in production branch.  Fork repo, download any files in production branch.
	• Release Permissions
		○ View release definition
		○ View releases
	• Build permissions
		○ View build definition
		○ View builds
	• Work > Area Permissions: Monitoring
		○ NONE (view work items?)
	• Git repo permissions: Monitoring
		○ Contribute to pull requests
		○ Read
	• Git branch permissions
		○ Master
			§ NONE
		○ Production
NONE - can they still fork?