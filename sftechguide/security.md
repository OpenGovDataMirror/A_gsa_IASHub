---
title: Security
keywords: mydoc
sidebar: sftechguide_sidebar
toc: true
permalink: /sf-tech-guide/security/
---

All Salesforce and Force.com applications must go through security review and approval by the Information System Security Officer (ISSO). The ISSO will work with the project team and IT Governance to assess security impact and ensure that the application meets all security controls and compliances defined by the Office of the Chief Information Security Officer (OCISO).

## Reference

* Salesforce Security Implementation Procedural Guide 11-62

## Guideline

* Concept/Planning Phase –
	* The Project Team should involve the ISSO in the project kick-off meeting. 
	* The ISSO should meet with App Owners (new App Owners especially) to review the security process, outlined below, to ensure that Project Team and Business Line stakeholders understand the process and expectations. 
	* Every project is different and the ISSO will determine if more or less data points are needed.
* Design Phase – 
	* Inform the ISSO early on if the design of an application may include: 
		* Access to or storage of PII
		* Exposure of datasets outside of GSA
		* Any new methods for controlling access to data
		* Integrations 
		* Use of service accounts or personas
		* Employment of AppExchange products
		* Creation of new Profiles.  
		* Use of OOTB Salesforce capabilities that have not previously been utilized
		* Alternative language coding (excludes Apex and Visualforce)
* Development Phase – 
	* Developers should conduct regular scans using the GSA internal Checkmarx tool and resolve issues as they arise.

## Requirement
 
* All project teams must comply with requirements laid out in the Salesforce Security Implementation Procedural Guide 11-62, including the embedded document entitled “GSA’s Implementation of Security for Salesforce Minor Applications”.
* All Salesforce Orgs must be configured in accordance with Salesforce Security Implementation Procedural Guide 11-62, to include policies on Single Sign-On, session time-outs, etc.  
	* Please note that one of the security requirements for all GSA Orgs is to enable the “Lock sessions to the IP address from which they originated” checkbox. This has been known to cause issues with certain AppExchange products.
* All Checkmarx Security vulnerabilities must be mitigated before deploying to Integration, Staging, or Production environments.
* An application may not be deployed to Production until the Security Package has been signed by the appropriate Information Systems Security Manager (ISSM).
* Users may not be added to an application until the Security Package has been signed by a representative of the Office of the Chief Information Security Officer (OCISO).
* Checkmarx security scan results may be sent as email attachments within the gsa.gov email domain.  These results must be encrypted if attached to an email that travels outside of the gsa.gov domain, with the password to decrypt sent via a separate email.  For more information see: Appendix: Encryption Policy for Checkmarx Security Scans.
