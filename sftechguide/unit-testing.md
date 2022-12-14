---
title: Unit Testing
keywords: mydoc
sidebar: sftechguide_sidebar
toc: true
permalink: /sf-tech-guide/unit-testing/
---

This section provides best practices on unit testing so developers can produce effective code efficiently without extensive rework.  

## Reference
* Apex Test Coverage Best Practices:
http://developer.force.com/df_session?id=a0J300000009wdyEAA

## Guideline 
* Work in small batches - 
	* Unit test should be done at the smallest testable level so each unit of code is tested and validated, before the developer moves on to additional code. 
* Ensure coverage –
	* 100% code test coverage should always be the goal.
	* Test with all profiles and permission sets for a particular app, not just with developer admin rights.
* Test early –
	* Compose unit tests as part of development.  Do not wait until the week of deployment to compose unit tests.  Well written unit tests created during the earliest part of the development lifecycle often help uncover functional or logical gaps.
	* All Unit tests should be run prior to migration from one sandbox to another, not just when deploying to production.  
* Other best practices –
	* Unit tests should always include meaningful assertions to validate the functionality
	* Unit tests should reside in their own apex class to allow for decoupled refactoring
	* Use SeeAllData=true for appropriate use cases (testing for non-selective queries or for opportunities’ standard pricebook) only.    
	* Use Apex WebServiceMock class or HttpCalloutMock to test any webservice or http callouts.  Not using these interfaces risks either not testing the functionality or potentially causing an irretrievable/irrevocable callout to an integrated system.
	* Test negative scenarios to verify that error handling works as expected.
	* Since unit tests run as the logged-in user, make extensive use of system.RunAs to verify that functionality works for users other than IT staff deploying to production.

## Requirement
* Sandbox
	* Conduct unit testing in a development Sandbox.
* Code Test Coverage
	* 90% is the minimum required code coverage for every class promoted to production.  Please note that calls to System.debug are not counted as part of Apex code coverage in unit tests.
	* Extraordinary conditions in which 90% coverage is not achievable shall be considered by the Release Manager and Solution Architect on a case-by-case basis, though it shall be the responsibility of the Developer to ensure that these situations are brought up in advance of production deployment.
	* Code not meeting 90% coverage during production deployment which has not been previously considered runs the risk of being delayed or not deployed.
	