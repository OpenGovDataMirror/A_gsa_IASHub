---
title: Development
keywords: mydoc
sidebar: sftechguide_sidebar
toc: true
permalink: /sf-tech-guide/development/
---

This section describes key development principles and guidelines (both declarative configuration as well as Apex/VisualForce code) for designing and developing efficient and scalable applications at GSA.

Note the following general rules for when to use configuration vs. custom development in force.com at GSA: 

## Configuration

### Reference

- N/A

### Guideline

- Creating custom objects –
	- Where possible, reuse existing standard or custom objects before creating new objects.  Record types can be used to isolate application specific functionality and data elements.  Seek guidance from GSA’s Solution Architects to explore the possibility of reusing existing standard or custom objects.
	- Build custom reports and dashboards for new custom objects (in alignment with business needs).
	- Provide meaningful names and labels for your custom objects.  However, try to name them generically enough that they can be reused by other applications.
- Defining relationships
	- Review the ERD available in the Force.com API documentation before creating new objects or relationships.
- Creating custom tabs
	- Select the “Append tab to users’ existing personal customizations” checkbox when adding custom tabs to custom apps.
- Creating Custom Fields
	- Provide meaningful names and labels for your custom fields.  However, try to name them generically enough that they can be reused by other applications.
	- Provide Help Text when doing so will clarify the purpose of the field or the expected responses.
	- Populate the Description field for custom fields to inform Administrators of the purpose of the field and why it was created.
- Field-level security
	- Where possible, set field-level security using permission sets, not profiles.
	- To enable field-level security to be managed at the permission set level, be sure to uncheck access to fields at the Profile level. 
		- The exceptions are the “System Administrator”, “GSA System Administrator” and “System API” profiles, which should have access to everything at the Profile level.
- Page Layouts
	- Minimize the number of page layouts for each object -- aim to use the least number of page layouts to accomplish all business requirements. Create a different page layout only if needed (e.g., for multiple record types).
- Do not use page layouts to restrict access to fields -- this should be done using permission sets and field-level security.
- Record Types –
- Minimize the number of record types for each object.  Only create record types where there are differences in fields to be displayed (with corresponding page layout) or picklist values.  Do not create a record type when a simple “Type” field will suffice.
- Record types should be assigned via permission sets, not profiles.
	- Assign Page Layouts to record types as appropriate.
- Workflow (Field Updates)
	- In general, the use of Workflow is preferred to handle new “Field Update” actions.  An exception to this would be where “Field Update” actions already exist within a Trigger -- in this case it is preferable to use the existing Trigger.  Consolidating field updates to either Workflow or Trigger logic will ease debugging and code maintenance and will be less likely to result in unintended updates (as Workflow changes may cause Triggers to execute again, and vice versa).
- Validation Rules
	- Be selective in using validation rules to avoid situations where they run unnecessarily. 
- Approval Process
	- Before you begin creating an approval process, draw a diagram of the steps in the approval process.
	- Clone processes to create similar ones more quickly.
- Contact vs. User Lookup
	- Only use a user lookup if you need to leverage user functionality (e.g., sharing a record, approval process), otherwise, always use a contact lookup.
- Report/Dashboard Folders
	- Each application should have its own report folder and dashboard folder (as applicable).  
	- Visibility to report and dashboard folders should only be given to users who are using the app to which the folders apply.  
	- Access to an app’s report and dashboard folders for app users should be read-only.
- Existing Utilities
	- Become familiar with the utilities available on the target Org.  Reuse existing utilities across applications where possible. 
   
### Requirement

- Creating custom objects
	- Always populate the Description field for new custom objects to inform Administrators of the purpose of the object and why it was created.
- Creating custom tabs
	- Create permissions for new tabs and page layouts so that they can be deployed without users seeing the changes until they are finalized.
- Profiles/Permission Sets
	- Where possible, application-specific permissions must be assigned at the permission set level.
	- New profiles may only be considered if functionality is needed that cannot be implemented using permission sets (e.g., org-wide email address).  
	- GSA has created certain generic profiles based primarily on license type.  These profiles may not be modified for use by an application.  
	- Permission sets must be license-agnostic.
- Role Hierarchy
	- Always consult with GSA’s Solution Architects before using role hierarchy.  
	- Role-based functionality such as sharing is to be mimicked via the use of public groups and sharing rules where role hierarchy is discouraged.
	- Note: Certain GSA Orgs (e.g., EEO) do not leverage the role hierarchy due to issues with reliable sources of role information and role maintenance processes.
- AppExchange
	- AppExchange packages should not store data outside of salesforce.com, unless both the storage location and the transfer mechanism have gone through Assessment and Authorization (A&A).
	- All AppExchange packages (free or paid) must pass a code scan prior to being deployed to production.
- Branding
	- Replace the Salesforce-branded logo in the upper-left corner of the screen with a logo developed for the application or the standard GSA logo.

### EEO Org-Specific Details

- Existing Utilities
	- The section in this document titled ADDITIONAL TECHNICAL RESOURCES & REFERENCES contains a list of utilities available for reuse in the EEO org.  Please consult a GSA Solution Architect for additional details and/or an updated list of utilities.
- Approval Process
	- The EEO org does not leverage the standard “Manager” field on the user record, so this cannot be leveraged in an approval processes.
- Contact vs. User Lookup
	- EEO users are also created/updated as contacts via an automated feed.
- Report/Dashboard Folders
	- Certain EEO report and dashboard folders have been created and labeled with the prefix “Sharing”.  All users have the ability to save reports/dashboards to these folders.

## Apex Coding

### Reference

- Apex Best Practices
http://wiki.developerforce.com/page/Apex_Code_Best_Practices
- Salesforce Secure Coding Guidelines: https://developer.salesforce.com/page/Secure_Coding_Guideline
- Force.com Security Source Scanner Help: http://security.force.com/security/tools/forcecom/scannerhelp

### Guideline

- Avoid complex logic in triggers
- Complex logic in triggers should be avoided. Instead, use a separate class to encompass business logic as this facilitates code reuse and simplifies the test process.
- Modular code
	- Code should be modular and reusable whenever possible to improve readability and lower maintenance costs.
- Triggers and Validation Rule Check
	- All triggers and validation rules written on standard objects should check for application-specific constraints like profile ID or record type.
	- Both triggers and validation rules should be selective in when they run.  For example, a trigger may only need to fire when a status changes from one value to another and not for any change to the record.  A similar standard should be applied for validation rules.
- Custom Settings
	- Use Custom Settings to hold parameters or variables that could change from environment to environment or to enable changes to things like labels, text in Visualforce pages, or error messages.
- With Sharing keyword
	- Explicitly use ‘With Sharing’ or ‘Without Sharing’ keywords to assert whether the class should enforce record/row visibility or not.
- Separate Unit tests from functional classes
	- Apex test methods should be in their own classes, decoupled, to allow for refactoring and ensuring that private methods are not directly accessed.
- Hard-coding Strings
	- Avoid hardcoding strings (e.g., picklist values) as picklist values can change, and making the change across multiple classes and test classes can make a small change into a large effort.  Rather, use Custom Settings or a Class to hold and reference these static values so that the change is only needed in a minimum number of places.

### Requirement

- Checkmarx scan
	- A Checkmarx scan using the GSA internal Checkmarx tool must be performed on all Apex classes, triggers, and Visualforce pages. All potential vulnerabilities identified in the Checkmarx scan must be addressed (either by fixing them or receiving explicit permission to proceed from GSA security) before code may be deployed to upper environments such as Integration, Staging, and Production. Work with your Org’s administrator to conduct these scans.
- One trigger rule
	- There must be only one trigger for each object. The sequence of trigger execution cannot be controlled in Salesforce and having multiple triggers significantly reduces code manageability.
- Test Coverage 
	- All Apex classes and triggers must have test coverage of 90% and above. Specifically, each individual Apex class and trigger must have a test coverage of 90% and above.  Exceptions (classes or triggers with code coverage below 90%) may be granted on a case-by-case basis at the discretion of the destination Org Owner though they will require written justification and written approval.

## Visualforce Coding

Visualforce code allows developers to customize functionality as well as the look and feel beyond the constraints of the standard force.com development platform.  With the added flexibility of the custom Visualforce code comes a few downsides, including

- Increased future O&M costs
- Increased future enhancement costs

### Reference

- Best Practices for Improving Visualforce Performance:   http://www.salesforce.com/us/developer/docs/pages/Content/pages_best_practices_performance.htm
- Visualforce Developer’s Guide:   http://www.salesforce.com/us/developer/docs/pages/salesforce_pages_developers_guide.pdf

### Guideline

- Use FieldSets where appropriate
	- FieldSets allow an admin, in addition to a developer, to add/remove a field on a Visualforce page.  
	- Note: FieldSets have some limitations, like the inability to add a blank space.
- Look and Feel
	- Visualforce pages can look disjointed when styling is different.  Try to make use of pageblock titles, subtitles, and sectionheader tags and attributes to mimic standard Salesforce layout look & feel.   For example, when a pageblocktable has no records, it takes a few lines in Visualforce to add a “No records to display” message, but adding this text is best practice because it unifies the experience between Visualforce and standard Salesforce. 
	- Tab Order / Keyboard (like Enter) can improve the usability of applications when consistently applied to page layouts.  Keep Section 508 compliance in mind when designing tab order.
- Too Much Visualforce
	- If it is determined that an application requires more than 20% Visualforce code, present it for review by GSA’s Solution Architects to re-validate that the Salesforce platform is indeed the right fit for the business need.
- Javascript Libraries (JQuery, ExtJS, etc.)
	- Use static resources instead of direct links to Google APIs, for example.  This enables controlled versioning and decouples Salesforce from library hosts.
	- Avoid logic in JavaScript where possible as it cannot be unit-tested with Apex test classes.

### Requirement

- N/A

## GSA Naming Conventions
This section describes the coding styles which should be strictly followed by all the application teams.

### Reference

- N/A

### Guideline

See GSA naming conventions in the table below


|Type|Naming Convention|Examples|Additional Comments|
|-----|
|Public Groups|	{AppName}-{Short Description}|	EventTracker-OAS-Approvers<br> EventTracker-OGC-Approvers<br> FDCCI-DHS<br> FDCCI-DOD<br>	FDCCI-DOD-Army<br>	FDCCI-DOD-Navy|	|		
|Profile|	{GSA}{AppName}{LicenseType}{User}|	GSA FTRD Salesforce User|	If application name is too long (must be less than 80 characters), use abbreviations (otherwise spell out). If the profile spans applications, remove the “App Name” portion of the naming convention.  License type represents the type of Salesforce license, for example Salesforce, Platform, Chatter Free, OHVCP (Overage High Volume Customer Portal).|	
|Permission Set|{AppName}-{UserRole}-{LevelOfPermission}|	Note: Permission set description is required.	GITGO - User - R <br>GITGO - User - CRED|	User Role is dependent upon application functionality (e.g., user, admin, manager) and is not related to Salesforce.com role hierarchy.  CRED refers to the general permission (Create, Read, Edit, Delete) that is granted to user through this permission set.  Name must be less than 80 characters.|				
|Apex Custom Components (Classes / Triggers)|	{AppName}{FunctionName}{Category}{“Test”}|FcicArticlesController <br>
FcicArticlesControllerTest <br>FcicArticlesHelper <br> FcicArticlesHelperTest|The term Function (as in “FunctionName”) refers to a technical module or object.  See examples.|				
|Apex Custom Component (Pages)|	{AppName}{FunctionName}{Page}|FcicArticlesPage|	The term Function (as in “FunctionName”) refers to a technical module or object.  See examples.|				
|Apex Method Names|	{Action}{FunctionName}  <br>OR  <br>{“test”}{Action} <br>{FunctionName}|RetrieveAllArticles() <br>PopulateArticles() <br>TestRetrieveAllArticles|	The term Function (as in “FunctionName”) refers to a technical module or object.  See examples.  <br>Note:Apex method description is required.|	
|Email Templates|	{AppName}{NameOfTemplate}	|	FcicCaseConfirmationEmail|	|		
|Workflow Rules|	{AppName}{ObjectName}{ShortDescription}| FcicOpportunityNearingClosingDate|		|				
|Workflow Action Names|	{AppName}<br>{ActionShortDescription}|FcicUpdateCloseDate|				
|Approval Process|	{AppName}{ProcessShortDescription}|		FcicAgeGreaterThan25|		|				
|Visualforce Components/Static Resources|	If specific to application:<br>{App Name} {Component Name}<br><br>Or:<br><br>{GSA}{Component Name}|	FrppGridComponents <br>GsaGridComponent <br>GsaSiteLoginComponent|	Note:Visualforce component description is required|				
|Custom Settings|	{AppName}{CustomSettingName}|	FcicThirteenOrginalStates|	Note:Custom setting description is required|	


### Requirement

- Apex Header Information
	- All apex classes, components and triggers must have a header comment. This comment must include 
		- the application,
		- where it is being used, and 
		- contact information for the person(s) who wrote the code, as below

~~~
/******************************************************************************************
* 
* Description: <Include the Application which is using this class along with purpose of class and contents>
* 
*
* Modification Log:
* -----------------------------------------------------------------------------------------
* Mod ID      |   Date               	| Mod Author                            	| Brief Mod Description 
* -----------------------------------------------------------------------------------------
* 0001          |  1/1/2014        	| <Developer Name or	| Initial code creation.
*			     Application Contact >          
* -----------------------------------------------------------------------------------------
*
*******************************************************************************************/
~~~


### CEO Org-Specific Details

- Permission Set
	- Permission set names shall use the convention indicated in the “Requirement” section above but must also be restricted to 40 characters in length.  Where necessary, the app name or role can be abbreviated to accomplish this, so long as the same abbreviations are used consistently for all permission sets related to a given app.

## Integrations & Data Migration

This section describes practices specific to integrations and data migration.

### Reference

- Integration Resources
http://wiki.developerforce.com/page/Integration
http://www.google.com/url?q=http%3A%2F%2Fwww.salesforce.com%2Fus%2Fdeveloper%2Fdocs%2Fintegration_patterns%2Fintegration_patterns_and_practices.pdf
- Best Practices with Any Data Loader: http://www.salesforce.com/us/developer/docs/api/Content/best_practices_with_any_data_loader.htm

### Guideline

- Avoid custom-coded integrations
	- Custom-coded integrations are challenging to maintain and monitoring/visibility are often afterthoughts in implementation, leading to unnecessary complexity and lack of non-technical user manageability.
- Test, test, test
	- Leverage Full Sandbox Environments for testing wherever possible, and test using production size data volumes, using both source and target data that reflect production, ideally with a separate integration environment.
- Demand robust logging and error notification
	- Integrations should provide a consolidated source of summarized history, email alerts, along with actionable logs and a call plan for who is notified and the process for how issues are resolved if a job fails.
- Avoid personal accounts
	- When migrating data, use a general system administrator or the standard deployment user account; do not use a personal user account.
- Web service selection
	- Depending upon the destination Org, the web service protocol, framework and specification should be selected by liaising with the respective Org’s Solution Architect. GSA uses SOAP based web services for integration with the existing Enterprise Service Bus (ESB).
	- Use Outbound messaging and callback pattern for calls from Salesforce to leverage out of the box retry and error logging functionality where appropriate depending on transaction volume, requirements for message reliability, or operational requirements for managing queued messages.

### Requirement
- Optimize Security and Profiles
	- Ensure integration-critical fields are not editable by Salesforce users.
	- Leverage integration-specific user accounts for traceability and configure the user account to only have access to needed objects and provide ‘API only’ access on the user profile account.
- Adhere to 2-Factor requirements
	- Do not migrate non-sanitized Production data into a force.com environment that is not secured by 2-factor authentication (for testing purposes or otherwise). 

## Iframe Guidelines
Iframes can be a problematic design element for a number of technical and functional reasons, as detailed below. 

### Reference
- Inline Frame (iFrame) Definition: http://www.techopedia.com/definition/13639/inline-frame-iframe

### Guideline
- Technical Design
	- Before including an iFrame as a design element in an application, there should be a reasonable effort to determine and evaluate alternatives. If alternatives are not suitable, a justification as to the reason for using an iFrame should be provided in the Technical Design Document.
	- When submitting a Technical Design Document that includes iFrames, provide a brief explanation describing the plan addressing each item in the Compliance section or why it is not applicable.
- iFrame appearance
	- Changes in the layout of iFramed content may impact the appearance on the parent page.  Be prepared to account for this.
	- iFrames are usable across browsers; however, there may be variation from browser to browser regarding how content is displayed. For applications that targeted internally to GSA users, iFrames coding should be tested using the latest GSA approved browser standards.
- Section 508 Compliance
	- To ensure Section 508 compliance, consider having the site tested by the GSA Accessibility team.

### Requirement
- Same origin/framebusting
	- The content inside the iFrame must permit itself to be iFramed by another page, but subject to the same origin requirement.
	- If the content inside the iFrame finds itself iFramed by an unauthorized page, then it must either not load the content or have a mechanism to break out of the iFrame.
- Mixed content/HTTPS (note: these are technical limitations)
	- At least the login portion of a site must go through HTTPS.
	- If there is sensitive data protected by the login, then the whole site must be hosted on HTTPS.
	- If using iFrames, then the content inside the iFrames must also be HTTPS to prevent the user from receiving a 'mixed content' browser error.
- Section 508 compliance
	- Since iFrames are not inherently Section 508 compliant, an alternative to the iFrame for compatibility browsers must be provided.
	- During deployment, results of the Section 508 compliance check must be included in the documentation.
- Script communication between parent and iFrame
	- The script from the iFrame must not talk to the script on the Force.com site.
	- If this communication is absolutely necessary, then written documentation of accompanying security measures is required.
- Permission to publish content
	- Because the content is displayed via a Force.com site, provide a documented copy of approvals made by GSA Communications, Privacy, and/or Security teams to the group responsible for updating the content inside the iFrame.

## Canvas Guidelines

The following details the best practices and requirements for the use of Salesforce Canvas.

### Reference
- http://www.salesforce.com/us/developer/docs/platform_connect/canvas_framework.pdf

### Guideline
- Verify that the canvas integrations with Salesforce websites and mobile apps produce the same user experience. 
- The canvas frame size should be maintained dynamically to respond to user actions.
- Canvas Access Method should be “Signed Request(POST)” instead of “Signed Request(GET)”. 

### Requirement
- External applications must be accessed securely via SSL (https).

## Javascript Restrictions (JQuery)
The following guidelines reference the use of Javascript in Salesforce applications / modules.
JQuery is a cross-browser library designed to simplify client-side scripting of HTML.  

### Reference
- http://jquery.com/
- Appendix: 6.4 Javascript Restrictions (JQuery) Best Practice Examples

### Guideline
- Regular javascript functions on Visualforce pages are not recommended.  Instead make use of a published javascript framework such as JQuery. 
- Use the JQuery.noConflict() function to reassign jQuery’s global variable to something which won’t conflict with any existing libraries.
- Write code to maximize performance and ease maintenance.  See Appendix 6.4 JAVASCRIPT (JQUERY) BEST PRACTICE EXAMPLES for more details.
- Minimize client side scripting where possible.

### Requirement
- Ensure all javascript functions render across different browsers (Internet Explorer, Chrome, etc)
- If client side data parsing is required, use JQuery.

## Mobile Guidelines
The following details how to ensure your mobile-friendly applications and pages.  With the increasing use of mobile devices, it is important to build your applications to be mobile-friendly from the start. This is a relatively easy lift through the use of Bootstrap and is our preferred solution for developing mobile friendly pages with VisualForce.

### Reference
Bootstrap homepage

### Guideline
- Build and test all communications and applications to be compatible with mobile. This includes functionality, look and feel, user experience, and data capture.
- Verify that your application has properly utilized Bootstrap by changing your browser page width and using the function to view through a mobile device.
- Verify that Bootstrap is uploaded to your org. Avoid uploading multiple versions of Bootstrap.

### Requirement
- All applications and communications must be built with mobile in mind. Ensure that images, paragraphs, divs, headings, footers, etc. are all fluid width. Use percentages, not pixels. Any technology that is built or tested must also be built or tested for mobile.
- All applications should use Bootstrap to be mobile-friendly. Exceptions can be made, but must be approved through COE.
- Bootstrap must be built in from the beginning of the project, not added at the end as an afterthought.
- In the case of an existing application being updated, any VisualForce pages that are touched should also be updated to utilize Bootstrap. In the event that there are only minor updates, you may not be required to convert the page to be mobile friendly. Exceptions should be approved in Design Review.

## Communities
HTTPS
Per OMB Memo M-15-13, all community pages require HTTPS.

### Reference
OMB Memo M-15-13

### Guideline
- Clone this - ticket and update as needed for the given community.
- This request can take over a week to complete, plan accordingly.
- Enforce HTTPS-only across all community pages and utilize HTTP Strict Transport Security (HSTS)

### Requirement
- All communities must utilize and enforce HTTPS for all pages. 

## Style and Branding Guide

### GSA Logo 
- Use one of the downloadable files of the Star Mark found on InSite: https://insite.gsa.gov/portal/content/514554 
- The GSA Star Mark should be aligned on the left-hand side of the page 
 
### Abbreviations and Acronyms
- Avoid acronyms when possible and always identify acronyms on first use
- The acronym GSA can be used throughout websites (it’s not necessary to spell out)
- Abbreviations are NOT followed by a period (G.W.A.C.)
- On GSA websites, refer to General Services Administration as GSA
- Avoid using GSA as part of a program name unless it is part of the official program title (e.g., GSA Advantage!)

### Refer to GSA property as GSA-managed, GSA-leased or GSA-owned - 
- Do not use “GSA-controlled”  

### Number lists
- Write numbered lists as follows:	
	- 1. First item
	- 2. Second item
	- 3. Third item
- Do not write numbers using parentheses or extra periods such as 1) or 1.).

### Italics
- Different web browsers can make italics difficult to read on a computer screen and should be avoided in general text
- Use italics in the titles of books, films, plays, long poems, periodicals including newspapers, magazines and journals, works of art, and expressions  
- Italics may also be used when writing letters, words, and terms when they refer to the letter, word, or term itself, (e.g., an “em” dash is the width of the letter m)

### Hyperlinks
- Links are automatically underlined and colored blue and NO text anywhere on a site page other than links should be underlined
- The “link label” should be long enough to understand but short enough to minimize wrapping
- “Click Here” is not necessary
- Avoid wrapping text
- Place links at the end of paragraphs to improve scannability
- Use pointers (i.e. a link to an extended biography from a brief message could be written as follows: More about James Smith>)

### Documents for Download
- The text of the title of the document should be linked to the file, followed by information about the file type and size (i.e. For more information, consult the Project X Guidelines [DOCX1.2MB])

### Page Titles
- Limited to 256 characters, including spaces 
- Capitalization: use title case – initial capital for the first word of the title and for all other words of four or more letters (e.g., “The Lions and the Tigers”)
- Do not use an ampersand as a replacement for “and” unless it is part of an organization’s formal name

### Navigation Titles
- Limited to 40 characters
- Ampersands may be used
