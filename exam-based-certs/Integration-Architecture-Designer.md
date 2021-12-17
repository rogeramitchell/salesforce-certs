## Resources

### Salesforce Content

- [Trailhead Overview](https://trailhead.salesforce.com/credentials/integrationarchitecturedesigner)
  - [Trailmix](https://trailhead.salesforce.com/en/users/00550000006yDdKAAU/trailmixes/architect-integration-architecture)
  - [Exam Guide](https://trailhead.salesforce.com/help?article=Salesforce-Certified-Integration-Architecture-Designer-Exam-Guide)

### Community Recommended Content

- [Integration Patterns Overview](https://developer.salesforce.com/docs/atlas.en-us.integration_patterns_and_practices.meta/integration_patterns_and_practices/integ_pat_intro_overview.htm)
- [Data Integration](https://architect.salesforce.com/design/decision-guides/data-integration)
- [Best Practices for Deployments with Large Data Volumes](https://developer.salesforce.com/docs/atlas.en-us.salesforce_large_data_volumes_bp.meta/salesforce_large_data_volumes_bp/ldv_deployments_introduction.htm)

### Trailmix

[**Measure Performance for Your Salesforce Org**](https://help.salesforce.com/articleView?id=sf.technical_requirements_measuring_ept.htm&type=5)

- Make a sandbox, ideally a full copy, and have it be as close to production's metadata (and data-based config) as possible
  - Draw a system diagram to visualize current and future state
  - Estimate size and shape of data
  - Sandboxes and production orgs may use different instances and hardware, and thus may have different performance 
- Add `eptVisible` as parameter to app to measure Experienced Page Time (EPT)
  - Lightning Component Debug Mode is not as reliable, may negatively impact performance
  - Lightning Usage App (Activity or Usage tabs) displays data
  - Create a custom report type to show Lightning Usage App objects
    - `LightningUsageByAppTypeMetrics`
    - `LightningUsageByBrowserMetrics`
    - `LightningUsageByPageMetrics`
    - `LightningUsageByFlexiPageMetrics`
  - Also available with Event Monitoring Analytics App (prebuilt)
- Also, leverage browser developer tools, Selenium, LoadRunner, or JMeter

[**Congratulations! You Inherited a Mature Org...Now What?**](https://www.salesforce.com/video/1770820/)

[**Analyzing Your Org with Salesforce Optimizer**](https://admin.salesforce.com/blog/2017/analyzing-org-salesforce-optimizer-webinar-recap)

- Salesforce Optimizer is available in Setup, analyzes customizations, creates a PDF report, assigns resources to learn more for each item
- Helpful for
  - Proactive maintenance
  - Cleanup
  - Improving user experience
  - Moving to Lightning Experience

[**Salesforce to Salesforce**](https://help.salesforce.com/articleView?id=sf.business_network_intro.htm&type=5)

- Last Modified By is updated to Connection User if the other org updates your data
- Assign permission set to control which users can manage connections and view/accept data from other orgs
- Connection Finder assists with identifying who uses Salesforce (as a survey)
  - Responses are logged on the Account and Contact records
- Connection Templates define objects/fields to share with Connections (other orgs)
- Objects supported for publishing
  - Account
  - Attachment (unencrypted)
  - Case
  - Case Comment
  - Contact
  - Lead
  - Opportunity
  - Opportunity Product
  - Product
  - Task
  - Any custom objects
- Subscription is the recipient side of a published object and its fields
  - Map fields to whichever you'd like
  - Auto-accept will run assignment rules for Lead and Case when creating data in subscriber's org
  - Workflow rules will fire when accepting a parent record, child record is inserted, or a subscribed field triggers the workflow rule
- Forward a record via External Sharing related list, but don't share it back to the org that shared with you
  - Accept a forwarded record from the list view (if auto-accept is not enabled)
  - Records that are no longer shared are not deleted from subscribers, but those orgs stop receiving updates
  - At most 100 tasks can be shared

[**Explore Integration Patterns and Practices**](https://trailhead.salesforce.com/en/content/learn/trails/explore-integration-patterns-and-practices?trailmix_creator_id=strailhead&trailmix_slug=architect-integration-architecture)

- Integration initiatives
  - Application integration: extends features and functionality across systems => UI, API integrations, flows, connectors
  - Data integration: data movement and sync, involves integrity, governance, flow design, migration
  - Process integration: business processes that extend across systems
- Integration patterns
  - Remote process, request and reply: invoke a process on another system, await reply
  - Remote process, fire and forget: invoke a process on another system, and don't wait for it to finish
  - Batch data sync: data in one system is synced with another in batch (i.e. not real time) 
  - Remote call in: another system makes a request to your system
  - Data virtualization: access external data from within Salesforce (e.g. Salesforce Connect)
  - High frequency data replication: data is replicated to another system in near real time
  - Pub/sub: publish something to a channel, subscribers do (nothing) with it
- Four dimensions for integrations
  - Layers: tasks in a system
  - Volume: amount of data sync and transformation activity
  - Timing: sync or async
  - Direction: one way or bidirectional
- Three layers for integration
  - User interface: Canvas, mashups (e.g. Visualforce page), Lightning out
  - Business process/logic: Mulesoft, platform events, Streaming API, flows, outbound messages
  - Data: Heroku Connect, Salesforce Connect, Apex, APIs (REST, SOAP, Bulk, Composite, Apex REST)
- Patterns mapped to layers
  - Remote process, request and reply: business process/logic
  - Remote process, fire and forget: business process/logic
  - Data virutalization: data
  - Remote call in: business process/logic
  - Batch data sync: data
  - High frequency data replication: UI, data
  - Pub/sub: business process/logic, data
- Patterns mapped to timing
  - Remote process, request and reply: sync
  - Remote process, fire and forget: async
  - Data virutalization: sync
  - Remote call in: sync, async
  - Batch data sync: async
  - High frequency data replication: sync, async
  - Pub/sub: async
- Idempotent: same result when applied to itself (e.g. double clicking a button fires it twice)
  - Apply unique message ID to request
  - Check for duplicates before processing results
- If these don't exist, it impacts to scalability
  - Bulkification
  - Governance
  - Locking errors
  - Heavy post processing with Apex
- Decisions about integration type
  - Source and target
  - Type
  - Data volume
  - Timing
- Anti-patterns
  - Not testing in a sandbox
  - Using SOAP API for over 500K records
  - Running batch Apex in parallel with data migration
  - Expecting async operations to always fit in a window (both data loads and on platform ops)
  - No performance assessment on UI 
  - Mimic org structure as role hierarchy
- Connectors
  - Mulesoft Database
  - Mulesoft HTTP
  - Heroku Connect: uses SOAP, Bulk, Streaming APIs
  - Salesforce Connect: OData 2.0 or 4.0 REST APIs, cross org, custom Apex adapters
    - Limited to 20K callouts per hour
- Mulesoft's API layers
  - System: connects directly to a system / database
  - Process: reads from system layer, where business logic and process exists
  - Experience: users interact with data from this layer 

[**Integration Architecture for the Salesforce Platform**](https://developer.salesforce.com/blogs/developer-relations/2014/11/salesforce-integration-architecture.html)

- Mix of batch and real time
- Decide what the SLAs are for business stakeholders, design accordingly
- There's still a mix of clouds and ground (on premise)

[**Governance Basics**](https://trailhead.salesforce.com/content/learn/modules/governance-basics?trailmix_creator_id=strailhead&trailmix_slug=architect-integration-architecture)

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

[**Key Principles for a Successful Salesforce Implementation Part III: Governance**](https://medium.com/salesforce-architects/key-principles-for-a-successful-salesforce-implementation-part-iii-governance-b2a165f431c3)

- Checkponts for: solution design, solution approval, architectural reviews, change management
- Principles: assign an owner, version, status, review date, retirement date

[**Certificates and Keys**](https://help.salesforce.com/articleView?id=security_keys_about.htm&type=0)

- Verifies a request is originating from an org, required if that external service needs verification
- Self signed certificate from Salesforce: less legit, but works
- Certified signed by a CA: more legit
- Mutual auth certificate: used to prevent spoofing / impersonation
- Master encryption key: used for encrypted fields, can be managed by the org

[**Configure Remote Site Settings**](https://help.salesforce.com/articleView?id=configuring_remoteproxy.htm&type=0)

- Required before a Visualforce page, Apex callout, or JS can make a request, need a remote site
  - Acceptable outbound ports: 80, 443, 1024 through 65535
  - Allows both HTTP and HTTPS (although come on y'all... HTTPS is the only way)

[**Build Integrations Using Connected Apps**](https://trailhead.salesforce.com/en/content/learn/trails/build-integrations-using-connected-apps?trailmix_creator_id=strailhead&trailmix_slug=architect-integration-architecture)

- Use cases
  - Access Salesforce data via API integrations
  - Integrate service provider with org with SAML
  - Provide authorization for external gateways by creating a connected app for a third party client app
  - Manage access for a third party app for users
- OAuth flows
  - Web Server
    - Connected app directs user to Salesforce for auth and to authorize data ccess
    - Salesforce sends auth code to app
    - App sends auth code to Salesforce requesting token
    - Salesforce validates code, sends back token
    - App asks for data with access token
    - Salesforce validates its allowed and passes data
  - User Agent
    - Connected app directs user to Salesforce
    - Salesforce sends redirect URL with access and refresh tokens
    - App uses 
  - JWT Bearer
    - Connected app sends JWT
    - Salesforce validates JWT with signature and params
    - Salesforce issues access token
    - App asks for data with access token
  - Device
    - Connected app sends request to Salesforce
    - Salesforce returns a code (e.g. 4-8 characters), verification URL (e.g. https://salesforce.com/activate), device code
    - App starts polling Salesforce token endpoint to listen for auth
    - User provides code at verification URL
    - Salesforce sends access and refresh token to app
    - App can do things
  - Refresh Token
    - Web Server and User Agent flows: refresh token allows for accessing new access token
  - Username Password
    - Requires high level of trust with this flow
    - Returns access token, scopes are not supported
  - SAML Bearer
    - App uses SAML assertion to get access token
  - SAML Assertion
    - Allows access to web services via SAML assertion
- SSO
  - Identity provider: enables users to access other systems without a separate login event
  - Service provider: accepts identity from an identity provider to provide a service
- Options for using Salesforce as identity provider
  - SAML: create a connected app that uses SAML for auth
  - OpenID: create a connected app that uses OAuth for auth with the `openid` scope, as OpenID adds an authentication layer on top of OAuth 2.0
- IP restrictions on the user's profile can be:
  - Enforced
  - Enforced, relaxed for refresh tokens
  - Relaxed overall

[**Secure Secrets Storage**](https://trailhead.salesforce.com/content/learn/modules/secure-secrets-storage?trailmix_creator_id=strailhead&trailmix_slug=architect-integration-architecture)

- Storage for application secrets
  - Named Credentials
  - Custom Settings
  - Custom Metadata Types
- Protected means not available to subscriber orgs, only via logging in as managed package publisher
- Custom Settings vs Metadata Types
  - Setting: secret must be updated frequenty and available immediately (e.g. not in a subsequent release)
  - Metadata Type: deployable, easily migratable
- `Crypto` class
  - Encrypts and decrypts per AES 128, 192, 256 bit algos
  - Hash digests using MD5, SHA1, SHA256, SHA512
  - Hash-based message authentication codes for authenticity and integrity
  - Digital signatures

[**Change Data Capture Basics**](https://trailhead.salesforce.com/content/learn/modules/change-data-capture?trailmix_creator_id=strailhead&trailmix_slug=architect-integration-architecture)

- CDC is streaming product to sync changes in real time with other systems
- Essentially publishes to a Salesforce event bus for subscribers to handle
- Events published are stored for up to 3 days
- Components of an event
  - entityName: Salesforce object name
  - changeType: CREATE, UPDATE, DELETE, UNDELETE
  - changedFields: specific fields that were changed plus `LastModifiedDate`
  - changeOrigin: describes where the change event occurred based on an app's `clientID`
  - transactionKey: unique identifier for transaction
  - sequenceNumber: identifies when it was fired if multiple events occur per transaction 
  - `event.replayId`: allows for replaying events from that ID forward (for up to 3 days)
- Subscribe to standard or custom channels
  - Standard: `/data/ChangeEvents` for all, `/data/{{Object Name}}ChangeEvent` for single object
  - Custom: `/data/{{Channel Name}}__chn`
- Respects field level security based on authenticated user
- Also can subscribe to change events via Apex triggers

[**Lightning Platform API Basics**](https://trailhead.salesforce.com/content/learn/modules/api_basics?trailmix_creator_id=strailhead&trailmix_slug=architect-integration-architecture)

- Various APIs
  - REST API: RESTful with HTTP methods, supports XML and JSON
  - SOAP API: WSDL file to define parameters, supports XML
  - Bulk API: lots of records, Bulk API 2.0 is better because it loses conceopt of batches
  - Streaming API: pub/sub model where events are published via streaming topics
- Authentication
  - All require authentication except SOAP API's `login()`
  - Other auth mechanisms are supplying a Session ID or using OAuth
- When to use:
  - REST API: simple integrations for CRUD ops
  - SOAP API: when the calling platform needs a web service
  - Connect REST API: Chatter apps, B2B Commerce for Lightning, CMS content, Experience Cloud sites
  - User Interface API: create and reference records, list views, actions, etc
  - Analytics REST API: build things in Einstein Analytics (lenses, dashboards)
  - Bulk API: tons of data
  - Metadata API: CRUD ops for customizations
  - Streaming API: pub/sub 
  - Apex REST API: exposes an Apex class as RESTful resource
  - Apex SOAP API: exposes an Apex class as web service
  - Tooling API: building custom dev tools for Salesforce
- SOAP API WSDLs
  - Enterprise: strongly typed, specific to single org
  - Partner: loosely typed, generic for many orgs

[**Integration Patterns and best practices**](https://developer.salesforce.com/docs/atlas.en-us.integration_patterns_and_practices.meta/integration_patterns_and_practices/integ_pat_intro_overview.htm)

- Integrating Salesforce with Another System
  - Process integration
    - Sync: Request and Reply
    - Async: Fire and Forget
  - Data integration
    - Sync: Request and Reply
    - Async: UP update based on data changes
  - Virtual 
    - Data virtualization
- Integrating Another System with Salesforce
  - Remote call in, except async data intgration, then use batch data sync
- Remote Process Invocation, Request and Reply
  - Best
    - Enhanced External Services invokes a REST API call
    - Lightning component or page initiates a synchronous Apex SOAP or REST callout
    - A custom Visualforce page or button initiates a synchronous Apex SOAP callout
    - A custom Visualforce page or button initiates a synchronous Apex HTTP callout	
  - Suboptimal
    - A synchronous trigger that’s invoked from Salesforce data changes performs an asynchronous Apex SOAP or HTTP callout
    - A batch Apex job performs a synchronous Apex SOAP or HTTP callout
- Remote Process Invocation, Fire and Forget
  - Best
    - Process-driven platform events
  - Good
    - Customization-driven platform events
    - Workflow-driven outbound messaging
    - Outbound messaging and callbacks
  - Suboptimal
    - Custom Lightning component or Visualforce page that initiates an Apex SOAP or HTTP asynchronous callout	
    - Trigger that’s invoked from Salesforce data changes performs an Apex SOAP or HTTP asynchronous callout	
    - Batch Apex job that performs an Apex SOAP or HTTP asynchronous callout
- Batch Data Sync
  - Best
    - Salesforce Change Data Capture
    - Replication via third-party ETL tool (remote system as data master)
  - Good
    - Replication via third-party ETL tool (Salesforce as data master)
  - Suboptimal
    - Remote call-in
    - Remote process invocation
- Remote Call In
  - Best
    - SOAP API	
    - REST API 
  - Best for bulk
    - Bulk API 2.0
  - Suboptimal
    - Apex web services
    - Apex REST services
- UI Update Based on Data Changes
  - Use the Streaming API
- Data Virtualization
  - Best
    - Salesforce Connect	
  - Suboptimal
    - Request and Reply


[**Application Integration Patterns for Salesforce Lightning Platform**](https://trailhead.salesforce.com/content/learn/modules/app-integration-patterns?trailmix_creator_id=strailhead&trailmix_slug=architect-integration-architecture)

Note that most of this is duplicated from a section above.

- Integration initiatives
  - Application integration: extends features and functionality across systems => UI, API integrations, flows, connectors
  - Data integration: data movement and sync, involves integrity, governance, flow design, migration
  - Process integration: business processes that extend across systems
- Patterns mapped to layers
  - Remote process, request and reply: business process/logic
  - Remote process, fire and forget: business process/logic
  - Data virutalization: data
  - Remote call in: business process/logic
  - Batch data sync: data
  - High frequency data replication: UI, data
  - Pub/sub: business process/logic, data
- Patterns mapped to timing
  - Remote process, request and reply: sync
  - Remote process, fire and forget: async
  - Data virutalization: sync
  - Remote call in: sync, async
  - Batch data sync: async
  - High frequency data replication: sync, async
  - Pub/sub: async

[**Outbound Messaging**](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_om_outboundmessaging.htm)

- Sends an XML payload via `notifications()` call to an HTTP or HTTPS endpoint
- Invoked via workflow rules
- Messages sit in queue until sent successfully or 24 hours old, at which time dropped from queue
- Unsuccessful delivery increases time between retries to max of 2 hours
- Messages can be delivered out of order
- Session ID can be sent, allows API requests by receiving system back to Salesforce

[**Canvas Developer Guide**](https://developer.salesforce.com/docs/atlas.en-us.platform_connect.meta/platform_connect/canvas_framework_intro.htm#!)

- Canvas: set of tools and JavaScript APIs to embed an new/existing app hosted elsewhere within Salesforce
  - Auth: either signed request or OAuth
  - Context: provides details about where the canvas app is running
  - Cross domain XHR: JS support for XML HTTP requests to Salesforce 
  - Resizing: changes the size of canvas app
  - Events: JS to send/receive events from canvas app
  - Canvas in Visualforce: exposes canvas app 
  - Canvas in Publisher: exposes canvas app as an action
  - Canvas in Chatter: exposes as feed item
  - Canvas in Mobile: exposes in Salesforce mobile app

[**Quick Start: Salesforce Connect**](https://trailhead.salesforce.com/content/learn/projects/quickstart-lightning-connect?trailmix_creator_id=strailhead&trailmix_slug=architect-integration-architecture)

- Indirect Lookup: relates to an object by External ID
- External Lookup: relates to an external object by External ID

[**External Services**](https://trailhead.salesforce.com/content/learn/modules/external-services?trailmix_creator_id=strailhead&trailmix_slug=architect-integration-architecture)

- External Services: OpenAPI compliant spec that is effectively REST APIs

[**API Planning Framework for Architects**](https://trailhead.salesforce.com/content/learn/modules/design-with-the-right-api?trailmix_creator_id=strailhead&trailmix_slug=architect-integration-architecture)

- Salesforce APIs
  - REST API: REST; JSON + XML; Sync
  - SOAP API: SOAP; XML; Sync
  - Chatter REST API: REST; JSON + XML; Sync (photos async)
  - UI API: REST; JSON; Sync
  - Analytics REST API: REST; JSON + XML, Sync
  - Bulk API: REST; CSV + JSON + XML; Async
  - Metadata API: SOAP; XML; Async
  - Streaming API: Bayeux; JSON; Async
  - Apex REST API: REST; JSON + XML + custom (whatever you want); Sync
  - Apex SOAP API: SOAP; XML; Sync
  - Tooling API: REST + SOAP; JSON + XML + custom; Sync

[**API-Led Integration for Business Reinvention**](https://trailhead.salesforce.com/content/learn/modules/api-led-integration-for-business-reinvention?trailmix_creator_id=strailhead&trailmix_slug=architect-integration-architecture)

[**Platform Events Basics**](https://trailhead.salesforce.com/content/learn/modules/platform_events_basics?trailmix_creator_id=strailhead&trailmix_slug=architect-integration-architecture)

- Use Cases
  - Salesforce to External: publish an event, system subscribes and handles
  - External to Salesforce: publish an event, platform event trigger subscribes and handles 
  - Within Salesforce: trigger publishes event, platform event trigger subscribes and handles 
- Generic (`PushTopic`) vs Platform Events
  - Generic events have user defined payloads, published via multiple APIs, can be subscribed to via CometD (Streaming API)
  - Platform events: define event schema as typed fields, publish via Apex, subscribe via Apex triggers, publish via Process Builder and Flow
- Behavior
  - Publish After Commit: can be rolled back
  - Publish Immediately: cannot be rolled back, occurs when call is made
- Publishing
  - Apex: `EventBus.publish()`
  - Post to REST API: `/services/data/{{api version}}/sobjects/{{event name}}`

[**Access External Data With Salesforce Connect**](https://help.salesforce.com/articleView?id=sf.salesforce_connect.htm&type=5)

- Salesforce Connect Limits
  - External Objects: 200 per org
  - Rows retrieved by SOSL and Salesforce per hour: 100K
  - Rows retrieved or created per hour: 100K
  - Page size for server driven paging: 2K
- Identity options, always uses external source definition for metadata
  - Named Principal
  - Per User
- Salesforce assigns record IDs with external object records on first retrieval, remains until object is deleted
- Salesforce can write to external objects (e.g. via OData 4.0) 
- Platform native features
  - Reports
  - Chatter feed
  - Quick actions
  - Flows and process builder
  - Salesforce mobile
  - Classic console apps
  - SOQL, SOSL, Metadata API, change sets, and more!
- Adapters
  - Cross Org: access data from other Salesforce orgs
  - OData 2.0 or 4.0
  - Apex custom adapters: roll your own (burrito, or sadly, adapter)

[**Large Data Volumes**](https://trailhead.salesforce.com/content/learn/modules/large-data-volumes?trailmix_creator_id=strailhead&trailmix_slug=architect-integration-architecture)

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

[**Understanding Outbound Messaging**](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_om_outboundmessaging_understanding.htm)

1. Workflow sends message
1. SOAP sends to web service endpoint
1. Web service acknowledges receipt
  1. Web service may leverage endpoint and Session ID to update data via SOAP API

[**Play with Outbound Messaging**](http://intg-playground.herokuapp.com/sfdc/omlistener)

[**Apex Integration Services**](https://trailhead.salesforce.com/content/learn/modules/apex_integration_services?trailmix_creator_id=strailhead&trailmix_slug=architect-integration-architecture)

- REST
  - `Http` object to `send()` and `HttpRequest` with return value as `HttpResponse`
  - Implement `HttpCalloutMock` for test coverage, use `Test.setMock()` to assign 
- SOAP
  - Generate via WSDL2Apex
  - Implement `WebServiceMock` for test coverage, use `Test.setMock()` to assign
- Expose Apex as custom REST API
  - Use `@RestResource` annotation on class, must be `global`
  - Use annotations for `global static` methods that match HTTP methods
    - `@HttpGet`, `@HttpPost`, `@HttpDelete`, `@HttpPut`, `@HttpPatch`

[**Develop a Heroku App That Integrates with Salesforce**](https://trailhead.salesforce.com/content/learn/projects/develop-heroku-applications?trailmix_creator_id=strailhead&trailmix_slug=architect-integration-architecture)

[**Salesforce & Heroku Integration**](https://trailhead.salesforce.com/content/learn/modules/salesforce_heroku_integration?trailmix_creator_id=strailhead&trailmix_slug=architect-integration-architecture)

- Heroku Connect: either Salesforce to Heroku, or bidirectional with low latency (read: not near real time, but close)
- Why use Heroku?
  - Data replication
  - Data proxies
  - Custom UIs
  - External processes 

[**Build a Connected App for API Integration**](https://trailhead.salesforce.com/content/learn/projects/build-a-connected-app-for-api-integration?trailmix_creator_id=strailhead&trailmix_slug=architect-integration-architecture)

[**Quick Start: MuleSoft API Designer**](https://trailhead.salesforce.com/content/learn/projects/quickstart-mulesoft-design?trailmix_creator_id=strailhead&trailmix_slug=architect-integration-architecture)

- API specs are built with RAML (basically modified YAML)
- Publish to the exchange so your colleagues can leverage it

[**API Lifecycle Management with Anypoint Platform**](https://trailhead.salesforce.com/content/learn/modules/mulesoft-basics?trailmix_creator_id=strailhead&trailmix_slug=architect-integration-architecture)

- Anypoint Platform
  - Design: Design Center
  - Manage: Management Center
  - Engage: Exchange
  - Run: mules
  - Scale: runtime services

[**Event Monitoring**](https://trailhead.salesforce.com/content/learn/modules/event_monitoring?trailmix_creator_id=strailhead&trailmix_slug=architect-integration-architecture)

- EventLogFile records are accessible via
  - Dev Console
  - Salesforce's Event Log File Browser
  - cURL
  - Python

[**Data Integration Specialist**](https://trailhead.salesforce.com/content/learn/superbadges/superbadge_integration?trailmix_creator_id=strailhead&trailmix_slug=architect-integration-architecture)