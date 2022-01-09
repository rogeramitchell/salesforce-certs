## Resources

### Salesforce Content

- [Trailhead Overview](https://trailhead.salesforce.com/credentials/developmentlifecycledeploymentdesigner)
  - [Trailmix](https://trailhead.salesforce.com/en/users/00550000006yDdKAAU/trailmixes/architect-dev-lifecycle-and-deployment)
  - [Exam Guide](https://trailhead.salesforce.com/help?article=Salesforce-Certified-Development-Lifecycle-and-Deployment-Designer-Exam-Guide)

### Trailmix

[**Determine Which Application Lifecycle Management Model Is Right for You**](https://trailhead.salesforce.com/en/content/learn/trails/determine-which-application-lifecycle-management-model-is-right-for-you?trailmix_creator_id=strailhead&trailmix_slug=architect-dev-lifecycle-and-deployment)

- Application Lifecycle Management (ALM)
  - Plan Release
  - Develop
  - Test
  - Build Release
  - Test Release
  - Release
- Three dev models that Salesforce supports for ALM
  - Change Set Development
  - Org Development
  - Package Development
- Change Set Development Model
  - General Process
    - Leverage individual dev sandboxes for Develop and Test
    - Move to dev pro or partial sandbox for Build Release
    - Move to full sandbox for Test Release
    - Move to prod for Release
  - Changes must be tracked manually, especially those that are not supported by change sets (and require changes in target orgs)
  - Change sets require the target org to allow a deployment connection from the source org
  - Changes are not possible after upload, so need to clone change sets for new org
  - Validation locks components included in deployment, can run with different test levels
  - Deploy after successful validation
  - Change sets have specific behavior for permission sets and profiles
    - Always included
      - Permission sets
        - Standard object and field permissions
        - User permissions (e.g. API enabled)
      - Profiles
        - Tab settings
        - Page layout and record type assignments
        - Login IP ranges
        - User permissions
    - Requires component to be in change set
      - Permission sets
        - Apex class and Visualforce page access
      - Profile
        - Assigned apps
        - Custom object and field permissions
        - Apex class and Visualforce page access
- Org Development
  - General Process
    - Develop and Test occur in dev sandboxes, leverage `force:source:deploy` and `force:source:retrieve`
    - Build Release in a dev pro sandbox
    - Test Release in a partial sandbox
    - Release to a full sandbox and prod
  - Leverages source control repo to handle source of truth for customizations, does not require change sets
  - Build releases via `force:source:convert` and deploy via `force:mdapi:deploy` (Metadata API deployments)
- Package Development
  - General Process
    - Develop and Test occurs in scratch orgs via `force:source:push` and `force:source:pull`
    - Use CI to compile and test changes in scratch orgs
    - Use CD to build and install packages from repo in dev pro and partial sandboxes
    - Use CD to release to full sandbox and prod
  - Leverage `force:package:version:create` and `force:package:install`
  - Shared metadata belong in a base package, which other packages may reference

[**Governance Basics**](https://trailhead.salesforce.com/content/learn/modules/governance-basics?trailmix_creator_id=strailhead&trailmix_slug=architect-dev-lifecycle-and-deployment)

- Governance examples
  - Compliance
  - Risk assessment
  - Cost efficiencies
  - Velocity
- Without governance
  - No vision for the platform
  - Lack of alignment between teams
  - Low adoption
  - Too many enhancement requests (lack of cohesion)
- Exec steering committee: actions, overall health, KPIs, vision and strategy, budget, risks
- Project management: actions, overall health, resources and requirements, risks

[**Salesforce Agile Basics**](https://trailhead.salesforce.com/content/learn/modules/salesforce-agile-basics?trailmix_creator_id=strailhead&trailmix_slug=architect-dev-lifecycle-and-deployment)

- When to Choose Waterfall
  - Simple work
    - The work is simple and predictable
    - Anyone can determine how to complete the work
  - Complicated work
    - The work is predictable, but requires expertise
    - The work can be automated
- When to choose Agile
  - Complex work
    - The work is based on consistent feedback, risk, and innovation
- Agile is comprised of
  - Core values
  - Principles
  - Frameworks
  - Practices
- Lean Principles
  - Respect people
  - Eliminate waste
  - Deliver fast
  - Just in time decisions
  - Optimize the whole
  - Create knowledge
  - Build quality in

[**Sandbox Basics**](https://help.salesforce.com/articleView?id=sf.deploy_sandboxes_intro.htm&type=5)

- Types: Dev, Dev pro (for larger datasets), partial, and full (latter two can include data dopied over)
- Templates are used to define which objects should have data copied for partial and full
- Cloning sandboxes copies its data and metadata to new sandbox, must have same license type as the source org (e.g. full clones to full)

[**Sandbox licenses and storage limits by type**](https://help.salesforce.com/articleView?id=sf.data_sandbox_environments.htm&type=5)

- Developer
  - Refresh interval: 1 day
  - Data storage: 200MB
  - File storage: 200MB
- Developer Pro
  - Refresh interval: 1 day
  - Data storage: 1GB
  - File storage: 1GB
- Partial => must use sandbox template
  - Refresh interval: 5 days
  - Data storage: 5GB
  - File storage: same as prod
- Full => can use sandbox template
  - Refresh interval: 29 days
  - Data storage: same as prod
  - File storage: same as prod
- Sandboxes per edition
  - PE: 10 dev, partial and full not available
  - EE: 25 dev, 1 partial
  - UE/PXE: 100 dev, 5 dev pro, 1 partial, 1 full
- Sandbox add on SKUs come with additional dev sandboxes
  - Dev pro => 5 dev
  - Partial => 10 dev
  - Full => 15 dev
- Data storage limits are enfoced in sandboxes

[**Secure your sandbox data with Salesforce Data Mask**](https://help.salesforce.com/articleView?id=sf.data_mask_overview.htm&type=5)

- Data Mask is an add on product to assist with PII and NPI in sandboxes
- Masking
  - Random (e.g. Suzy Peters => jdsfjsf sdfsfsdfsdf)
  - Familiar Values (e.g. John Doe => Janet Smith)
  - Pattern generated (e.g. maria@example123.com => person@word567.com)
  - Delete
- Exists as a managed package that is installed in production org
- Org level settings
  - Anonymize case comments
  - Delete all records from `EmailMessage` sobject
  - Delete all Chatter activity
- Define filter criteria for the data that should be masked
- Data Mask disables automation when running
  - Triggers
  - Workflow rules
  - Validation rules
  - Flows
  - Field history tracking
  - Feed tracking
- Considerations
  - Required fields need values
  - Records that conflict with duplicate rules are skipped
  - Workflow rules, triggers, and validation rules in managed packages are not deactivated
  - Serial mode can be used if there are errors

[**Org Development Model**](https://trailhead.salesforce.com/content/learn/modules/org-development-model?trailmix_creator_id=strailhead&trailmix_slug=architect-dev-lifecycle-and-deployment)

  - General Process
    - Develop and Test occur in dev sandboxes, leverage `force:source:deploy` and `force:source:retrieve`
    - Build Release in a dev pro sandbox
    - Test Release in a partial sandbox
    - Release to a full sandbox and prod
  - Leverages source control repo to handle source of truth for customizations, does not require change sets
  - Build releases via `force:source:convert` and deploy via `force:mdapi:deploy` (Metadata API deployments)
- Package Development
  - General Process
    - Develop and Test occurs in scratch orgs via `force:source:push` and `force:source:pull`
    - Use CI to compile and test changes in scratch orgs
    - Use CD to build and install packages from repo in dev pro and partial sandboxes
    - Use CD to release to full sandbox and prod
  - Leverage `force:package:version:create` and `force:package:install`
  - Shared metadata belong in a base package, which other packages may reference

[**Simplify Your Development Process with Continuous Integration**](https://trailhead.salesforce.com/en/content/learn/trails/move-to-a-continuous-integration-development?trailmix_creator_id=strailhead&trailmix_slug=architect-dev-lifecycle-and-deployment)

Notes for this are captured in the next two links, as this is a trail comprised of those two modules.

[**Git and GitHub Basics**](https://trailhead.salesforce.com/content/learn/modules/git-and-git-hub-basics?trailmix_creator_id=strailhead&trailmix_slug=architect-dev-lifecycle-and-deployment)

- Git
  - Repos: collection of source files
  - Commits: snapshots of changes to source files
  - Branch: different paths within the same repo with their own set of commits 
  - Merge: combines multiple branches
  - Tag: pointer to a commit
- GitHub 
  - Hosts git repos and all of their associated functionality
  - Issues: basically ticketing / collaboration
  - Pull requests: package of commits to merge
  - Actions: basically a CI/CD capability with tasks that comprise a workflow
  - Projects: a collection of issues in a nice board format
  - Wiki: also exists for documentation, not called out in Trailhead module
- GitHub Workflow
  - Create a branch
  - Make changes
  - Submit pull request to another branch
  - Merge accepted pull request into that branch
- Working within historical changes
  - `git log`: see the changes
  - `git diff`: compare file across commits, branches, or tags
  - `git revert`: new commit that is opposite of what is being undone 
  - `git reset`: rewinds (including those commits) to a prior state 
  - Recursive merge: combines changes from a branch into current state of the branch to which the merge is occurring
  - Fast forward merge: pulls the original branch forward to where the new branch is if no changes occurred to original branch
  - `git rebase`: creates a fast forward merge if git would have done a recursive merge

[**Develop an App with Salesforce CLI and Source Control**](https://trailhead.salesforce.com/content/learn/projects/develop-app-with-salesforce-cli-and-source-control?trailmix_creator_id=strailhead&trailmix_slug=architect-dev-lifecycle-and-deployment)

- `auth:web:login` allows for authenticating SFDX via browser, can set dev hub via `--setdefaultdevhubusername` flag
- `force:org:list` to see all authorized orgs
- `force:project:create` to create a new project
- `force:source:retrieve` can use a package.xml file as its `--manifest` to pull from the org 
- `force:data:tree:export` can pull records into project from org to simplify data seeding
- `force:org:create` to create a new scratch org
- `force:source:push` to push the files into that org
- `force:user:permset:assign` to assign permission sets by developer name
- `force:data:tree:import` to import data (which may have been exported via previous commant)
- `force:org:open` will open that org in the browser
- `force:apex:test:run` has parameters to assist with determining more than pass/fail on a specific test (or all tests)
- `force:source:pull` to get changes from org to local
- `force:source:deploy` to push changes into non-scratch org

[**Managing scratch orgs**](https://help.salesforce.com/articleView?id=sf.managing_scratch_orgs.htm&type=5)

- Enable dev hub to allow scratch orgs or if needing second gen packages (2GP), as those rely on scratch orgs
- Link a namespace to a dev hub and log into that dev org where the namespace is registered
- Beta feature can capture an org shape from a source org and leverage that for scratch orgs

[**Branching Strategy**](https://clickdeploy-team.medium.com/salesforce-source-control-5561ed917d0)

- Single main branch for all environments
  - Pros
    - Less branches to manage
    - Move changes to UAT automatically, manually deploy to prod
  - Cons
    - Inflexible
    - Requires coordination and blocking a dev pipeline (i.e. stop commits to main branch)
    - Production release is manual
- One branch per org, one branch per feature
  - Pros
    - Flexible
    - Deployment is automated (because changes are done via pull request to the org branch)
    - Deployment is predictable
  - Cons
    - Main and other branches will deviate over time
    - Environments and branches need to be refreshed over time
    - Pull requests are vulnerable to merge conflicts
- One branch per org, two feature branches per feature: basically a feature branch per org (e.g. feature_main, feature_uat)

[**Metadata API Developer Guide**](https://developer.salesforce.com/docs/atlas.en-us.api_meta.meta/api_meta/meta_intro.htm)

- Deploy and retrieve metadata, does not touch data
- Moves metadata to/from local file system and various orgs (prod, sandbox, scratch)
- Has an XML file to track metadata about your metadata (e.g. API version, name, etc)
- `deploy` and `retrieve` calls are used to facilitate transfer of data
- Relies upon a `package.xml` file to list out changes and `destructiveChanges.xml`, which is basically a `package.xml` for things to delete from target org during deployment
- Can pull the Metadata WSDL file down to use in local applications if desired
- Offers both SOAP and REST interfaces for handling deployments
- Metadata API maps a few calls to SOAP API
  - `createMetadata` => `create`
  - `updateMetadata` => `update`
  - `deleteMetadata` => `delete`
- Hardcoded references to sandbox name on a username are ignored (provided that format is used)
- Not all metadata types are available

[**Tooling API Developer Guide**](https://developer.salesforce.com/docs/atlas.en-us.api_tooling.meta/api_tooling/intro_api_tooling.htm)

- Use to build development tools or apps that work on metadata
- The following tasks are good candidates for using the Tooling API
  - Retrieve metadata about an object's field
  - Retrieve custom or standard object properties
  - Manage working copies of Apex classes and triggers and Visualforce pages and components
  - Manage working copies of static resource files
  - Check for updates and errors in working copies of Apex classes and triggers and Visualforce pages and components
  - Commit changes to your organization
  - Set heap dump markers
  - Overlay Apex code or SOQL statements on an Apex execution
  - Execute anonymous Apex
  - For sample code, see SOAP Calls and REST Overview
  - Generate log files for yourself or for other users
  - Set checkpoints with TraceFlag
  - Access debug log and heap dump files
  - Manage custom fields on custom objects
  - Access code coverage results
  - Execute tests, and manage test results
  - Manage validation rules and workflow rules
- 

[**Unit Testing on the Lightning Platform**](https://trailhead.salesforce.com/content/learn/modules/unit-testing-on-the-lightning-platform?trailmix_creator_id=strailhead&trailmix_slug=architect-dev-lifecycle-and-deployment)



[**Package Development Readiness**](https://trailhead.salesforce.com/content/learn/modules/package-development-readiness?trailmix_creator_id=strailhead&trailmix_slug=architect-dev-lifecycle-and-deployment)



[**Unlocked Packages for Customers**](https://trailhead.salesforce.com/content/learn/modules/unlocked-packages-for-customers?trailmix_creator_id=strailhead&trailmix_slug=architect-dev-lifecycle-and-deployment)



[**Quick Start: Unlocked Packages**](https://trailhead.salesforce.com/content/learn/projects/quick-start-unlocked-packages?trailmix_creator_id=strailhead&trailmix_slug=architect-dev-lifecycle-and-deployment)



[**Choose your tools for developing and deploying changes**](https://help.salesforce.com/articleView?id=sf.code_tools_ant.htm&type=5)



[**Continuous Integration**](https://developer.salesforce.com/docs/atlas.en-us.sfdx_dev.meta/sfdx_dev/sfdx_dev_ci.htm)



[**Unlocked Packages**](https://developer.salesforce.com/docs/atlas.en-us.sfdx_dev.meta/sfdx_dev/sfdx_dev_unlocked_pkg_intro.htm)



[**Apex Metadata API**](https://trailhead.salesforce.com/content/learn/modules/apex_metadata_api?trailmix_creator_id=strailhead&trailmix_slug=architect-dev-lifecycle-and-deployment)