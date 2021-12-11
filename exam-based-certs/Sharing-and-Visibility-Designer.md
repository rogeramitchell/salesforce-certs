## Resources

### Salesforce Content

- [Trailhead Overview](https://trailhead.salesforce.com/credentials/sharingandvisibilitydesigner)
  - [Trailmix](https://trailhead.salesforce.com/en/users/00550000006yDdKAAU/trailmixes/architect-sharing-and-visibility)
  - [Exam Guide](https://trailhead.salesforce.com/help?article=Salesforce-Certified-Sharing-and-Visibility-Designer-Exam-Guide)

### Trailmix

[**A Guide to Sharing Architecture**](https://resources.docs.salesforce.com/224/latest/en-us/sfdc/pdf/sharing_architecture.pdf)

- Licenses
  - Full Sharing Model
  - High Volume Customer Portal (includes Community and Service Cloud licenses) use a foreign key match between the portal user and data on Account + Contact lookups
  - Chatter Free: does not have a sharing model
- Sharing Architecture Upside Down Triangle (More Precision Towards Bottom)
  1. Territory Hierarchy Access
  1. Team Access
  1. Manual Sharing
  1. Sharing Rules
  1. Role Hierarchy
  1. Org Wide Defaults
  1. Profile + Permission Sets
- If a single user must own more than 10K records, either ensure that user has no role or their role is at top of role hierarchy
- Grant Access Using Hierarchies can disable/enable hierarchal access to records via role hierarchy on custom objects only
- Role hierarchy use cases
  - Management access: managers see/do what their subordinates see/do
  - Management reporting: rollup so higher sees more than subordinates
  - Dividing organizational branches
  - Dividing data between people within same role
- Public groups can include users, roles, territories, and other groups
  - Sharing to an arbitrary group of people via sharing rule or manual sharing
  - Leverage Grant Access Using Hierarchies to disable/enable people above group members from seeing data via role hierarchy
- Ownership based sharing rules
  - Try to keep this to under 1K sharing rules per object
  - Share data from owners to other people (via roles, public groups, territories)
- Criteria based sharing rules
  - Try to keep this to under 50 sharing rules per object
  - Uses record field criteria to share with people (via roles, public groups, territories)
- Manual sharing is possible to provide sharing to a specific record
- Teams
  - Available on Account, Opportunity, and Case
  - Only owners, people higher in hierarchy, and administrators can add/change team members
- Territory hierarchy
  - Only for Account, Opportunity, and detail objects to Account and Opportunity (via master-detail relationship)
  - Allows a single user to exist in different hierarchy levels 
- Programmatic sharing (f.k.a. Apex managed sharing)
  - Only use when no other method works or poor performance exists with native sharing
  - Integrate with an external system to define access to records
  - Either provide a custom reason or leverage the "manual share" option; latter is manageable from within Salesforce similar to manual sharing above
- Large data volumes can cause a large volume of share records, which slows transactions and record access

[**Protect Your Salesforce Data**](https://trailhead.salesforce.com/en/content/learn/trails/security?trailmix_creator_id=strailhead&trailmix_slug=architect-sharing-and-visibility)

- Access controls
  - Enable and enforce MFA
  - Restrict IP ranges from which users can log in
  - Freeze and deactivate users 
  - Limit to least privilege
  - Encrypt data
  - Trigger and monitor events
- Permission set groups can be leveraged to combine a set of permission sets 
- Muting permission sets within a permission set group can specifically suppress / disable permissions
- Session based permission sets are assigned when a given session is active
  - Insert a record into `SessionPermSetActivation` with session ID and permission set ID to activate
  - Possible via Apex, API, and Flow
- Salesforce Identity
  - Single Sign On:  Salesforce as acts as the IdP for other apps
  - Connected Apps: allow third party apps to access Salesforce
  - Social Sign On: log into Salesforce via external authenticate from social networkrs
  - MFA: either use an authenticator app or security key
  - My Domain: custom subdomain for your org
  - Identity Connect: sync Microsoft Active Directory with Salesforce, which allows for provisioning and deactivation

[**User Management**](https://trailhead.salesforce.com/content/learn/modules/lex_implementation_user_setup_mgmt?trailmix_creator_id=strailhead&trailmix_slug=architect-sharing-and-visibility)

[**Salesforce Security Guide**](https://resources.docs.salesforce.com/224/latest/en-us/sfdc/pdf/salesforce_security_impl_guide.pdf)

- Control access to objects and fields with a mix of user permissions, object permissions, custom permissions, profiles, permission sets
- Control access to recods with role hierarchy, sharing rules, manual sharing, view/modify all in profiles and permission sets
- Encrypt data with either text (encrypted) fields or Shield Platform Encryption
- Monitor login history, field history tracking, setup audit trail
- Use event monitoring to track what users do within Salesforce

[**Who Can See My File?**](https://help.salesforce.com/articleView?id=collab_files_settings_perms.htm&type=0)

- Access levels
  - Private: owner and those with Modify All Data 
  - Privately Shared: file owner, users with Modify All Data or View All Data, and those users/groups with whom the file is shared
  - Your Company: all users
- Permission levels
  - Owner
  - Collaborator: owner less making the file private, restricting access, deletion
  - Viewer: collaborator less uploading new versions, editing details, changing permissions

[**Account Teams Overview**](https://help.salesforce.com/articleView?id=accountteam_def.htm&type=0)

[**Creating Custom List Views**](https://help.salesforce.com/articleView?id=customviews.htm&type=0)

- Visible to all users: includes Customer Community Plus, Partner Community, Lightning Platform Starter + Plus licenses
- Visible to certain groups of users: share to All Internal Users group to avoid leaking to Experience Cloud users

[**Share a Report or Dashboard Folder**](https://help.salesforce.com/articleView?id=analytics_share_folder.htm&type=0)

- Share to users, groups, roles, territories
  - Up to 25 entities via UI
  - Up to 100 entities via REST API
- Access levels: profiles dictate what a user can do to reports and dashboards
  - Viewer: view 
  - Editor: view and save 
  - Manager: view, save, share, rename, delete

[**Who sees what in Lightning Experience**](https://salesforce.vidyard.com/watch/B1bQnMFg2VyZq7V6zXQjPg?)

[**Classic Encryption for Custom Fields**](https://developer.salesforce.com/docs/atlas.en-us.securityImplGuide.meta/securityImplGuide/fields_about_encrypted_fields.htm)

- AES 128-bit encryption, can bring your own master encryption key
- View Encrypted Data required to see contents
- Always masked in email templates
- `apex:outputField` can present encrypted fields in Visualforce (if using standard components)
- Restrictions
  - Cannot have unique nor external ID constraints, no default value
  - Cannot be included in Lead conversion field mapping
  - Limited to 175 characters
  - Cannot be used in filters or criteria
  - Not searchable
  - Not available in Web-to-Lead and Web-to-Case fields, formula fields

[**Territory Management Basics**](https://trailhead.salesforce.com/content/learn/modules/territory-management-basics?trailmix_creator_id=strailhead&trailmix_slug=architect-sharing-and-visibility)

- Key terminology
  - Territory: organize groups of Accounts and users
  - Territory type: organize and create territories
  - Territory type priority: assists with defining a level of importance
  - Territory model: allows for previewing different structures before activating
  - Territory hierarchy: assign territories and view detail pages for related records to a territory
  - Territory model state: a status of territory model
- Assignments
  - Assignment rules can use fields to define whether a record should be assigned to a given territory
  - Manual assignments can be used
  - Assign users to one or more territories

[**Control Access to Records**](https://trailhead.salesforce.com/en/modules/data_security/units/data_security_records)

[**Locking Down Record Access**](https://developer.salesforce.com/blogs/engineering/2013/12/locking-down-record-access-in-salesforce.html)

- Remove Grant Access Using Hierarchies 
- Remove View All and Modify All from profiles and permission sets (both object and system permission)

[**Custom Permissions**](https://help.salesforce.com/articleView?id=custom_perms_overview.htm&type=0)

- Allows org specific access controls that can be referenced via validation rules, Apex (`FeatureManagement` class)
- Define dependencies where one custom permission requires another custom permission
- Assigned via permission sets 

[**Account Team Fields**](https://help.salesforce.com/articleView?id=accountteam_fields.htm&type=0)

- Sharing cannot be more restrictive than default sharing access
  - Account Access: read/write, read only
  - Case Access: read/write, read only, no access
  - Contact Access: read/write, read only; does not appear if org wide default is controlled by parent
  - Opportunity access: read/write, read only, no access
  - Team Member: user
  - Team Role: a picklist that describes the membership (e.g. Sales Engineer)

[**Built-in Sharing Behavior**](https://help.salesforce.com/articleView?id=sharing_across_objects.htm&type=0)

- Access to a child record implies access to the account
- Access to an account implies access to related children
- Account's portal/site user has read only access to the account and all related contacts
- Portal/site users whose contact is related to a case provides read/write access to that case

[**Implicit Sharing**](https://developer.salesforce.com/docs/atlas.en-us.draes.meta/draes/draes_object_relationships_implicit_sharing.htm)

[**Communities User Licenses**](https://help.salesforce.com/articleView?id=users_license_types_communities.htm&type=0)

- Licenses not required for unauthenticated experiences
- Up to 100 experiences allowed per org (regardless of status)
- Members vs Monthly Logins
  - Ratio of 20 users per monthly login (e.g. 1K monthly logins allows up to 20K active licenses)
  - Overages are charged on an annual basis (monthly logins * 12 = allowable logins per year)
- Experience Cloud limit of users per org
  - Partner Community, Customer Community Plus: 2M
  - Customer Community: 10M
- Guest user limits are based on monthly page views
  - Enterprise: 500K 
  - Unlimited: 1M
- Partners: Campaigns, Leads, Opportunities, Quotes, ability to modify their own reports and dashboards, has territory management
- Customer Community Plus: advanced sharing (not via sharing sets), create/view reports and view dashboards

[**Managing Access to the Partner Community**](https://trailhead.salesforce.com/modules/sf_partner_community/units/sf_partner_community_manage)

- Available option to manage for ISVs and SIs:
  - Users
  - Listings (on AppExchange)
  - Cases
  - Education
  - For SIs only:
    - Leads
    - Opportunities
    - Projects
    - Partnership

[**Access to Records for Community Users**](https://help.salesforce.com/articleView?id=networks_setting_light_users.htm&type=0)

- Enables sharing records with users based on their user's account and contact lookups that match to records with an account or contact lookup
- Also can bypass this with view all access on the profile (where appropriate)

[**Share Groups**](https://help.salesforce.com/articleView?id=networks_sharing_light_users.htm&type=0)

- Share records from high-volume user to internal users and other external users from that high-volume user's account

[**Territory Management Guide**](http://resources.docs.salesforce.com/210/10/en-us/sfdc/pdf/salesforce_implementing_territory_mgmt2_guide.pdf)

- Filter-based opportunity territory assignment uses an Apex class to manage assignments

[**Territory Management Differences**](https://help.salesforce.com/HTViewSolution?id=000212568)

- Original territory management did not offer
  - Multiple territories and hierarchies
  - Running a territory from a territory's detail page
  - Territory types, priorities, and models
  - Integration with collaborative forecasts
  - Separate of rule execution vs deployment
  - Deep clones of territory hierarchies
  - Rule sharing amongst many territories
  - Audit trail
  - Availability in Metadata API
  - Trigger on object that relates a user and territory

[**Deploying Territory Management**](http://resources.docs.salesforce.com/216/12/en-us/sfdc/pdf/salesforce_implementing_territory_mgmt2_guide.pdf)

[**Sharing a Record Using Apex**](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_bulk_sharing_creating_with_apex.htm)

- Write records to the object's share table (e.g. `AccountShare`, `SweetObject__Share`)
  - AccessLevel: Edit, Read, All
  - ParentId: record ID
  - UserOrGroupId: user, public group, group for a role, or territory
  - RowCause: can be "Manual" or a specific Apex Sharing Reason that is configured on the object (e.g. `Hero_Mode__c`)

[**Avoiding Account Data Skew**](https://developer.salesforce.com/blogs/engineering/2013/01/reducing-lock-contention-by-avoiding-account-data-skews.html)

- Limit a single Account from having more than 10K children in a single record
- Try using a public read/write sharing model to avoid sharing calculations

[**Group Membership Sharing**](https://developer.salesforce.com/blogs/engineering/2013/01/salesforce-group-membership-sharing-for-peak-performance.html)

- Any object with org wide default as public read-only or private gets a sharing table
- Group types
  - System: role and territory hierarchies, queues
  - User-defined: public and private groups

[**Record-Level Access: Under the Hood**](https://resources.docs.salesforce.com/sfdc/pdf/salesforce_record_access_under_the_hood.pdf)

- Salesforce calculates access when a user attempts to view one or many records (e.g. list views, reports, search results)
- Salesforce evaluation
  1. Finds the objects, uses those records IDs to check the sharing tables
  1. From sharing tables, collect user/group IDs with access,
  1. From group tables, check access for the user

[**Dynamic Data Sharing on Force.com**](https://developer.salesforce.com/blogs/engineering/2013/01/dynamic-data-sharing-on-force-com.html)

- Use criteria based sharing rules and Apex managed sharing to facilitate specific access levels as records change

[**Protecting Custom Sharing Code**](https://developer.salesforce.com/blogs/engineering/2013/02/protecting-force-com-custom-sharing-code.html)

- Use Apex managed sharing to define access levels and Apex sharing reasons
- Alternatively, send a message to an external service that can manage sharing records via a separate inbound calls to Salesforce
- Create a shadow table (not the actual underlying sharing table) to define access (e.g. Contact Teams)

[**Storing Sensitive Data**](https://developer.salesforce.com/page/Secure_Coding_Storing_Secrets)

- Sensitive data includes:
  - Passwords, passphrases
  - Encryption keys and tokens
  - Banking and credit info
  - NPI and PII

[**Enforcing Sharing Rules**](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_security_sharing_rules.htm)

- Execute anonymous code always applies `with sharing`
- Access keywords
  - When none applied to a class, it will run as `without sharing`
  - `with sharing` does not enforce object and field level security, just record access
  - `without sharing` does not enforce record access 
  - `inherited sharing` acts as `with sharing` when used as
    - Aura component controller
    - Apex REST service
    - Visualforce controller
    - Any other entrypoint of an Apex transaction

[**Create Custom Record Sharing Logic**](https://developer.salesforce.com/page/Using_Apex_Managed_Sharing_to_Create_Custom_Record_Sharing_Logic)

- NOTE: This is duplicative of a section above, content below is repeated from that section
- Write records to the object's share table (e.g. `AccountShare`, `SweetObject__Share`)
  - AccessLevel: Edit, Read, All
  - ParentId: record ID
  - UserOrGroupId: user, public group, group for a role, or territory
  - RowCause: can be "Manual" or a specific Apex Sharing Reason that is configured on the object (e.g. `Hero_Mode__c`)

[**Enforcing Object and Field Permissions**](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_classes_perms_enforcing.htm)

- Apply `WITH SECURITY_ENFORCED` keyword to SOQL to enforce object and field level access for current user
- Also, check access by describing objects and fields with `Schema.DescribeSObjectResult` and `Schema.DescribeFieldResult`

[**Designing Record Access**](https://resources.docs.salesforce.com/sfdc/pdf/draes.pdf)

- Group Membership: Roles, Public Groups, Territories
  - Make changes to the hierarchy from bottom up
  - Limit number of records owned by single user to 10K or less
  - Remove redundant paths to access (e.g. role hierarchy inherited sharing + an ownership based sharing rule)
  - Schedule large changes for off-peak times
- Data Access and Relationships
  - Use public read only or public read/write for non-confidential data
  - Avoid implicit shares to have child objects Controlled by Parent
  - Limit child records to 10K or less per single parent record
  - Sequence operations by the parent record's ID to avoid locking issues

[**Managing Group Membership Locks**](https://developer.salesforce.com/blogs/engineering/2012/09/group-membership-operation-already-in-progress-managing-group-membership-locks-for-success.html)

- Group membership lock is applied when any of these transactions occur
  - Role creation
  - Role deletion
  - Moving a role in the hierarchy
  - Adding a user to a territory
  - Removing a user from a territory
  - Moving a territory in the hierarchy
  - Territory deletion
  - Territory creation
  - Provisioning an internal user with an existing role
  - User role change
  - Provisioning a non-HVPU portal user under an account
  - Portal Account owner change
  - User Role change of a user who owns one or more portal accounts

[**Complex Sales Realignment**](https://developer.salesforce.com/blogs/engineering/2012/09/technical-enablement-case-study-complex-sales-realignment.html)

[**Using the Apex Crypto Class**](https://developer.salesforce.com/page/Apex_Crypto_Class)

- Decrypts, encrypts, generates keys, returns random data, signs and verifies signatures
- Throws its own set of exceptions when issues occur calling:
  - decrypt
  - decryptWithManagedIV
  - encrypt
  - encryptWithManagedIV

[**Platform Encryption**](https://help.salesforce.com/articleView?id=security_pe_overview.htm&type=0)

- Encrypt standard and custom fields, files, attachments, indexes
- Uses a tenant secret and master secret, although you can bring your own encryption key (be careful with that, Salesforce can't bail you out if you lose it)

[**The Difference Between Encryption Types**](https://help.salesforce.com/articleView?id=security_pe_vs_classic_encryption.htm&type=5)

- Classic: "free", only a specific field type, can mask the data with different mask types / characters, uses 128-bit AES
- Shield: additional cost, applies to many different types of fields and data, uses 256-bit AES

[**Shield Platform Encryption**](https://trailhead.salesforce.com/content/learn/modules/spe_admins?trailmix_creator_id=strailhead&trailmix_slug=architect-sharing-and-visibility)

- Encrypt only where necessary
- Backup and archive keys and data
- Encryption applies to all users