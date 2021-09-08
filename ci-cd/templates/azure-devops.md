---
description: >-
  Quickstart user guide for DX@Scale on Azure DevOps for Modern Modular
  Salesforce Org Development
---

# Azure DevOps



### Pre-requisites

The following lists of items are required to setup your end-to-end pipeline using [Azure DevOps](https://azure.microsoft.com/en-in/services/devops/) and [Salesforce](https://www.salesforce.com/).

### DevOps Platform

* [ ] [Microsoft Account](https://go.microsoft.com/fwlink/?LinkId=307137)
* If you don't have a Microsoft account, you can create one when you sign up for Azure DevOps.
* Use your Microsoft account if you don't need to authenticate users for an organization with [Azure AD](https://docs.microsoft.com/en-us/azure/active-directory/fundamentals/active-directory-whatis). All users must sign in to your organization with a Microsoft account.

### Salesforce

* [ ] [System Administrator Account](https://help.salesforce.com/s/articleView?id=How-to-change-Administrators-1327365222554&language=en_US&r=https%3A%2F%2Fwww.google.com%2F&type=1)
* [ ] [Enable DevHub](https://help.salesforce.com/s/articleView?id=sf.sfdx_setup_enable_devhub.htm&type=5)
* [ ] Create **Salesforce Service Account** in your DevHub that can be utilized create scratch orgs and deploy packages executing as the [CI Service Account](https://sfpowerscripts.dxatscale.io/getting-started/prerequisites#create-a-ci-service-user-in-production) using [AuthURL](https://developer.salesforce.com/docs/atlas.en-us.sfdx_cli_reference.meta/sfdx_cli_reference/cli_reference_auth_sfdxurl.htm)
* [ ] Create [Permission Sets](https://developer.salesforce.com/docs/atlas.en-us.securityImplGuide.meta/securityImplGuide/perm_sets_overview.htm#:~:text=A%20permission%20set%20is%20a,access%20without%20changing%20their%20profiles.&text=Users%20can%20have%20only%20one,can%20have%20multiple%20permission%20sets.) and [Sharing Groups](https://sfpowerscripts.dxatscale.io/getting-started/prerequisites#grant-developers-access-to-scratch-org-pools) for Developers on DevHub to [fetch scratch orgs](https://github.com/Accenture/sfpowerkit/wiki/Getting-started-with-ScratchOrg-Pooling#4-fetch-scratch-org-from-a-pool) and work with Salesforce DX
* [ ] Assign [Permission Sets](https://developer.salesforce.com/docs/atlas.en-us.securityImplGuide.meta/securityImplGuide/perm_sets_overview.htm#:~:text=A%20permission%20set%20is%20a,access%20without%20changing%20their%20profiles.&text=Users%20can%20have%20only%20one,can%20have%20multiple%20permission%20sets.) created above to Developers to ensure Object-Level Security \(OLS\) and Field Level Security \(FLS\) is available on [ScratchOrgInfo](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_objects_scratchorginfo.htm)
* [ ] Install sfpowerscripts [Scratch Org Pooling](https://github.com/Accenture/sfpowerscripts/tree/develop/prerequisites/scratchorgpool) unlocked package in DevHub
* [ ] Install [sfpowerscripts-artifact](https://github.com/Accenture/sfpowerscripts/tree/develop/prerequisites/sfpowerscripts-artifact) unlocked package in DevHub and existing lower existing sandboxes

### Developer Tools

* [ ] [Visual Studio Code IDE](https://code.visualstudio.com/download)
  * [ ] [Salesforce Extension Pack](https://marketplace.visualstudio.com/items?itemName=salesforce.salesforcedx-vscode)
  * [ ] [Markdown All in One](https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one) _\(Optional\)_
  * [ ] [Material Icon Theme](https://marketplace.visualstudio.com/items?itemName=PKief.material-icon-theme) _\(Optional\)_
  * [ ] [Prettier - Code formatter](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode) _\(Optional\)_
  * [ ] [Beautify](https://marketplace.visualstudio.com/items?itemName=HookyQR.beautify) _\(Optional\)_
  * [ ] [Azure Account](https://marketplace.visualstudio.com/items?itemName=ms-vscode.azure-account) _\(Optional\)_
  * [ ] [Azure Pipelines](https://marketplace.visualstudio.com/items?itemName=ms-azure-devops.azure-pipelines) _\(Optional\)_
* [ ] [git](https://git-scm.com/)
* [ ] [Salesforce CLI](https://www.npmjs.com/package/sfdx-cli)
* [ ] [sfpowerkit Plugin](https://github.com/dxatscale/sfpowerkit)
* [ ] [sfpowerscripts Plugin](https://github.com/Accenture/sfpowerscripts)
* [ ] [SFDX-Data-Move-Utility \(SFDMU\) Plugin](https://github.com/forcedotcom/SFDX-Data-Move-Utility)

### Dashboard Platform

* [ ] [New Relic Account](https://newrelic.com/signup) _\(Optional\)_
* [ ] D[ata Dog Account](https://www.datadoghq.com/) \(Optional\)
* [ ] Other [StatsD](https://github.com/statsd/statsd) Compatible Monitoring Platform  _\(Optional\)_

### Azure DevOps Services

Use all the Azure DevOps services or choose just what you need to complement your existing workflows

![](../../.gitbook/assets/image%20%287%29.png)

To learn more, visit:  
Azure Pipelines - [https://azure.microsoft.com/services/devops/pipelines/](https://azure.microsoft.com/services/devops/pipelines/)   
Azure Boards - [https://azure.microsoft.com/services/devops/boards/](https://azure.microsoft.com/services/devops/boards/)   
Azure Repos - [https://azure.microsoft.com/services/devops/repos/](https://azure.microsoft.com/services/devops/repos/)   
Azure Artifacts - [https://azure.microsoft.com/services/devops/artifacts/](https://azure.microsoft.com/services/devops/artifacts/)   
Azure Test Plans - [https://azure.microsoft.com/services/devops/test-plans/](https://azure.microsoft.com/services/devops/test-plans/)

### Overview

![Azure DevOps Overview](../../.gitbook/assets/image%20%2827%29.png)



| Feature | Summary |
| :--- | :--- |
| **Organization** | An organization in Azure DevOps is a mechanism for organizing and connecting groups of related projects, helping to scale up an enterprise.  |
| **Organization Settings** | Billing, Agent Pools, Change location/Time zone, Manage Active Directory, change Organization Owner, install and approve extensions, Manage Projects |
| **Project** | Used to host your codebase, track issues, plan work, collaborate on code, and continuously build, test, and use built-in pipelines to deploy your app. |
| **Project Settings** | Enable/Disable Azure Services, Add Users, Grant or restrict permissions, Manage Service Connections \(GitHub, NPM, Azure, Salesforce...etc.\) |
| **Azure Repos** | Azure Repos are a set of repositories that allow you to version control and manage your project code. It helps to work and coordinate code changes across your team. It will allow you to monitor code, solutions, builds, commits, pushes, PR’s \(Pull requests\) and branching |
| **Azure Boards** | Track your software projects and plan better with agile tools, including scrum _boards_, Kanban _boards_ and dashboards for any agile methodology. |
| **Azure Pipelines** |  Azure Pipeline is **a cloud service** that you can use to build and test your code project automatically. The Azure pipeline has a lot of capabilities such as continuous integration and continuous delivery to regularly and consistently test and builds our code and ship to any target. |
| **Azure Artifacts** | Azure Artifacts is **a package management solution integrated into Azure DevOps** that allows you to create and share Maven, npm, NuGet...etc. packages via feeds that can be both public and private to an organization with teams of any size |
| **Users** | Each GitLab account has a user profile, which contains information about you and your GitLab activity. |
| **Permissions** | Users have different abilities depending on the role they have in a particular group or project.  The roles available in GitLab are Owner, Maintainer, Developer, Reporter and Guest. |

