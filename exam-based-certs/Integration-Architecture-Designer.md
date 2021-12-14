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

TODO

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

- 

[**Integration Architecture for the Salesforce Platform**](https://developer.salesforce.com/blogs/developer-relations/2014/11/salesforce-integration-architecture.html)



[**Governance Basics**](https://trailhead.salesforce.com/content/learn/modules/governance-basics?trailmix_creator_id=strailhead&trailmix_slug=architect-integration-architecture)



[**Key Principles for a Successful Salesforce Implementation Part III: Governance**](https://medium.com/salesforce-architects/key-principles-for-a-successful-salesforce-implementation-part-iii-governance-b2a165f431c3)



[**Certificates and Keys**](https://help.salesforce.com/articleView?id=security_keys_about.htm&type=0)



[**Configure Remote Site Settings**](https://help.salesforce.com/articleView?id=configuring_remoteproxy.htm&type=0)



[**Build Integrations Using Connected Apps**](https://trailhead.salesforce.com/en/content/learn/trails/build-integrations-using-connected-apps?trailmix_creator_id=strailhead&trailmix_slug=architect-integration-architecture)



[**Secure Secrets Storage**](https://trailhead.salesforce.com/content/learn/modules/secure-secrets-storage?trailmix_creator_id=strailhead&trailmix_slug=architect-integration-architecture)



[**Change Data Capture Basics**](https://trailhead.salesforce.com/content/learn/modules/change-data-capture?trailmix_creator_id=strailhead&trailmix_slug=architect-integration-architecture)



[**Lightning Platform API Basics**](https://trailhead.salesforce.com/content/learn/modules/api_basics?trailmix_creator_id=strailhead&trailmix_slug=architect-integration-architecture)



[**Integration Patterns and best practices**](https://developer.salesforce.com/docs/atlas.en-us.integration_patterns_and_practices.meta/integration_patterns_and_practices/integ_pat_intro_overview.htm)



[**Application Integration Patterns for Salesforce Lightning Platform**](https://trailhead.salesforce.com/content/learn/modules/app-integration-patterns?trailmix_creator_id=strailhead&trailmix_slug=architect-integration-architecture)



[**Outbound Messaging**](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_om_outboundmessaging.htm)



[**Canvas Developer Guide**](https://developer.salesforce.com/docs/atlas.en-us.platform_connect.meta/platform_connect/canvas_framework_intro.htm#!)



[**Quick Start: Salesforce Connect**](https://trailhead.salesforce.com/content/learn/projects/quickstart-lightning-connect?trailmix_creator_id=strailhead&trailmix_slug=architect-integration-architecture)



[**External Services**](https://trailhead.salesforce.com/content/learn/modules/external-services?trailmix_creator_id=strailhead&trailmix_slug=architect-integration-architecture)



[**API Planning Framework for Architects**](https://trailhead.salesforce.com/content/learn/modules/design-with-the-right-api?trailmix_creator_id=strailhead&trailmix_slug=architect-integration-architecture)



[**API-Led Integration for Business Reinvention**](https://trailhead.salesforce.com/content/learn/modules/api-led-integration-for-business-reinvention?trailmix_creator_id=strailhead&trailmix_slug=architect-integration-architecture)



[**Platform Events Basics**](https://trailhead.salesforce.com/content/learn/modules/platform_events_basics?trailmix_creator_id=strailhead&trailmix_slug=architect-integration-architecture)



[**Access External Data With Salesforce Connect**](https://help.salesforce.com/articleView?id=sf.salesforce_connect.htm&type=5)



[**Large Data Volumes**](https://trailhead.salesforce.com/content/learn/modules/large-data-volumes?trailmix_creator_id=strailhead&trailmix_slug=architect-integration-architecture)



[**Understanding Outbound Messaging**](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_om_outboundmessaging_understanding.htm)



[**Play with Outbound Messaging**](http://intg-playground.herokuapp.com/sfdc/omlistener)



[**Apex Integration Services**](https://trailhead.salesforce.com/content/learn/modules/apex_integration_services?trailmix_creator_id=strailhead&trailmix_slug=architect-integration-architecture)



[**Develop a Heroku App That Integrates with Salesforce**](https://trailhead.salesforce.com/content/learn/projects/develop-heroku-applications?trailmix_creator_id=strailhead&trailmix_slug=architect-integration-architecture)



[**Salesforce & Heroku Integration**](https://trailhead.salesforce.com/content/learn/modules/salesforce_heroku_integration?trailmix_creator_id=strailhead&trailmix_slug=architect-integration-architecture)



[**Build a Connected App for API Integration**](https://trailhead.salesforce.com/content/learn/projects/build-a-connected-app-for-api-integration?trailmix_creator_id=strailhead&trailmix_slug=architect-integration-architecture)



[**Quick Start: MuleSoft API Designer**](https://trailhead.salesforce.com/content/learn/projects/quickstart-mulesoft-design?trailmix_creator_id=strailhead&trailmix_slug=architect-integration-architecture)



[**API Lifecycle Management with Anypoint Platform**](https://trailhead.salesforce.com/content/learn/modules/mulesoft-basics?trailmix_creator_id=strailhead&trailmix_slug=architect-integration-architecture)



[**Event Monitoring**](https://trailhead.salesforce.com/content/learn/modules/event_monitoring?trailmix_creator_id=strailhead&trailmix_slug=architect-integration-architecture)



[**Data Integration Specialist**](https://trailhead.salesforce.com/content/learn/superbadges/superbadge_integration?trailmix_creator_id=strailhead&trailmix_slug=architect-integration-architecture)