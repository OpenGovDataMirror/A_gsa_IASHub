---
title: Technical Change Management
keywords: mydoc
sidebar: sftechguide_sidebar
toc: true
permalink: /sf-tech-guide/technical-change-management/
---
In enterprise system architecture with multiple production and sandbox organizations, code and configuration changes can occur at the same time in different environments. Tracking changes sounds simple in concept, but can become challenging due to the fast development life cycle afforded by the simple-to-use Salesforce.com and Force.com development tools.  

## Reference
* N/A

## Guideline
* Manually track changes, and then define a proper Deployment Plan to ensure that only the appropriate changes are deployed to production without overwriting functionality already in use.  This is because while the development team can use an application development tool, such as the Force.com IDE, to track and version changes, there are other user interface or configuration components that are not available in the Metadata API.  

## Requirement
* Maintain compliance with defined change control processes so only validated and approved changes are migrated to the correct environment at the right time.Distribute Click Path / Release Notes for each Deployment
	* The Click Path document may serve as Release Notes for an application’s initial release.
	* The Click Path document must be updated to reflect changes, additions, or removals of major functions.
	* Release Notes for subsequent releases must be embedded within the Revision History of the updated Click Path document.
* Comments required
	* Any changes made to code must be commented to indicate the developer name, time stamp and ticket/requirement information.
