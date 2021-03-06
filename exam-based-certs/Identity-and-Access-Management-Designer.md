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

- Secure assets
  - Least privilege
  - Appropriate level of access
  - Multi-factor auth
- When things go wrong there are costs
  - Direct
    - Compromised customer / employee details, business plans, financial data, IP
    - Downtime
  - Indirect
    - Fines and compensation
    - Legal costs
    - Reputation
    - Share price
- Two levels of security
  - Generic: API access, custom permissions, Visualforce, ability to request fresh access tokens
  - User and service specific: CRUD, FLS, record level sharing, system permissions, licensing

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

- Authentication vs authorization metaphor
  - Authentication: hotel front desk confirms you are who you say you are, gives you a key
  - Authorization: key provides access to scopes like room, pool, gym, etc
- OAuth access token
  - Request
    - `code`
    - `grant_type`
    - `client_id`
    - `client_secret`
    - `redirect_url`
  - Response
    - `access_token`
    - `instance_url`
    - `id`
    - `token_type`
    - `issued_at`
    - `signature`
- OpenID Connect is authentication built on OAuth 2.0 (authorization)
- Sample responses
  - Raw response
    - `id`
    - `issued_at`
    - `scope`
    - `instance_url`
    - `token_type`
    - `refresh_token`
    - `id_token`
    - `signature`
    - `access_token`
  - Client app decodes to the following
    - `exp`
    - `sub`
    - `aud`
    - `iss`
    - `iat`

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

- Terms
  - Federation Authentication: users login once to access many apps
  - SAML: open standard authentication protocol
  - Identity Provider: acts as trusted service to authenticate user identity
  - Service Provider: provides client app to which the user wants to access
  - SAML Request: SP sends to IdP to authenticate user
  - SAML Response: IdP sends to SP after authentication occurs, has signed SAML assertion
  - SAML Assertion: part of SAML response, asserts facts like username, email, etc
  - JIT Provisioning: create a new user account when user accesses SP for the first time
  - OpenID Connect: open standard authentication protocol built on OAuth 2.0
  - Custom Authentication Protocol: general term for any custom authentication protocol that is used with an authorization service
  - Authentication Provider: framework to connect Salesforce with authorization, authentication, or both
  - Relying Party: SP in OpenID Connect land
- Salesforce as SP
  - Predefined Auth Provider
    - Apple
    - Facebook
    - Google
    - Janrain
    - LinkedIn
    - Microsoft Access Control
    - Twitter
  - Configure via OpenID Connect
    - Amazon
    - Azure AD
- SAML SSO flows
  - SP initiated
    - User requests secure session to protected resource
    - Service provider initiates login via SAML request to IdP
    - IdP sends user to login page
    - User authenticates to IdP
    - IdP sends SAML response to SP
    - SP validates signature and identifies user
    - User is able to leverage protected resource of SP
  - IdP initiated
    - User authenticates to IdP
    - User tries to access SP
    - IdP sends SAML response to SP
    - SP validates signature and identifies user
    - User is able to leverage protected resource of SP

[**Deploying Single Sign-On and Identity for Employees, Customers, and Partners**](https://www.youtube.com/watch?v=swguz0ZKggM)

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

- What is it?
  - Can invoke business processes during login
  - Profile based association
  - Available in Salesforce, Experiences, and Salesforce Mobile
  - Supports username/password, SAML SSO, Social Sign On
- How it works?
  - Create a screen flow
  - Associate a user profile with the flow
  - User redirected to that flow, restricted access to login flow only, upon successful login gets full Salesforce access
- Use cases
  - Custom login experience
  - Post registration forms
  - Custom multi factor auth
  - Conditional login flows
  - Accept terms of service
  - Identity confirmation
  - Geofencing
  - Verify identities

[**Configure a Salesforce Authentication Provider**](https://help.salesforce.com/articleView?id=sso_provider_sfdc.htm&type=0)

- Allows for logging into external apps based on Salesforce credentials, requires a Connected App
- Configured within Setup => Auth. Providers
- Provide the URL suffix, which is basically after the base Salesforce URL (e.g. `/services/auth/sso/Name`)
- Paste consumer key and secret values from Connected App
- Set Authorize and Token Endpoint URLs, Default Scope, and Custom Error and Logout URLs
- Specify either an existing Apex class or create a new one that will act as template (needs to be modified)
- A variety of client configuration URLs are created
  - Test-Only Initialization URL: use to ensure third party service is set up corectly
  - Single Sign-On Initialization URL: use to perform SSO into Salesforce using third party creds
  - Existing User Linking URL: use to link existing Salesforce users to a third party service's account
  - OAuth-Only Initialization URL: use to get OAuth access tokens for a third party, need to authenticate with Salesforce in order to get tokens
  - Callback URL: auth provider redirects to this URL with information for each client config

[**Social Single Sign-On with OpenID Connect**](https://www.youtube.com/watch?v=XIFMnzbG5Ew)

- OpenID Connect
  - Identity protocol built on OAuth 2.0
  - Verify a user identity using auth by another server
  - Standard for sharing profile information
- Provide users with form of social sign on
- Allows users (internal and external) to log into Salesforce with other credentials
- Process
  - Register as an OAuth client with the identity provider
  - Configure Auth. Provider in Setup
  - Define logic for user management
  - Add Auth Provider to My Domain or Experience Cloud list of auth methods
- How to manage identities
  - Define logic in registration handler with Apex
  - Use profile information from provider
  - Either match to existing or create a new user
  - For previously logged in profile, update profile details
- OpenID Connect is built on OAuth 2.0
- OpenID Connect Identity + OAuth 2.0 Authorization = access
- Use authorization plus access token to access resources 
- Use scope to define access levels (same as OAuth 2.0)

[**Identity 101: Design Patterns for Access Management**](https://www.youtube.com/watch?v=_0v3b029sH4&t=822s)

- Leverage a single Salesforce org to act as hub (identity provider) to other service providers (Salesforce or Experience Cloud apps)
- Leverage social sign on to let people easily access Salesforce or Experience Cloud

[**FAQs for Single Sign-On**](https://help.salesforce.com/articleView?id=sso_tips.htm&type=0)

- SSO via SAML or OpenID Connect, or preconfigured Auth Providers for services with their own protocols (e.g. Facebook)
- SSO errors appear in Setup => Login History
- SAML response validation via Setup => Single Sign-On Settings, click SAML Validation after a user fails to log in via SSO
- SAML is disabled in sandboxes during copy, so test in those instances first
- Preventing users from logging in with their Salesforce creds and forcing SSO
  - Setup => Single Sign-On Settings => check Disable login with Salesforce credentials
  - Enforce at profile or perm set level with Is Signle-Sign On Enabled permission, must have Federation Identifier set on user
- Salesforce's MFA is supported only if Salesforce is the IdP
- Third party MFA service is permissible, ensure that the SSO configuration is configured as high assurance in Setup => Session Settings

[**Delegated Authentication**](https://help.salesforce.com/articleView?id=sf.sso_delauthentication.htm&type=5)

- SSO and delegated auth enable users to log into multiple apps with one set of credentials, except the user must log into each app separately
- Effectively, Salesforce takes a username and password and sends it to the external service to validate, along with source IP address which is where the login event initiated
- The external service must be accessible to Salesforce's servers
- Salesforce username must match to something in the external service's schema
- Password reset is disabled for delegated auth 
- See error histories in Setup => Delegated Authentication Error History
- To get started, Setup => API => Download Delegated Authentication WSDL
- Update Setup => Single Sign-On Settings => Delegated Gateway URL

[**Configure SSO to Salesforce Using Microsoft AD FS as the Identity Provider**](https://help.salesforce.com/articleView?id=sf.identity_provider_examples_3p_adfs.htm&type=5)

- Microsoft ADFS supports SAML 2.0
- IdP initiated: Browser goes to ADFS, ADFS returns to browser, browser forwards to Salesforce
- Need to use Kerberos SPNs to generate IIS instance
- But seriously y'all... it's way easier with Azure AD
- Ensure that approrpiate attributes are part of SAML response
- Federation ID is case sensitive unless Single Sign-On Settings is updated to treat it is case insensitive
- Other issues may be related to assertion expiring, where timestamp is 8 minutes past or 3 minutes prior

[**OAuth Authorization Flows**](https://help.salesforce.com/articleView?id=sf.remoteaccess_oauth_flows.htm&type=5)

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

[**OAuth With Salesforce Demystified**](https://www.youtube.com/watch?v=zpToAGuhg60&t=540s&ab_channel=SalesforceDevelopers)

- Roles in an OAuth Flow
  - Owner: a person that uses an app
  - Client application: the app to which the user interfaces
  - Resource server: the server to which the client app interfaces, but requires tokens that were granted to owner from authorization server
  - Authorization server: hands over authentication and authorization to that server, passes tokens to client app
- Tokens
  - Access: short lived (e.g. session ID)
  - Refresh: long lived, allows for getting a new access token, can be revoked
  - ID: related to OpenID Connect
- OAuth 2.0 is for authentication, identity is not in scope
  - Access token does not represent user identity
  - OpenID Connect built to create authentication layer with authorization from OAuth

[**Authorize Apps with OAuth**](https://help.salesforce.com/articleView?id=sf.remoteaccess_authenticate.htm&type=5)

- OAuth tokens give permissions to client app via tokens
- Resource server validates tokens from client app and provides access to resources

[**Connected App and OAuth Terminology**](https://help.salesforce.com/articleView?id=sf.remoteaccess_terminology.htm&type=5)

- Access token: client app uses this to gain access to resources on behalf of user
  - OAuth 1.0: exchanged for a session ID
  - OAuth 2.0: this is a session ID
- Authorization code: OAuth 2.0 web server flow uses this as a token with 15 minute life that can be exchanged for access and refresh tokens
- Authorization server: authorizes an owner, issues access tokens to that owner
- Callback URL: invoked after OAuth for client app, must either be a real URL or the same value as configured in the Connected App
- Consumer: client app that uses OAuth to auth a user and itself
- Consumer key: key to identify itself, the `client_id` 
- Consumer secret: establishes ownership of the consumer key, the `client_secret`
- OAuth endpoint: URLs to which OAuth requests are made to Salesforce
- Nonce: random nubmer used during auth to prevent reusing a request
- OAuth: standard, token-based protocol for authorization
- Refresh token: used in OAuth 2.0, client app can use to get a new access token without owner approving access again
- Request token: similar to authorization code, but for OAuth 1.0
- Resource owner: end user granting access to resource
- Resource server: hosts protected resource
- Token secret: owner uses to establish ownership of a given token for both request and access tokens

[**Connected App Basics**](https://trailhead.salesforce.com/content/learn/modules/connected-app-basics?trailmix_creator_id=strailhead&trailmix_slug=architect-identity-and-access-management)

- Framework to enable external app to integarate with Salesforce via API and protocols like SAML, OAuth, Open ID Connect; authorizes, authenticates, and provides SSO 
- Use Cases
  - Access data for API integrations
  - Integrate service providers with Salesforce
  - Provide authorization for external API gateways
  - Manage access to third party apps
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
- Salesforce can be the IdP leveraging both SAML and OpenID Connect
- OpenID Connect has dynamic client registration
  - Enables resource servers to dynamically create client apps as connected apps
  - Sends request to create a connected app for client app
- OpenID Connect has token introspection
  - Check curent state of OAuth 2.0 access and refresh tokens
  - Resource server sends client ID and secret to auth server, if access token is current and valid, resource server granted access

[**Build a Connected App for API Integration**](https://trailhead.salesforce.com/content/learn/projects/build-a-connected-app-for-api-integration?trailmix_creator_id=strailhead&trailmix_slug=architect-identity-and-access-management)

- Connected App => Enable OAuth Settings
  - Permitted Users is either all may self-approve or only admin approved users are pre-authorized via profile
  - IP Relaxation enfores the IP restrictions for org, could be relaxed for refresh tokens, or pre-activated devices, or not have any restrictions at all

[**Configuring SAML SSO for a Canvas App**](https://developer.salesforce.com/docs/atlas.en-us.sso.meta/sso/sso_examples_canvas.htm)

- Link above redirects to a different page, instead referencing [SAML Single Sign-On for Canvas Apps](https://developer.salesforce.com/docs/atlas.en-us.platform_connect.meta/platform_connect/canvas_app_saml_sso_intro.htm)
  - `refreshSignedRequest` returns new signed request via callback, can be initiated after SAML SSO process is completed, is more client-side JS focused
  - `repost` asks parent window to `POST` to canvas app, reloads app page with refreshed signed request, uses server-side approach

[**Security Basics**](https://trailhead.salesforce.com/content/learn/modules/security_basics?trailmix_creator_id=strailhead&trailmix_slug=architect-identity-and-access-management)

- Exploits to human behavior: fear, trust, morality, reward, conformity, curiosity
- Attack methods: phishing, malware, social engineering, exploiting public information, tailgating, eavesdropping, dumpster diving, installing rogue devices
- Passwords: unique, complex, change often, keep to yourself, use a password manager
- Phishing: check subject and sender's email on Google, consider source and verify links, check with Salesforce (if spoofing Salesforce)
- Remote workspace: use VPN, secure virtual meetings, secure background, use headphones, uses locks and wifi passwords, keep device soft/firmware up to date
- Salesforce
  - Use MFA
  - Restrict IP ranges on profile and perm set level
  - Freeze and deactivate former users
  - Limit to least rights required
  - See what those users have done
  - Implement Salesforce Shield to encrypt, leverage transaction security policies, and monitor events
- Use Security Settings => Health Check to determine org health
  - Click Fix Risks button to change to recommended values
  - Security Center is an add-on that can run Health Check across multiple orgs

[**Journey to MFA: Launch Multi-Factor Authentication**](https://salesforce.vidyard.com/watch/O3rQLAtVX0Z4lLjdOvVFYQ)

- Send an email
- Test with a permission set on a user
- Decide which method to use (Salesforce Authenticator, physical security key, other authenticator app)
- Conduct training

[**Lightning Login Overview (Lightning Experience)**](https://salesforce.vidyard.com/watch/Pk8QwpPk9QguuzZPtVh5dR?_ga=2.159533757.1689205894.1618347339-1069822817.1618266881)

- Allows user to log in via Salesforce Authenticator on their mobile app when "Remember Me" is selected in browser that previously had a successful authentication with username/password (and presumably uses cookies?)

[**Multi-Factor Authentication**](https://help.salesforce.com/articleView?id=security_overview_2fa.htm&type=0)

- Salesforce will require MFA for all users logging in via Salesforce UI
- Methods for MFA
  - Salesforce Authenticator
  - Use Touch ID, Face ID, or similar as built-in auth (beta)
  - Register U2F security key
  - Verify with TOTP authenticator app
- Click Disconnect to remove any of those methods above if a user has already connected
- Able to create a temporary verification code manually on user record via Temporary Verification Code, and can expire that code as well

[**Session-Based Permission Sets and Security**](https://trailhead.salesforce.com/content/learn/modules/session_based_perms?trailmix_creator_id=strailhead&trailmix_slug=architect-identity-and-access-management)

- Session Activation Required checkbox on perm set defines the set of perms is only available with activated session
- Use Flow or Apex to activate session-based perm sets

[**Session Security**](https://help.salesforce.com/articleView?id=sf.security_overview_sessions.htm&type=5)

- Setup => Session Settings
  - Session Timeout from 15 minutes to 24 hours
    - Last active session time value isn't updated until halfway through activity period
  - Session Settings
    - Lock sessions to IP address from which originated
    - Allow employees to log in directly to Experience Cloud site
  - Secure Connections
    - Force relogin after login-as-user
    - Require HttpOnly attribute to restrict session ID access (prevents calls from JavaScript)
    - Use POST for cross domain sessions (to keep session details in body, not request URL)
    - Enforce login IP ranges for all requests
  - Caching settings
    - Enable caching and autocomplete on login pages 
    - Enable secure and persistent browser caching to improve performance
      - Turn this off if you're rapidly testing UI with saves to server in sandboxes, but it'll kill your perf with Lightning in prod
    - Enable user switching 
    - Remember me until logout
    - Enable CDN for Lightning Component framework (uses Akamai to load Salesforce's framework)
  - Clickjack Protection Settings
    - Enable clickjack protection for customer VF pages with standard headers or headers disabled
    - Allow iframes on trusted external domains if necessary
  - Cross-Site Request Forgery (CSRF)
    - Automatically protected with random string of characters in URL parameter or hidden form field for GET and POST requests respectively
  - Content Security Policy Protection
    - Override resriction on accessing email templates in Salesforce Classic Using IE
    - Enable Stricter Content Security Policy to avoid using `unsafe-inline` for `script-src`
  - Extra Protection
    - Enable XSS to avoid cross site scripting 
    - Enable Content Sniffing protection to prevent browser from inferring MINME type, executing JS / CSS as dynamic content
    - Hide this site's URL from other web sites (including VF pages) shows only Salesforce.com instead of entire URL in referred header when pages load
    - Warn users before they are redirected outside of Salesforce shows warning when leaving Salesforce
  - Session Security Levels: standard or high assurance
    - Username and Password
    - Delegated Auth
    - Activation
    - Lightning Login
    - Passwordless Login
    - Multi-Factor Auth
    - Auth Provider
    - SAML
  - High Assurance Settings
    - Can be required for reports, dashborads, and connected apps
  - Logout Page Settings
    - Used only if Logout URL is blank for IdP, SAML SSO, or third party auth
  - Session Settings for New User Email
    - Link expires in 1, 7, o 180 days; applies to existing links
- Enable Browser Security Settings
  - Referrer URL Protection: referrer header shows only Salesforce/Force.com URL
  - Public Key Pinning: supported by Chrome and Firefox, monitors which SSL certs a user can see
  - HSTS Protection: redirects browsers to use HTTPS and cannot be disabled
- Setup => Network Access
  - Defines list of IP addresses from which users log in without verifying their identity (i.e. MFA)
- Setup => Identity Verification
  - Require High Assurance Session Security for Sensitive Operations
  - Define policy leevls for a variety of pages along with Reports and Dashboards, either raising to high assurance or blocking user
- Can revoke sessions on per user basis 
- Setup => Session Management
  - View sesssion types for specific user 
- Use frontdoor.jsp to bridge an existing session
  - Parse session ID from serverUrl of the LoginResult returned from SOAP API `login()` call via POST request with `sid` and optionally `retURL` 
  - OAuth 2.0 Hybrid App Token Flow can use POST request to frontdoor.jsp with `directBridge2=true` parameter, which passes access token to session ID cookie
  - `access_token` is a full session ID when obtained from OAuth, will need either `web` or `full` scope in connected app definition

[**Standard User Licenses**](https://help.salesforce.com/articleView?id=users_license_types_available.htm&type=5)

- Salesforce: full access to CRM and AppExchange apps
- Knwoeldge User Only: only provides access to articles, article management, chatter, files, home, profile, reports, custom objects, custom tabs
- Identity Only: provides SSO access to other apps via Salesforce
- External Identity: enables customers/partners to self register, securely access web and mobile apps 
- WDC Only User: for those orgs that are still using Work.com
- Salesforce Platform: custom apps, not full CRM activity, does not have access to forecasts, leads, campaigns, opps, etc
- Lightning Platform - One App: only one app, 10 custom objects at most, read only for accounts and contacts, unlimited number of tabs
- Force.com - App Subscription: one app, 10 custom objects, read only for accounts and contacts, 10 tabs, can only view dashboards if running user has same license; not technically monitored by Salesforce, is contractual in nature
- Company Community User: employee communities, files, chatter, Experience Cloud site, 10 custom objects, 10 tabs, activities, tasks, calendar, events, accounts, contacts, cases, documents
- Developer: provides one dev sandbox, scratch org, access to Dev Hub

[**Identity Connect Basics**](https://trailhead.salesforce.com/content/learn/modules/identity_connect?trailmix_creator_id=strailhead&trailmix_slug=architect-identity-and-access-management)

- Syncs changes from Active Directory to Salesforce
- Provisions users for onboarding and offboarding automatically
- Set up SSO to allow users to access Salesforce via AD credentials
- Use Data Source tab to map base contexts, user and group filters by Objectclasses
- Map Salesforce user attributes to AD, default value, or a transformation script
- Able to map permissions and access based on AD group
  - Profile to AD Group
  - User Role to AD Group
  - Permission Set to AD Group
  - Group (i.e. public group) to AD Group
- Deployment
  - On-premise, AD communicates via LDAP(S), and Identity Connect needs to communicate to Salesforce via HTTPS (DMZ is likely place to put Identity Connect)
  - Can support multiple Salesforce orgs
  - Can support multiple AD domains, although needs to aggregate via global catalog prior to entering Identity Connect or use multiple instances of Identity Connect
  - An instance of Identity Connect can support either production or sandbox instances, but not a mix of both

[**Deploying Single Sign-on and Provisioning for Active Directory**](https://www.youtube.com/watch?v=kNRHsHcphg0&t=491s)

[**Identity for Customers**](https://trailhead.salesforce.com/content/learn/modules/identity_external?trailmix_creator_id=strailhead&trailmix_slug=architect-identity-and-access-management)

- With Person Accounts enabled, ensure that an Experience has registration page configuration with a blank Account, which will ensure that newly created external users are created as Person Accounts
- Records are created in this order
  - Person account
  - Contact
  - User

[**Identity for Mobile-Centric Customers**](https://trailhead.salesforce.com/content/learn/modules/identity-for-mobile-centric-customers?trailmix_creator_id=strailhead&trailmix_slug=architect-identity-and-access-management)

- Mobile first identity for these licenses
  - External Identity
  - Customer Community
  - Customer Community Plus
  - Partner Community
  - Lightning External Apps
  - Lightning External Apps Plus
- Available with email verification for free, can provide text messaging for add-on license of Identity Verification Credits
- Login Discovery supports both password and passwordless login methods, so that is ideal page for login/self registration
- Customize login discovery handler for social sign-on
  - Set up Auth Providers (for social networks, as example)
  - Locate SSO URLs for that network
  - Check `ThirdPartyAccountLink` SObject to see if the `Handle` matches that user's email
    - If so, redirect user via `PageReference` to the associated `AuthProvider.SsoKickoffUrl` for that social platform
  - Also can use `requestAttributes` to find details like
    - `CommunityUrl`
    - `IpAddress`
    - `UserAgent`
    - `Platform`
    - `City`
    - `Country`
    - `Subdivison` (state/province)
- Use these reports report types to track usage
  - Verification History 
  - Identity Verification Methods

[**Connecting To Your Customers Across Every Channel With Salesforce Identity**](https://www.salesforce.com/video/1778176/)

- Create login flow to inject terms of service, new features, etc based on checking the user
- Setup => Login Flow, map that to a user profile
- Various input variables are available in the flow
  - `LoginFlow_LoginType`
  - `LoginFlow_IpAddress`
  - `LoginFlow_UserAgent`
  - `LoginFlow_Platform`
  - `LoginFlow_Application`
  - `LoginFlow_Community`
  - `LoginFlow_SessionLevel`
  - `LoginFlow_UserId`
- Experience ID `{expid}` can be injected into the logo URL, right frame URL within Experience => Administration => Login & Registration, and that would map to a different piece of content in CMS
- Dynamic branding is possible with a single community that supports many brands
- `Site.getExperienceId()` allows for this on Apex side
- Setup => CORS to ensure that Salesforce is allowed to communicate with an external site (e.g. your ecommerce store)
- Setup => Connected App to setup OAuth app with a client ID and callback URL that is added to the external client app's code to assist with Embedded Login 
- Salesforce Identity components in action
  - Quick and easy registration => Auth Providers
  - Social Sign On => Auth Providers
  - Create Accounts, Contacts, Users => Registration Handlers (Apex)
  - Progressive profiling and consent => Login Flow
  - No browser redirects => Embedded Login
  - Multiple brands in single org => Dynamic Branding

[**Salesforce Data Mask**](https://trailhead.salesforce.com/content/learn/modules/salesforce-data-mask?trailmix_creator_id=strailhead&trailmix_slug=architect-identity-and-access-management)

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

[**Secure Secrets Storage**](https://trailhead.salesforce.com/content/learn/modules/secure-secrets-storage?trailmix_creator_id=strailhead&trailmix_slug=architect-identity-and-access-management)

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

[**Secure Salesforce Configuration**](https://trailhead.salesforce.com/content/learn/modules/secure-salesforce-configuration?trailmix_creator_id=strailhead&trailmix_slug=architect-identity-and-access-management)

- Health Check is a dashboard to show ranking of 0-100 for how secure the org is
- Provides a set of recommendations to implement
- Salesforce Shield provides
  - Platform Encryption
  - Event Monitoring
  - Field Audit Trail

[**Security Awareness and Training**](https://trailhead.salesforce.com/content/learn/modules/security-awareness-and-training?trailmix_creator_id=strailhead&trailmix_slug=architect-identity-and-access-management)

- Assist with stakeholder buy in on being a security minded organization