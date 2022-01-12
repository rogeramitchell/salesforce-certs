## Resources

### Salesforce Content

- [Trailhead Overview](https://trailhead.salesforce.com/credentials/identityandaccessmanagementdesigner)
  - [Trailmix](https://trailhead.salesforce.com/en/users/00550000006yDdKAAU/trailmixes/architect-identity-and-access-management)
  - [Exam Guide](https://trailhead.salesforce.com/help?article=Salesforce-Certified-Identity-and-Access-Management-Designer-Exam-Guide)

### Trailmix

[**Identity Basics**](https://trailhead.salesforce.com/content/learn/modules/identity_basics?trailmix_creator_id=strailhead&trailmix_slug=architect-identity-and-access-management)

- Salesforce Identity handles the following
  - Single sign-on: allows log via existing authenticated session
  - Connected apps: authorized resources to which users have access
  - Social sign-on: using social networks to log into an org
  - Multi-factor authentication: additional layer of auth via tokens from a text message, email, app
  - My Domain: unique to users to assist with security
  - Centralized user account management: manage user accounts in once place (as attributes can be sent with auth requests)
  - User provisioning: creates users in other orgs and services 
  - Identity Connect: sync users and attributes from Active Directory (AD) to Salesforce
  - App Launcher: presents connected apps for easily accessing other services (i.e. think tiles available in Okta)
- Helps employees
  - Convenience
  - Control
  - Security
- Helps customers and partners
  - User registration
  - Brand control
  - Social sign on, use existing accounts or phone/email (for OTP flows) 
  - Seamless web experience
  - One comprehensive view of user
- SAML
  - XML-based protocol that contains attributes in the SAML request
- OAuth 2.0
  - Open protocol for secure data sharing between apps or services
  - Prompts user to allow specific set of scopes
- OpenID Connect
  - Authentication layer built on OAuth 2.0 to share user information
- Salesforce as service provider: external identity management solution passes authenticated users to Salesforce
- Salesforce as identify provider: authenticated users in Salesforce easily access other apps and services 
- SAML flow
  - User tries to access Salesforce
  - Salesforce recognizes SSO request and generates SAML request
  - Salesforce sends SAML request to browser
  - Browser redirects SAML request to external identity provider
  - Identify provider verifies user's identity and sends a SAML assert with user auth
  - Identity provider sends SAML assertion to browser
  - Browser redirects SAML assertion to Salesforce
  - Salesforce verifies the assertion
  - User can access Salesforce
- Terms
  - Authentication: who a person is
  - Authorization: what a person can do
  - Protocol: set of rules that enable systems to share data
  - Standard: a spec or set of industry practices that orgs agree to follow
  - Username/password, credentials: how a person logs into a system
  - Single sign on: enables one login event that enables multiple apps with logging in again
  - Social sign on: logging into an app with social media service
  - Identity provider: trusted service that enables users to access apps and services without logging in again
  - Service provider: hosts an app and accepts identity from an identity provider

[**Identity and Access Management for Beginners**](https://www.youtube.com/watch?v=fcSXiUsU5lE)

TODO

[**User Authentication**](https://trailhead.salesforce.com/content/learn/modules/identity_login?trailmix_creator_id=strailhead&trailmix_slug=architect-identity-and-access-management)

- Multi factor auth combines something you know and have
  - Know: username and password
  - Have: mobile device, access to receive emails or texts to a predefined address; also can be a time based one-time password (TOTP) or physical security key
- Identity Verification in Setup
  - Allow location based automated verifications with Salesforce Authenticator, can enforce trusted IP ranges
- My Domain has policies to 
  - Prevent logging in from **login.salesforce.com**
  - Redirecting to same page within domain, displaying warning, or not redirecting (if a person referenes an instance/pod instead of my domain)
  - Customize login page type, auth methods, right side page, logo, and color
- When setting up SSO with an external identity provider
  - Set a Federation ID for each user
  - Set up issuer and entity ID for the IdP in Salesforce
  - Use the login URL that Salesforce providers to specify the recipient URL, entity ID (my domain URL typically)

[**OAuth with Salesforce Demystified**](https://www.youtube.com/watch?v=zpToAGuhg60)

TODO

[**Salesforce Licensing**](https://trailhead.salesforce.com/content/learn/modules/salesforce-licensing?trailmix_creator_id=strailhead&trailmix_slug=architect-identity-and-access-management)

- Each org has at least one edition, which provides functionality to activate an org, but those editions must be the same level (e.g. Sales Cloud Unlimited and Service Cloud Unlimited)
  - Edition has a mix of platform licenses and user licenses
- Add ons have a mix of user licenses and permission set licenses
- Settings are controlled via permissions and preferences
- Components of how access to features are controlled
  - Platform level permissions: specify what is possible for org
  - Platform level preferences: specify what preferences are available for an org
  - User level perms: specify what is possible for that user
  - User level preferences: specify what that user prefers 
- Profile and permission set combine platform level permissions and preferences, are assigend to users to provide user level perms and prefs
- Can sync production org license changes to existing sandboxes from production via Match Production Licenses to Sandbox

[**How to Provision Salesforce Communities Users**](https://developer.salesforce.com/blogs/developer-relations/2014/06/how-to-provision-salesforce-communities-users.html)

- Contacts need to exist before a Community / Experience Cloud external user is created
- Contacts linked to a 
  - Person account can only be customers
  - Non-partner business account can only be customers (until account is enabled as partner)
  - Partner account can be either customers or partners
- External users can be created via
  - Salesforce license with Manage External Users, allows for creating users on Accounts to which the user has read access
  - Partner Community, Partner Portal with Delegated External User Administrator on that external user's Account
  - Customer Portal Manager, Customer Communities Plus with Delegated External User Administrator on that external user's Account
- Partner users are role based, defined at account level, can have between 1-3 roles (defined for entire org on Experience Settings)
- Users can either be provisioned:
  - Manually
  - Self register
  - Created via SOAP or REST API
  - Data Loader
  - Social sign on
  - SAML JIT (just in time)
    - Requires `Account.Name`, `Account.AccountNumber`, `Account.Owner` (as 15 or 18 character ID), `Contact.LastName`, `Contact.Email`, `User.LastName`, `User.Email`, `User.Username`, `User.ProfileID`, `User.PortalRole`
    - Attempts to match a user by Federation ID, then find a contact with matching email, then find an account by either name or account number fields; email has to be unique and the account owner must have a role

[**Single Sign-On Implementation Guide**](https://developer.salesforce.com/docs/atlas.en-us.230.0.sso.meta/sso/sso_about.htm)

TODO

[**Deploying Single Sign-On and Identity for Employees, Customers, and Partners**](https://www.youtube.com/watch?v=swguz0ZKggM)

TODO

[**Auditing**](https://help.salesforce.com/articleView?id=sf.security_overview_auditing.htm&type=5)

- Record Modification Fields
  - Created By
  - Last Modified by
- Login History
  - 6 months of successful and failed login history per user
- Field History Tracking
  - Tracks changes for up to 20 fields per object, some fields do not support old and new values
- Setup Audit Trail
  - Tracks modifications to the org (metadata)

[**Shield Platform Encryption**](https://trailhead.salesforce.com/content/learn/modules/spe_admins?trailmix_creator_id=strailhead&trailmix_slug=architect-identity-and-access-management)

- Encrypt only where necessary
- Backup and archive keys and data
- Encryption applies to all users

[**Secure Your Apps with Salesforce Shield**](https://trailhead.salesforce.com/en/content/learn/trails/shield?trailmix_creator_id=strailhead&trailmix_slug=architect-identity-and-access-management)

- Event Monitoring
  - EventLogFile records are accessible via
    - Dev Console
    - Salesforce's Event Log File Browser
    - cURL
    - Python
- Event Monitoring Analytics App
  - Event Monitoring offers app with prebuilt dashboards
  - Identifies suspicious behavior, slow page perf, poor user adoption
  - Event Monitoring comes with 10 Event Monitoring Analytics app licenses
  - Enable from Setup => Event Monitoring Settings => View Event Log Data in Analytics Apps
    - Assign Event Monitoring Analytics Admin to users that customize the apps and data flows
    - Assign Event Monitoring Analytics User to viewers
  - Allows for storing 1 to 30 days of data
  - Leverage metrics like `CPU_TIME`, `DB_TOTAL_TIME`, `NUMBER_COLUMNS` to track report performance
  - Set notifications when aggregate values exceed thresholds
  - Can sync event monitoring datasets with other datasets for more meaningful reporting (e.g. Account datasets)
- Real-Time Event Monitoring
  - Requires Salesforce Shield or Salesforce Event Monitoring add-ons
  - Can be used with Transaction Security to block actions and notify in real time
  - Key Terms
    - Event: anything that happens, like user clicks, record state changes, etc
    - Event Monitoring: stores events in log files
    - Event log file: standard object `EvetLogFile`, can be downloaded after 24 hours or hourly, stores up to 30 days of data
    - Real-Time Event Monitoring: events in near real time, can be stored in Big Objects for auditing and reporting
    - Real-Time Events: platform events that are streamed and stored in Big Objects, can be queried via SOQL or Async SOQL
    - Standard Platform Events: RTEM uses standard platform events to which subscriptions can be established
    - RTEM Objects: has ability to stream and store data, and enforce policies on that data
    - Big Objects: store way more data this way than with event log files
  - Different Event Types
    - ApiAnonmalyEvent => stored => available in TSP
    - BulkApiRequestEvent => stored => available in TSP
    - ConcorLongRunApexErrEvent => not stored => not available for TSP
    - CredentialStuffingEvent => stored => available in TSP
    - IdentityVerificationEvent => stored => not available for TSP
    - ListViewEventStream => stored => available in TSP
    - LoginAsEventStream => stored => not available for TSP
    - LoginEventStream => stored => available in TSP
    - LogoutEventStream => stored => not available for TSP
    - ReportAnomalyEvent => stored => available in TSP
    - ReportEventStream => stored => available in TSP
    - SessionHijackingEvent => stored => available in TSP
  - View Real-Time Event Monitoring Data is required user permission
  - Recommend querying Big Objects for data instead of subscring to past events from now to 3 days ago
  - Use EMP Connector, open source tool to connect via CometD
- Enhanced Transaction Security
  - Setup => Transaction Security Policies to set up new policies
  - Either use Condition Builder or Apex to create policies
    - Condition Builder: choose an event, conditional logic, and associated actions along with notifications via email or in-app 
    - Apex: choose an event, specify an Apex class, and associated actions along with notifications via email or in-app
      - `TxnSecurity.EventCondition` is interface implemented, has `evaluate` method that returns boolean to define whether it triggers the action
- Shield Platform Encryption (repeated from above section)
  - Encrypt only where necessary
  - Backup and archive keys and data
  - Encryption applies to all users


[**Customizing User Authentication with Login Flows**](https://www.youtube.com/watch?v=gYes8OLAc-k)



[**Configure a Salesforce Authentication Provider**](https://help.salesforce.com/articleView?id=sso_provider_sfdc.htm&type=0)



[**Social Single Sign-On with OpenID Connect**](https://www.youtube.com/watch?v=XIFMnzbG5Ew)



[**Identity 101: Design Patterns for Access Management**](https://www.youtube.com/watch?v=_0v3b029sH4&t=822s)



[**FAQs for Single Sign-On**](https://help.salesforce.com/articleView?id=sso_tips.htm&type=0)



[**Delegated Authentication**](https://help.salesforce.com/articleView?id=sf.sso_delauthentication.htm&type=5)



[**Configure SSO to Salesforce Using Microsoft AD FS as the Identity Provider**](https://help.salesforce.com/articleView?id=sf.identity_provider_examples_3p_adfs.htm&type=5)



[**OAuth Authorization Flows**](https://help.salesforce.com/articleView?id=sf.remoteaccess_oauth_flows.htm&type=5)



[**OAuth With Salesforce Demystified**](https://www.youtube.com/watch?v=zpToAGuhg60&t=540s&ab_channel=SalesforceDevelopers)



[**Authorize Apps with OAuth**](https://help.salesforce.com/articleView?id=sf.remoteaccess_authenticate.htm&type=5)



[**Connected App and OAuth Terminology**](https://help.salesforce.com/articleView?id=sf.remoteaccess_terminology.htm&type=5)



[**Connected App Basics**](https://trailhead.salesforce.com/content/learn/modules/connected-app-basics?trailmix_creator_id=strailhead&trailmix_slug=architect-identity-and-access-management)



[**Build a Connected App for API Integration**](https://trailhead.salesforce.com/content/learn/projects/build-a-connected-app-for-api-integration?trailmix_creator_id=strailhead&trailmix_slug=architect-identity-and-access-management)



[**Configuring SAML SSO for a Canvas App**](https://developer.salesforce.com/docs/atlas.en-us.sso.meta/sso/sso_examples_canvas.htm)



[**Security Basics**](https://trailhead.salesforce.com/content/learn/modules/security_basics?trailmix_creator_id=strailhead&trailmix_slug=architect-identity-and-access-management)



[**Journey to MFA: Launch Multi-Factor Authentication**](https://salesforce.vidyard.com/watch/O3rQLAtVX0Z4lLjdOvVFYQ)



[**Lightning Login Overview (Lightning Experience)**](https://salesforce.vidyard.com/watch/Pk8QwpPk9QguuzZPtVh5dR?_ga=2.159533757.1689205894.1618347339-1069822817.1618266881)



[**Multi-Factor Authentication**](https://help.salesforce.com/articleView?id=security_overview_2fa.htm&type=0)



[**Session-Based Permission Sets and Security**](https://trailhead.salesforce.com/content/learn/modules/session_based_perms?trailmix_creator_id=strailhead&trailmix_slug=architect-identity-and-access-management)



[**Session Security**](https://help.salesforce.com/articleView?id=sf.security_overview_sessions.htm&type=5)



[**Standard User Licenses**](https://help.salesforce.com/articleView?id=users_license_types_available.htm&type=5)



[**Identity Connect Basics**](https://trailhead.salesforce.com/content/learn/modules/identity_connect?trailmix_creator_id=strailhead&trailmix_slug=architect-identity-and-access-management)



[**Deploying Single Sign-on and Provisioning for Active Directory**](https://www.youtube.com/watch?v=kNRHsHcphg0&t=491s)



[**Identity for Customers**](https://trailhead.salesforce.com/content/learn/modules/identity_external?trailmix_creator_id=strailhead&trailmix_slug=architect-identity-and-access-management)



[**Identity for Mobile-Centric Customers**](https://trailhead.salesforce.com/content/learn/modules/identity-for-mobile-centric-customers?trailmix_creator_id=strailhead&trailmix_slug=architect-identity-and-access-management)



[**Connecting To Your Customers Across Every Channel With Salesforce Identity**](https://www.salesforce.com/video/1778176/)



[**Salesforce Data Mask**](https://trailhead.salesforce.com/content/learn/modules/salesforce-data-mask?trailmix_creator_id=strailhead&trailmix_slug=architect-identity-and-access-management)



[**Secure Secrets Storage**](https://trailhead.salesforce.com/content/learn/modules/secure-secrets-storage?trailmix_creator_id=strailhead&trailmix_slug=architect-identity-and-access-management)



[**Secure Salesforce Configuration**](https://trailhead.salesforce.com/content/learn/modules/secure-salesforce-configuration?trailmix_creator_id=strailhead&trailmix_slug=architect-identity-and-access-management)



[**Security Awareness and Training**](https://trailhead.salesforce.com/content/learn/modules/security-awareness-and-training?trailmix_creator_id=strailhead&trailmix_slug=architect-identity-and-access-management)