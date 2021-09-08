---
description: >-
  Quickstart user guide for DX@Scale on GitLab for Modern Modular Salesforce Org
  Development
---

# GitLab

## ![](https://gblobscdn.gitbook.com/assets%2F-MI39dIf1BuKlg_oSIG_%2F-MhfD9klkbDUE6peCxSs%2F-MhfDbf-4L7J4Tq084t3%2Fimage.png?alt=media&token=e9ef0586-7c30-443c-ab79-ada13498fe40)

## A Refrerence Implementation of DX@Scale on Gitlab‌

![](https://gblobscdn.gitbook.com/assets%2F-MI39dIf1BuKlg_oSIG_%2F-MhfFoF1sJbZPqCtLhfF%2F-MhfHHimwttkCH-_lUxZ%2Freference_implementation_gitlab.png?alt=media&token=b22ecc15-2d12-4a81-bea0-311591d9074f)

## Pre-requisites <a id="pre-requisites"></a>

‌

The following lists of items are required to setup your end-to-end pipeline using [GitLab](https://about.gitlab.com/) and [Salesforce](https://www.salesforce.com/).‌

#### DevOps Platform <a id="devops-platform"></a>

* ​[GitLab Account](https://gitlab.com/users/sign_in)​

#### Salesforce <a id="salesforce"></a>

* ​[System Administrator Account](https://help.salesforce.com/s/articleView?id=How-to-change-Administrators-1327365222554&language=en_US&r=https%3A%2F%2Fwww.google.com%2F&type=1)​
* ​[Enable DevHub](https://help.salesforce.com/s/articleView?id=sf.sfdx_setup_enable_devhub.htm&type=5)​
* Create **Salesforce Service Account** in your DevHub that can be utilized create scratch orgs and deploy packages executing as the [CI Service Account](https://sfpowerscripts.dxatscale.io/getting-started/prerequisites#create-a-ci-service-user-in-production) using [AuthURL](https://developer.salesforce.com/docs/atlas.en-us.sfdx_cli_reference.meta/sfdx_cli_reference/cli_reference_auth_sfdxurl.htm)​
* Create [Permission Sets](https://developer.salesforce.com/docs/atlas.en-us.securityImplGuide.meta/securityImplGuide/perm_sets_overview.htm#:~:text=A%20permission%20set%20is%20a,access%20without%20changing%20their%20profiles.&text=Users%20can%20have%20only%20one,can%20have%20multiple%20permission%20sets.) and [Sharing Groups](https://sfpowerscripts.dxatscale.io/getting-started/prerequisites#grant-developers-access-to-scratch-org-pools) for Developers on DevHub to [fetch scratch orgs](https://github.com/Accenture/sfpowerkit/wiki/Getting-started-with-ScratchOrg-Pooling#4-fetch-scratch-org-from-a-pool) and work with Salesforce DX
* Assign [Permission Sets](https://developer.salesforce.com/docs/atlas.en-us.securityImplGuide.meta/securityImplGuide/perm_sets_overview.htm#:~:text=A%20permission%20set%20is%20a,access%20without%20changing%20their%20profiles.&text=Users%20can%20have%20only%20one,can%20have%20multiple%20permission%20sets.) created above to Developers to ensure Object-Level Security \(OLS\) and Field Level Security \(FLS\) is available on [ScratchOrgInfo](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_objects_scratchorginfo.htm)​
* Install sfpowerscripts [Scratch Org Pooling](https://github.com/Accenture/sfpowerscripts/tree/develop/prerequisites/scratchorgpool) unlocked package in DevHub
* Install [sfpowerscripts-artifact](https://github.com/Accenture/sfpowerscripts/tree/develop/prerequisites/sfpowerscripts-artifact) unlocked package in DevHub and existing lower existing sandboxes

5‌

#### Developer Tools <a id="developer-tools"></a>

* ​[Visual Studio Code IDE](https://code.visualstudio.com/download)​
  * ​[Salesforce Extension Pack](https://marketplace.visualstudio.com/items?itemName=salesforce.salesforcedx-vscode)​
  * Optional Extensions
    * ​[GitLab Workflow](https://marketplace.visualstudio.com/items?itemName=GitLab.gitlab-workflow)​
    * ​[Markdown All in One](https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one)​
    * ​[Material Icon Theme](https://marketplace.visualstudio.com/items?itemName=PKief.material-icon-theme)​
    * ​[Prettier - Code formatter](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)​
    * ​[Beautify](https://marketplace.visualstudio.com/items?itemName=HookyQR.beautify)​
* ​[git](https://git-scm.com/)​
* ​[Salesforce CLI](https://www.npmjs.com/package/sfdx-cli)​
* ​[sfpowerkit Plugin](https://github.com/dxatscale/sfpowerkit)​
* ​[sfpowerscripts Plugin](https://github.com/Accenture/sfpowerscripts)​
* ​[SFDX-Data-Move-Utility \(SFDMU\) Plugin](https://github.com/forcedotcom/SFDX-Data-Move-Utility)​

‌

#### Dashboard Platform <a id="dashboard-platform"></a>

* ​[New Relic Account](https://newrelic.com/signup) _\(Optional\)_
* D[ata Dog Account](https://www.datadoghq.com/) \(Optional\)
* Other [StatsD](https://github.com/statsd/statsd) Compatible Monitoring Platform _\(Optional\)_

## Solution Overview <a id="solution-overview"></a>

In order to configure DX@Scale with GitLab, there are a number of key features that need to be setup on the platform before executing the pipeline. Whether you are new to GitLab or have prior experience developing CI/CD for other software stacks on GitLab, this guide is meant to quickly summarize the key configuration steps on the platform and use the templates provided in our sample repository.‌

For a deeper dive on the platform, documentation is available on [GitLab Docs](https://docs.gitlab.com/ee/topics/use_gitlab.html).‌

### GitLab Overview <a id="gitlab-overview"></a>



![GitLab Overview](https://gblobscdn.gitbook.com/assets%2F-MI39dIf1BuKlg_oSIG_%2F-Mi-dFvtuvobHA_8LqXi%2F-Mi-lSMx4lktRfTmL6Rn%2Fimage.png?alt=media&token=486c1ac8-4246-4666-a58d-2ed2eabee37b)

<table>
  <thead>
    <tr>
      <th style="text-align:left">Feature</th>
      <th style="text-align:left">Summary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>Organization</b>
      </td>
      <td style="text-align:left">Top level hierarchy in GitLab used to configure your users and access
        to projects.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Project</b>
      </td>
      <td style="text-align:left">Used to host your codebase, track issues, plan work, collaborate on code,
        and continuously build, test, and use built-in CI/CD to deploy your app.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Repository</b>
      </td>
      <td style="text-align:left">Store your code in metadata <a href="https://developer.salesforce.com/tools/vscode/en/user-guide/source-format/">source format</a> and
        make changes to it. Your changes are tracked with version control.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Issues</b>
      </td>
      <td style="text-align:left">Collaborate on ideas, solve problems, and plan work.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>CI/CD</b>
      </td>
      <td style="text-align:left">
        <p>Tooling built into GitLab for software development through the continuous
          methodologies:</p>
        <ul>
          <li>Continuous Integration (CI)</li>
          <li>Continuous Delivery (CD)</li>
          <li>Continuous Deployment (CD)</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Package &amp; Repository</b>
      </td>
      <td style="text-align:left">Acts as a private or public registry for a variety of common package managers
        (eg. npm) and allows you to publish and share packages.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Settings</b>
      </td>
      <td style="text-align:left">Update general project settings, merge request approvals, default and
        protected branches, access tokens, CI/CD variables.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Others</b>
      </td>
      <td style="text-align:left">Additional menu options in GitLab such as Project Information, Security
        &amp; Compliance, Deployments, Monitor, Infrastructure, Analytics, Wiki,
        and Snippets.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Member</b>
      </td>
      <td style="text-align:left">Users and groups who have access to your project. Each member gets a role,
        which determines what they can do in the project.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Group</b>
      </td>
      <td style="text-align:left">Use to manage one or more related projects at the same time.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Subgroup</b>
      </td>
      <td style="text-align:left">Nested groups or hierarchical groups.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>User</b>
      </td>
      <td style="text-align:left">Each GitLab account has a user profile, which contains information about
        you and your GitLab activity.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Roles</b>
      </td>
      <td style="text-align:left">Users have different abilities depending on the role they have in a particular
        group or project. The roles available in GitLab are Owner, Maintainer,
        Developer, Reporter and Guest.</td>
    </tr>
  </tbody>
</table>

‌

### Configuration File <a id="configuration-file"></a>

‌

The [.gitlab-ci.yml](https://docs.gitlab.com/ee/ci/yaml/gitlab_ci_yaml.html) template file is the primary configuration file used to executing continuous integration, delivery and deployment on the platform. This CI/CD configuration file exists by default in the root directory of your repository and controls pipeline execution of stages and jobs triggered from updates to the repository via merge requests and/or merges, scheduled executions, or manual triggered.‌

In the template file provided, the structure of the [YAML](https://docs.gitlab.com/ee/ci/yaml/) file follows the following structure:

| Section | Description |
| :--- | :--- |
| **Comments** | General header for DX@Scale Template for GitLab and reference links to review. |
| **Project CI/CD Variables** |  Initial project Project CI/CD Variables required to be created in the project to authenticate and setup DevHub and Sandbox Environment alias, NPM Scope for artifacts, and optional dashboard connection details for DataDog or New Relic. |
| **Image** | Docker image to use for the job, defaulted to the [docker-sfpowerscripts](https://hub.docker.com/r/dxatscale/sfpowerscripts) image running on Ubuntu. |
| **Variables** | Custom variable used in the .gitlab-ci.yml during pipeline execution. |
| **NPM Configuration** | ​ |

‌

1. ​
2. NPM Configuration File Initialization
3. Stage Definitions
4. Rules Anchors
   * Merge Request
   * Merge
   * Manual
5. Triggered Job Definitions
6. Schedule Job Definitions
7. Manual Job Definitions

‌

### Pipelines <a id="pipelines"></a>

‌

The diagram below depicts the various stages and jobs configured in the GitLab CI/CD configuration file .gitlab-ci.yml which incorporates the [sfpowerscripts orchestrator](https://sfpowerscripts.dxatscale.io/faq/orchestrator) and [sfpowerkit package](https://github.com/Accenture/sfpowerkit#sfpowerkitpackagedependenciesinstall) commands in the script to structure your CI/CD process.

2CI/CD Pipeline Triggers for Development and Releases

![](https://gblobscdn.gitbook.com/assets%2F-MI39dIf1BuKlg_oSIG_%2F-MhyEFMCDctNzNd7OWTc%2F-MhzA16UBpp5TTTZ0sdm%2Fimage.png?alt=media&token=47c1e7d3-7cfb-4b23-84c9-88064ae9ae56)

​‌

Runners and Agents‌

General Concepts on Stages, Jobs and Scripts‌

DevHub Authentication‌

Schedules‌

Approvals‌

Rules‌

Anchors‌

Concurrency Control \(Resource Group\)‌

Dependencies‌

Environments -- Control Approvals‌

Artifacts - NPM Details / Description‌

Release Definition‌

Scratch Org Pool Config, CI Pool Config, and Dev Pool Config‌

## Design Considerations <a id="design-considerations"></a>

‌

The following are additional design configurations to consider when using this template:‌

1. Public Docker Registry vs. Project Registry
2. Public DX@Scale Unlocked Package vs. DevHub Unlocked Package for **Scratch Org Pool** and **sfpowerscripts-artifact**
3. On Premise vs. Cloud GitLab
4. Project NPM Package Registry vs. External NPM Package Registry
5. Project CI/CD Variables vs. External Secrets Provider
6. Multi-Repository Checkout Support
7. Release Gates Process
8. Operational Dashboard Tooling
9. ALM Integration vs. GitLab Issue Management Tool
10. Protected Branches
11. Merge Request Rules \(eg. Squash commits when merging\)
12. Merge request \(MR\) approvals
13. Requirements for Access Tokens and SSH Keys
14. Security Design - Roles Assignment to Users

​

​

​‌

### CI/CD Variables <a id="ci-cd-variables"></a>

‌

Reuse values based on a variable/value key pair.‌

### Job Artifacts <a id="job-artifacts"></a>

‌

### Environments <a id="environments"></a>

‌

### Roles <a id="roles"></a>

‌

## Getting Started <a id="getting-started"></a>

‌

## 1. Clone Repository <a id="1-clone-repository"></a>

‌

To get started, clone the [dxatscale-template](https://github.com/dxatscale/dxatscale-template) to your local machine.

```text
git clone git@github.com:dxatscale/dxatscale-template.git
```

 Super-powers are granted randomly so please submit an issue if you're not happy with yours.‌

## 2. Create Project <a id="2-create-project"></a>

‌

Create New GitLab Project

​

```text
hello.sh# Ain't no code for that yet, sorryecho 'You got to trust me on this, I saved the world'
```

‌

3. Project CI/CD Variables‌

Navigate to **Settings &gt; CI/CD** and expand the **Variables** section‌

## References <a id="references"></a>

‌

* ​[GitLab Docs](https://docs.gitlab.com/ee/topics/use_gitlab.html)​
* ​[GitLab CLI Tool](https://glab.readthedocs.io/en/latest/)​
* ​[Keyword reference for the .gitlab-ci.yml file \(FREE\)](https://microfluidics.utoronto.ca/gitlab/help/ci/yaml/README.md)​
* ​[Using external secrets in CI](https://docs.gitlab.com/ee/ci/secrets/)​

‌

## Tutorials <a id="tutorials"></a>

‌

* ​[Scheduled and On Demand Jobs with Run Pipeline Form](https://gitlab.com/guided-explorations/gitlab-ci-yml-tips-tricks-and-hacks/scheduled-and-on-demand-tasks/-/tree/master)​
* ​[GitLab environment variables demystified](https://about.gitlab.com/blog/2021/04/09/demystifying-ci-cd-variables/)​
* ​[First time GitLab & CI/CD workshop with Michael Friedrich](https://www.youtube.com/watch?v=kTNfi5z6Uvk&t=553s)​

‌

## Final Thought <a id="final-thought"></a>

‌

We hope this user guide has enabled you to quickly onboard DX@Scale on your Salesforce Projects. Feedback is always welcome as we look to continue to mature and simplify the onboarding experience for DX@Scale end users.

