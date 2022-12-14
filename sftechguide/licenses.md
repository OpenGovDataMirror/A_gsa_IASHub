---
title: Licenses
keywords: mydoc
sidebar: sftechguide_sidebar
toc: true
permalink: /sf-tech-guide/licenses/
---
## Choosing Salesforce License Type
Salesforce offers different user license types for each organization.  User license entitles a user to different functionality within Salesforce and determines which profiles and permission sets are available to the user.  To view a list of the active user licenses for each organization, click 

~~~ 
Your Name > Setup > Company Profile > Company Information 
~~~
.  

### Reference
* See below for examples of the most common license types and their permissions.
* Note: Additional types exist and Chatter Plus is not currently being used.

|Feature|Chatter Free|Chatter Plus|Platform|Salesforce|
|---------|
|Chatter & File Tabs|✔|✔|✔|✔|
|Profiles, Feeds|✔|✔|✔|✔|
|People, Groups|✔|✔|✔|✔|
|Desktop & Mobile Apps|✔|✔|✔|✔|
|Chatter Invite (invite non-CRM users to Chatter)|✔|✔|✔|✔|
|Accounts & Contacts| |Read-Only|✔|✔|
|Content / Libraries| |✔|✔|✔|
|Reports & Dashboards| |✔|✔|✔|
|Ideas, Answers| |✔|✔|✔|
|Tasks, Activities| |✔|✔|✔|
|Calendar, Events| |✔|✔|✔|
|Custom Apps| |1|✔|✔|
|Custom Objects| |10|✔|✔|
|Knowledge / Articles| | |✔|✔|
|Visual Workflow / Workflow Approvals (submit)| | | |✔|
|Follow Opportun* ities & Cases| | | |✔|
|Follow Campaigns & Leads| | | |✔|

### Guideline

* Do not assume that all users will have access to all Salesforce features. Consider the intended audience for the application and what their license types are currently and what they will need to be.  

### Requirement

* License Type requirements will be reviewed by GSA Salesforce Solution Architects during design review. Licensing issues may be escalated as needed for further guidance. 
* GSA Salesforce Solution Architects shall consult with the Center of Excellence (COE) if the application is anticipated to affect Org licensing limits.  This includes both internal licenses (Platform, Salesforce) as well as external-facing licenses (Portal, Community).
* GSA Salesforce Government project leads shall consult with App Owners if the application is anticipated to result in additional licensing costs that may be subject to chargeback.
