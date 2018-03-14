This section describes the Visual Studio permissions, policies and access controls used within the **Monitoring Project**. The roles are based on the [defined personas](https://easplatform.visualstudio.com/Monitoring/_apps/hub/agile-extensions.personas.personas-work-hub) for the monitoring & automation team.

## Monitoring Roles
The Monitoring project uses the [standard group permission definitions](https://docs.microsoft.com/en-us/vsts/security/permissions) for users within this instance. 

### Monitoring Team Member

Members are given project "Contributor" permissions by default.  Users who need additional administrative permissions are given "Project Administrator" permissions.

### Monitoring Contributors

**Visual Studio Group Name:**  Monitoring Collaborators

**Summary:** People within Microsoft that want to contribute to the monitoring platform. They need to have read access to WIKI / Code / work and able to create separate branches and pull requests.  NOT able to trigger deployments.  

| Category | Permissions |
| -- | -- |
| Release | view release definition; view release |
| Build | view build definition; view builds |
| Work (Monitoring and sub-areas) | edit work items, view permissions, view work items |
| Repo (Monitoring) | contribute, contribute to pull requests, create branch, create tag, manage notes, read |
| Git branch permissions | **Master**: Contribute; **Production**: None |

### Other Microsoft Roles

**Visual Studio Group Name:**  Readers

**Summary:** Internal and external (customers) users that can download code in production branch.  Fork repo, download any files in production branch.

| Category | Permissions |
| -- | -- |
| Release | view release definition; view release |
| Build | view build definition; view builds |
| Work (Monitoring and sub-areas) | None |
| Repo (Monitoring) | contribute to pull requests, read |
| Git branch permissions | **Master**: Contribute; **Production**: None |
| Wiki permissions | Read-only |

## Branch Policies
A comprehensive overview of branch polices and permissions using git in VSTS can be found on the [Visual Studio documentation site.](https://docs.microsoft.com/en-us/vsts/git/branch-policies)

**Production**
- Check for linked work items on pull requests (optional / warning)
- Required reviewers for pull request:  Niels Nijweide

**Master**
- Required reviewers for pull request:  Niels Nijweide