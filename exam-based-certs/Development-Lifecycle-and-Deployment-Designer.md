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

- Use to build development tools or apps that work on metadata and leverage 
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
- Different types of objects
  - Programming: Apex, Visualforce, Lightning, etc
  - Setup: compact layouts, apps, etc
  - Tooling: code coverage, logs, etc
  - Operational: deployments, collections of metadata
- Can leverage both SOQL and SOSL to find metadata

[**Unit Testing on the Lightning Platform**](https://trailhead.salesforce.com/content/learn/modules/unit-testing-on-the-lightning-platform?trailmix_creator_id=strailhead&trailmix_slug=architect-dev-lifecycle-and-deployment)

- Unit tests: tests code's ability to meet specific expected results at a granular level
- Functional: tests code's ability to handle functionality
- Integration: tests code's ability to integrate with other systems
- Test data
  - Within a test method itself (that is also asserting results from code)
  - Create a factory that creates a set of records (as its own class, call methods to create from other places)
  - `@TestSetup` method in the test class to ensure that each method has the same baseline, without requiring a call to factory to create test data
  - Upload a CSV as Static Resource and use `Test.loadData` method to specify the SObjectType and the name of that data file
- Positive tests: return expected result when presenting valid data to code
- Negative tests: ensures that code handles invalid data, unexpected inputs, and etc
- Permission based tests: create or leverage users with different profiles/permission sets and use `System.runAs` block to validate the code works as expected
- Lightning Web Component tests: leverages Jest, which is adopted by Salesforce to test components in isolation, its `@api`, user interactions via clicks, and DOM + events output
- Mocks and Stubs
  - Mocks are object level: `Test.setMock` for things like validating callouts from `HttpCallout` in code
  - Stubs are method level: `Test.setStub` to remove dependency on exactly how a method works when testing

[**Package Development Readiness**](https://trailhead.salesforce.com/content/learn/modules/package-development-readiness?trailmix_creator_id=strailhead&trailmix_slug=architect-dev-lifecycle-and-deployment)

- Unlocked packages are repeatable, scriptable, and trackable for managing changes in orgs
- Packages are used to migrate changes between environments
- Determine current state of programmatic and declarative customizations around
  - Patterns (e.g. one trigger / flow per object)
  - Logic (e.g. handler classes)
  - Naming conventions
  - Testing patterns and adherence to best practices
  - Comments and descriptions
  - API versions

[**Unlocked Packages for Customers**](https://trailhead.salesforce.com/content/learn/modules/unlocked-packages-for-customers?trailmix_creator_id=strailhead&trailmix_slug=architect-dev-lifecycle-and-deployment)

- Changes can occur to production with metadata included in unlocked package, although will be overwritten on next version installation (unless change is included in that version as well)
- Create new packages via `force:package:create` with a path to the metadata
- Create new package versions via `force:package:version:create` with a reference to the package `-p`
- Package aliases are captured in `sfdx-project.json` with the accompanying IDs
- Promote from beta to release via `force:package:version:promote` with the `-p` to the alias of that specific version
- Use `force:package:install` with `--package` to the alias of that version that is desired for the given org
- Three models for untangling into packages
  - App-based (e.g. Commissions App, HR App)
  - Customizations-based (e.g. Sales, Service, etc)
  - Shared library (e.g. a base package that other packages leverage)
- Package dependencies
  - Unlocked packages can depend on AppExchange packages
  - Unlocked packages can depend on other unlocked packages
  - Unlocked packages can have deep dependencies on other unlocked packages 

[**Quick Start: Unlocked Packages**](https://trailhead.salesforce.com/content/learn/projects/quick-start-unlocked-packages?trailmix_creator_id=strailhead&trailmix_slug=architect-dev-lifecycle-and-deployment)

Basically same as module directly above

[**Choose your tools for developing and deploying changes**](https://help.salesforce.com/articleView?id=sf.code_tools_ant.htm&type=5)

- Dev Console
- VS Code (via Salesforce Extensions)
- Directly via Metadata API (meaning you can use whatever you want to author those pieces of metadata)
- Ant Migration Tool: built on Apache Ant to assist with specific tasks, includes `build.properties` and `build.xml` files for credentials and tasks to execute respectively
- Change Sets

[**Continuous Integration**](https://developer.salesforce.com/docs/atlas.en-us.sfdx_dev.meta/sfdx_dev/sfdx_dev_ci.htm)

- Various sample repos exist for Org and Package Development Models
  - AppVeyor
  - Bamboo
  - Bitbucket
  - CircleCI
  - GitLab
  - Jenkins
  - TravisCI

[**Unlocked Packages**](https://developer.salesforce.com/docs/atlas.en-us.sfdx_dev.meta/sfdx_dev/sfdx_dev_unlocked_pkg_intro.htm)

- Unlocked an org dependent uunlocekd packages are slightly different
  - Org dependent are built for specific prod and sandbox orgs, only can be installed in orgs that have metadata on which the package relies
- Namespace can be assigned to unlocked packages
- `sfdx-project.json` file contains 
  - Package dependencies, both managed and unlocked
  - Metadata dependencies for Apex tests via permission sets and permission set licenses
- Unlocked packages allow for deprecating metadata from the package or moving that metadata to a different unlocked package
- Unlocked packages can be pushed to subscriber orgs via 2GP push upgrades

[**Apex Metadata API**](https://trailhead.salesforce.com/content/learn/modules/apex_metadata_api?trailmix_creator_id=strailhead&trailmix_slug=architect-dev-lifecycle-and-deployment)

- Supports page layouts and custom metadata types are supported currently
- Metadata namespace can retrieve metadata from an org, update metadata, and deploy to an org
- Can also be used to execute actions after a deployment occurs via `DeployCallback` interface
- Good use is creating an admin friendly tool to manage custom metadata types for reference table style features (e.g. tax rates)
- Setup => Apex Settings => Deploy Metadata from Non-Certified Package Versions via Apex allows non-certified packages (e.g. managed packages that have not gone through security review) to update an org; regardless will allow unmanaged and certified to modify
- Use protected metadata to prevent other managed packages, your package's subcribers from viewing metadata