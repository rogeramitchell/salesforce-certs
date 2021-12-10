## Resources

### Salesforce Content

- [Trailhead Overview](https://trailhead.salesforce.com/credentials/dataarchitectureandmanagementdesigner)
  - [Trailmix](https://trailhead.salesforce.com/en/users/strailhead/trailmixes/architect-data-architecture-and-management)
  - [Exam Guide](https://trailhead.salesforce.com/en/help?article=Salesforce-Certified-Data-Architecture-and-Management-Designer-Exam-Guide)

### Trailmix

[**Data Management**](https://trailhead.salesforce.com/content/learn/modules/lex_implementation_data_management?trailmix_creator_id=strailhead&trailmix_slug=architect-data-architecture-and-management)

- Import Data
  - Data Import Wizard: some objects, up to 50K rows
  - Data Loader: practically all objects, up to 5M rows, can be automated via CLI
- Export Data
  - Data Export Service: manually every 7 days (weekly) or 29 days (monthly), PE and DE orgs only allow every 29 days (monthly)
  - Data Loader: manual or automated via CLI 

[**Large Data Volumes**](https://trailhead.salesforce.com/content/learn/modules/large-data-volumes?trailmix_creator_id=strailhead&trailmix_slug=architect-data-architecture-and-management)

- Data Skew
  - Account: too many child records cause record locking and sharing issues
  - Ownership: too many records owned by a single user (e.g. a system or integration user)
  - Lookup: too many records associated with a single record in a lookup object, where concurrent DML can cause issues
- External Objects
  - Leverage off platform storage and Salesforce Connect (a.k.a. Lightning Connect) to surface data in Salesforce
  - Relationship Fields
    - Lookup: Salesforce ID matches to parent; parents are standard / custom, children are standard / custom / external
    - External Lookup: standard External ID matches to parent; parents are external / children are standard / custom / external
    - Indirect Lookup: custom field with External ID and unique constraints matches to parent; parents are standard / custom, children are external
- Queries
  - SOSL: multiple sObjects, returns 2K records
  - SOQL: single object with children and fields via relationship, returns 50K records
  - Batch Apex: query and asynchronously process up to 50M records in up to 200 records per batch
  - Bulk API Queries: query and retrieve up to 15GB of data in 1GB files, returns CSV, JSON, and XML
- Bulk Queries
  - Query error can be thrown for a timeout, requires simpler query
  - If it succeeeds, retrieves the results and may hit a 1GB file size limit or exceed 10 minutes
    - 15 retries occur with cached data for completed results, then an error is thrown
    - Resolve that error with PK Chunking header 
  - Results stored for 7 days
- Skinny Tables
  - Custom table with standard / custom fields
  - Do not contain deleted records
  - Custom indexes from base table are copied to skinny table 
  - Improvements to speed can occur by filter on fields containing numeric / string date parts (e.g. Year__c, Month__c, Day__c)
- Loading LDV
  - Org wide sharing defaults: private causes sharing calculations at time of load, public read/write allows for deferring processing
  - Complex object relationships: more lookups means more checks, populate those later
  - Sharing rules
    - Ownership based sharing rules cause sharing calculations if record owners are part of those rules 
    - Criteria based sharing rules cause sharing calculations if fields match criteria 
  - Workflow, validation, triggers: can slow down processing, disable unless necessary
  - Role hierarchy itself does not impact performance for loads
  - APIs
    - SOAP API is optimized for a smaller loads
    - Bulk API allows for parallelization and more rows per batch (up to 10K)
- Extracting LDV
  - Bulk API splits queries into 100K records by default, can be lower or up to 250K
  - Use PK Chunking on tables with more than 10M records or when queries timeout
  - Truncating objects can permanently delete records from an object, but only if that object is not referenced by another object, is not master on a master-detail, part of reporting snapshot, has custom indexes or external IDs, or has a skinny table

[**Salesforce Anti-Patterns: A Cautionary Tale**](https://developer.salesforce.com/blogs/engineering/2014/11/salesforce-anti-patterns-a-cautionary-tale)

- Takeaways
  - Pre-sort child records by the parent's ID to avoid locking issues with Bulk API parallelization
  - Sharing configuration can impact performance 
  - Full extracts to other systems is not a best practice, use SystemModstamp (indexed) to identify recently modified records
  - Use triggers to populate fields instead of formulas

[**Avoid Account Data Skew for Peak Performance**](https://developer.salesforce.com/blogs/engineering/2012/04/avoid-account-data-skew-for-peak-performance)

- Many child records related to a single Account causes data skew
- When a child record is modified, it locks both the child and Account for a very short period, but that can be concurrent with another update 
- Changing an Account owner causes recalculation for children as well, if sharing is configured that way
- Avoid more than 10K records related to a single parent

[**Customize Your Data Model**](https://www.youtube.com/watch?v=J5t6XBBf3ew)

[**Extreme Force.com Data Loading, Part 1: Tune Your Data Model**](https://developer.salesforce.com/blogs/engineering/2013/02/extreme-salesforce-data-loading-part-1-tune-your-data-model)

- Wide objects: implement skinny tables
- Slow queries: use indexed fields
  - Primary keys: Id, Name, OwnerId
  - Foreign keys: lookup, master-detail, CreatedById, LastModifiedById
  - Audit dates: CreatedDate, LastActivityDate, SystemModstamp (not LastModifiedDate)
  - Custom fields with these constraints: unique, external ID
- Ownership skew: don't do it, but if you must, in their own role at top of role hierarchy
- Parent / child skew: keep less than 10K child records to a single parent record

[**Data Quality**](https://trailhead.salesforce.com/content/learn/modules/data_quality?trailmix_creator_id=strailhead&trailmix_slug=architect-data-architecture-and-management)

- Examples
  - Missing records
  - Duplicate records
  - No standardization (e.g. state/province)
  - Incomplete records
  - Stale data
- Assess quality per business objective and stakeholder group
- Create reports and dashboards to highlight quality

[**Manage Duplicate Records**](https://help.salesforce.com/s/articleView?id=sf.managing_duplicates_overview.htm&type=5)

- Manage and resolve one off issues with Potential Duplicates component
- Create duplicate jobs to identify duplicate record sets across org
- Use matching rules to define criteria
- Use duplicate rules to define behavior when a duplicate is identified on create and update
- Salesforce Mobile does not alert when users about existing duplicates or when they are about to create one

[**Data Governance and Stewardship**](https://a.sfdcstatic.com/content/dam/www/ocms-backup/assets/pdf/misc/data_Governance_Stewardship_ebook.pdf)

- Assess current data
  - Who is using it?
  - What are business needs?
  - Which data is used most?
  - How is it being used?
- Data Quality Measures
  - Age
  - Completeness
  - Usage
  - Accuracy
  - Consistency
  - Duplication
- Governance Plan
  - Data definitions
  - Quality standards
  - Roles and ownership (tip: use RACI)
  - Security and permissions
  - Quality control
- MDM assists with consistency by:
  - Record creation assistance
  - Record maintenance across systems
  - Regulatory and compliance enforcement
  - Enterprise wide visibility 
- Implement plan
  - Standardize 
  - Remove duplicates
  - Compare to a referential source (e.g. third party data providers that are trusted)
  - Create scheduled data maintenance tasks
  - Continually monitor and adapt

[**Person Accounts**](https://help.salesforce.com/s/articleView?id=account_person.htm&language=en_US&type=5)

- Person accounts can only be merged with other person accounts
- Person accounts can only be enabled for Customer Experiences, not Partner Experiences
- Contacts to Multiple Accounts facilitates connections to other Accounts and Contacts
- Integration with Pardot requires additional configuration

[**Contacts to Multiple Accounts**](https://help.salesforce.com/s/articleView?id=shared_contacts_overview.htm&language=en_US&type=5)

- Direct relationship via `Contact.AccountId`
- Indirect relationship via `AccountContactRelation` 
- Contact and Related Contacts related lists are available, Contacts shows directly related

[**Manage Products**](https://help.salesforce.com/s/articleView?id=products_landing_page.htm&language=en_US&type=5)

- Products can exist in multiple price books as price book entries
- Cloning a product will clone its related price book entries, but:
  - Only for those price books to which you have access
  - Fields to which a user has read only access are not cloned

[**Reference Data Management Key Concepts**](http://www.mdmgeek.com/2013/03/21/reference-data-management-an-overview/)

- Reference data examples
  - State codes, country codes, postal codes
  - NAICS, GICS codes

[**Implementing State and Country Picklists**](https://help.salesforce.com/s/articleView?id=sf.admin_state_country_picklists_overview.htm&type=5)

- Contains default set, some values from Data.com are not part of default
- Configure the desired set
- Scan data and customizations that reference state/country fields
- Convert data to new values
- Turn on feature
- Ensure leveraging Code values for comparison, but ensure that code and label values match when updating

[**Lightning Platform API Basics**](https://trailhead.salesforce.com/content/learn/modules/api_basics?trailmix_creator_id=strailhead&trailmix_slug=architect-data-architecture-and-management)

[**Apex Basics & Database**](https://trailhead.salesforce.com/content/learn/modules/apex_database?trailmix_creator_id=strailhead&trailmix_slug=architect-data-architecture-and-management)

[**Long- and Short-Term Approaches for Tuning Force.com Performance**](https://developer.salesforce.com/blogs/engineering/2013/03/long-and-short-term-approaches-for-tuning-force-com-performance)

- Only store what is needed
- Know expected data growth rates
- Define criteria for archiving and purging 

[**Query Plan Tool**](https://help.salesforce.com/s/articleView?id=000334796&type=1)

- Enable in Developer Console's settings
- Use to determine if a filter is selective 
  - Standard: 30% of first 1M rows, 15% of remaining
  - Custom: 10% of first 1M rows, 5% of remaining, and maxes out at 333,333 records (so up to 5.6M total records)
- Plan results
  - Cardinality: estimated number of records returned
  - Fields: indexed fields used by Query Optimizer
  - Leading operating type; index, sharing, tablescan, other
  - Cost: values over 1 are not selective
  - sObject cardinality: approximate record count of object
  - sObject type: object name being queried

[**Deployments with LDV Best Practices**](https://resources.docs.salesforce.com/sfdc/pdf/salesforce_large_data_volumes_bp.pdf)

- Use efficient queries
- Implement skinny tables
- Create custom indexes
- Implement divisions for partitioning
- Defer sharing for large loads
- Delete data that is no longer relevant
- Integrate data from external datastores via mashups and/or External Objects

[**Query and Search Optimization**](http://resources.docs.salesforce.com/194/0/en-us/sfdc/pdf/salesforce_query_search_optimization_developer_cheatsheet.pdf)

[**Import and Export with Data Management Tools**](https://trailhead.salesforce.com/content/learn/projects/import-and-export-with-data-management-tools?trailmix_creator_id=strailhead&trailmix_slug=architect-data-architecture-and-management)

- Data Import Wizard exists
- Dataloader.io also exists

[**Duplicate Management**](https://trailhead.salesforce.com/content/learn/modules/sales_admin_duplicate_management?trailmix_creator_id=strailhead&trailmix_slug=architect-data-architecture-and-management)

- Matching rules: criteria for how a duplicate is identified
- Duplicate rules: what to do when duplicates are identified

[**Extracting LDV in Force.com**](https://developer.salesforce.com/blogs/engineering/2013/06/extracting-large-data-volume-ldv-in-force-com)

- Chunk data into smaller sets (e.g. by querying against an Id or External ID)
- Run requests in parallel with Bulk API
- Add a skinny table if extracting under 100 fields from base table
- 

[**10 Steps to Data Quality and Trusted Information**](http://mitiq.mit.edu/IQIS/Documents/CDOIQS_200977/Papers/01_02_T1D.pdf)

1. Define business need and approach
1. Analyze information environment
1. Assess data quality
1. Analyze business impact
1. Identify root cause
1. Develop improvement plans
1. Prevent future data errors
1. Correct current data errors
1. Implement controls
1. Communicate actions and results throughout above steps

[**Automatically Get Geocodes for Addresses**](https://help.salesforce.com/s/articleView?id=data_dot_com_clean_admin_automatically_get_geocodes_for_addresses.htm&type=5)

- Data.com Geo service can update latitude, longitude, and accuracy fields on Accounts, Contacts, and Leads
- Accuracy values indicate the quality of the coordinates: Address, NearAddress, Block, Street, ExtendedZip, Zip/Postal Code, Neighborhood, City, County, State/Province, Unknown

[**AppExchange Data Apps**](https://appexchange.salesforce.com/collection/data)

- The AppExchange exists, and you can use it!

[**Agile Data Governance**](http://agiledata.org/essays/dataGovernance.html)

- Challenges
  - Data governance doesn't fit into overall governance 
  - Efforts are ignored
  - Traditional methods are too onerous
  - Governors are slow to respond
  - Data teams are not perceived as having additive value
- Strategies
  - Include data professionals
  - Educate devs
  - Allow teams to define their work methodology
  - Align team and architecture
  - Embed compliance 
  - Build flexible architectures
  - Be pragmatic
  - Empower self organizing teams

[**Data Governance & Stewardship Best Practices**](https://www.salesforce.com/video/194468/)

- Data governance requires people, processes, and systems to be aligned
- Mix of customizations, routing, enablement, enrichment, and automation
- More than half the audience left between the start and end 😬

[**Loading Large Data Sets with Bulk API**](https://developer.salesforce.com/docs/atlas.en-us.api_asynch.meta/api_asynch/asynch_api_intro.htm)

- Bulk API 2.0
  - Supports same OAuth 2.0 flows as other Salesforce REST APIs
  - Ingests via CSV 
  - Automatically implements PK chunking
  - Limits by total records per day: 150M records
  - Not compatible with Data Loader
- Bulk API
  - Uses session from login call to SOAP API
  - Ingests via CSV, JSON, XML, and binary
  - PK chunking is optional, default disabled
  - Limits by quantity of batches per day: 15,000 batches, which can be up to 150M records
  - Available in Data Loader

[**Master Data Management (MDM)**](https://www.slideshare.net/tataconsultancyservices/master-data-management-mdm-plm-in-context-of-enterprise-product-management)

- MDM acts as master for different domains of data
- Variety of ways to connect datastores to MDM: ESB, ETL, ELT
- MDM feeds downstream data warehouses and data lakes

[**Territory Mgmt Implementation Guide**](http://resources.docs.salesforce.com/202/18/en-us/sfdc/pdf/salesforce_implementing_territory_mgmt2_guide.pdf)

- 

[**Use Batch Apex**](https://trailhead.salesforce.com/content/learn/modules/asynchronous_apex/async_apex_batch)

- Batch has logic that fires during start and finish for entire batch, execute method is called for each sub-batch of 200 sObjects (not always a record, can be an iterable object in code)
- Stateful batches can maintain and access instance level details (e.g. counting exactly how many instances of something occurred across sub-batches)
- Batches can also make callouts to external systems

[**Asynchronous Apex**](https://trailhead.salesforce.com/content/learn/modules/asynchronous_apex?trailmix_creator_id=strailhead&trailmix_slug=architect-data-architecture-and-management)

[**Backup and Restore Essentials Part 1**](https://developer.salesforce.com/blogs/2015/03/salesforce-backup-and-restore-essentials-part-1-backup-overview-api-options-and-performance)

- Backup types: full, incremental, partial (e.g. only specific segments of a given object)
- Mixture of backup types is appropriate
  - Weekly full backup
  - Daily incremental backup
  - Monthly partial backup that can be used for archival
- Determine security mechanisms for accessing backup data, as a function of encryption in transit and rest, who has access, and infrastructure availability / redundancy / durability
- Restoring data may be involved for some or all records to complete or partial states (e.g. all fields, some fields)

[**Backup and Restore Essentials Part 2**](https://developer.salesforce.com/page/Salesforce_Backup_and_Restore_Essentials_Part_2)

- Restores can be a single record, a logical set (e.g. records owned by a single user, metadata from a deployment, an entire object), or an entire org

[**Backup and Restore Essentials Part 3**](https://developer.salesforce.com/blogs/engineering/2016/02/salesforce-backup-restore-essentials-part-3-learn-customers-experience)

- Salesforce Data Recovery: additional cost, Salesforce keeps data up to 90 days
- Scheduled Data Export: generate your own backups weekly or monthly
- Data Loader: manual or automate your own backups
- Organization Sync: doesn't exist anymore, but it sounded cool at the time!
- Salesforce's Professional Services: hire Salesforce to spin up something for you instead of DIY

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

[**Managing Task Locks for Data Loads**](https://developer.salesforce.com/blogs/engineering/2014/08/managing-task-locks-data-loads)

- Tasks lock the records in `AccountId`, `WhoId`, and `WhatId` when loading
- Sort by `AccountId` when loading and attempt using parallel jobs
- Alternatively, use a controlled feed load that intelligently creates serialized jobs based on data

[**PK Chunking**](https://developer.salesforce.com/blogs/engineering/2015/03/use-pk-chunking-extract-large-data-sets-salesforce)

- Available for most standard and all custom objects
- Add a header to the Bulk API job (Bulk API 2.0 has this enabled automaticaly)

[**Tableau CRM Dashboard Navigation**](https://trailhead.salesforce.com/content/learn/modules/wave_exploration_dashboard_navigation?trailmix_creator_id=strailhead&trailmix_slug=architect-data-architecture-and-management)

