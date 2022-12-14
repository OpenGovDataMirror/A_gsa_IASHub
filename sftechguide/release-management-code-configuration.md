---
title: Release Management - Code & Configuration
keywords: mydoc
sidebar: sftechguide_sidebar
toc: true
permalink: /sf-tech-guide/release-management-code-configuration/
---
The Salesforce Program involves multiple projects and teams that require their own isolated space for development, testing, or training at the same time.  The GSA Salesforce Solution Architects have defined a clear organizational system architecture to ensure clean migration paths, avoid confusion, and to keep the environments current and relevant.  

## Reference
* Below is a snapshot of the application Salesforce sandbox promotion path:

 
Figure 2 - GSA Salesforce Sandbox App Promotion Path

The above process and environment configuration provides the ability to conduct iterative development and testing while maintaining a production-like environment for testing complex defects and deployment dry-runs (Staging).  Maintaining a Production-like environment is crucial to minimizing the disruption to a current iteration/release, and allowing immediate and effective resolution to critical Production defects.

## Guideline
* All changes migrated into production should be merged into lower environments where a sandbox refresh is not possible.  
* It is acceptable to perform User Acceptance Testing (UAT) on a Dev sandbox and then promote to Integration.
	* For cases where user acceptance requires real data, the Integration box can serve that function.
	* It is also possible for larger projects to use a Dev sandbox to integrate code prior to promoting to the Integration box.

## Requirement
* All Setup/Auditable changes must go from a lower environment into production; written justification is required from the Org owner to make changes directly in production.  
	* This includes changes to profile or permission sets.
* Smaller, less complex deployments may not necessarily need to go through Staging.
	* Solution Architects make the determination during Design as to whether Staging deployment is required.  If no specific determination is made during the Design phase, then the assumption should be that Staging deployment is required.
	* If Staging deployment is determined by the Solution Architects to not be required, the Release Manager or Deployment Admin may determine it is necessary regardless.