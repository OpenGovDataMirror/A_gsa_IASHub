---
title: Deployment Plan
keywords: mydoc
sidebar: sftechguide_sidebar
toc: true
permalink: /sf-tech-guide/deployment-plan/
---

## Reference
* Deployment Plan Template - http://goo.gl/rvWchv
* One major production release is planned at the end of each calendar month. The actual release date is adjusted to fall on a Friday, in order to minimize impact to Production users.
	* Fast Track releases are possible though justification is required.

## Guideline
* For particularly complex deployments or in cases where there is likely to be misunderstandings between the Developer and Deployment Admin, the two parties should meet in advance of deployment to walk through the plan step by step.
* Deployments from sandbox to sandbox should mirror the sandbox to production deployment.  In complex deployments involving many components, particularly destructive changes, it is imperative not to perform a deployment step for the first time in production.
* All apex unit tests should have been run during the deployment into the target sandbox.  Any unit test failures should roll back the deployment to simulate a production roll out.
* Use of Screenshots in Deployment Plan:
	* Simple single parameter changes generally do not require a screenshot.
	* Manual changes to multiple settings for existing objects generally necessitate screenshots.
	* Screenshots are not required to indicate navigation through Salesforce.
	* Screenshots are not required for components that are automatically deployed through Change Sets or Eclipse.
	* Screenshots are required to show Data Wizard field mapping.
	* Where possible, screenshots should be targeted to the area of the screen with the setting or settings to verify (not a shot of the entire window).
	* If the Release Manager or Deployment Admin are not comfortable with a step or would like clarification, they may request additional screenshots for specific steps during their review period (prior to Go Live, assuming the plan was submitted by the Developer on time).
	* All other screenshot-related issues will be handled via a combination of common sense and collaborative negotiation.
* While Force.com IDE is an acceptable deployment method, the Admin Team’s preferred method for deployment is Change Sets. All Project Teams should use this method when requesting application deployments to an upper environment (Integration, Staging, and Production).  Where possible, Change Sets should be promoted vs. recreated.
* Each team should take part in a combined Integration Test, to validate their code as part of the overall Release and Deployment Plan.
* Deployment Plans should be submitted 5 business days in advance of the monthly Go Live Review date (typically the 3rd Wednesday of the month) in order to ensure review and approval by the Release Manager.

## Requirement
* Development Teams must use the Deployment Plan Template in the Reference Link at the top of this section.
* Each Development Team will have the ability to move code into their defined Sandboxes, but only the Org’s Admin Team will have the ability to deploy code to Integration, Staging, and Production.
* When a first-time Developer or Release Manager is involved in the process, the Release Manager & Deployment Admin must meet with the Developer (pre-Deployment) to walk through the Deployment Plan step by step to ensure understanding.
* Deployment Plans must use one of the following deployment methods:
	* Force.com IDE (aka Eclipse): Salesforce provides the use of metadata API for code and configuration migration.  Code and configuration changes can be downloaded into text-based metadata files, and then deployed to another environment using an automated tool such as Force.com IDE, a tool based on the Eclipse platform for development and deployment.  Using Force.com IDE for deployment requires that the user use the Force.com IDE application and to have the “Modify All Data” permission.  This method is best suited for a more technical audience.  Few users should be granted such access because this method will allow the user to change every aspect of customization in an organization.
	* Change Sets: Salesforce provides a user interface-based migration tool called “change sets” that can be used by non-technical resources to migrate changes from one organization to another.  Change sets can be used between sandbox organizations, or between a sandbox and production organization.  Change sets can only contain customizations that can be made directly through the Setup menu; some specific Setup customization cannot be migrated using change sets.
	* Manual: The other alternative method for migrating changes is through direct manual replication of customization in the environment.  For example, if a change in profile needs to be migrated to a different environment, the user can manually perform this change in the target environment.  This is a fully manual and time-consuming process.  It is prone to user error if the changes are extensive.  This is not a recommended method for migration.

