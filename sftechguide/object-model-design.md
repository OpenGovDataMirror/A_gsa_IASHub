---
title: Object Model Design
keywords: mydoc
sidebar: sftechguide_sidebar
toc: true
permalink: /sf-tech-guide/object-model-design/
---


The application development team must consider the following design principles during the Object Model Design process:

Reference:

- [Information on Object Relationships](http://www.salesforce.com/us/developer/docs/api/Content/relationships_among_objects.htm)
- [Information on Entity Relationship Diagrams for Standard Salesforce.com Objects](http://www.salesforce.com/us/developer/docs/api/Content/data_model.htm)
- [Information on Standard Salesforce.com Object Details](http://www.salesforce.com/us/developer/docs/api/Content/sforce_api_objects_list.htm)

Guideline:

- Keep it simple –
  - Keep the object model as simple as possible and avoid creating junction objects unless absolutely necessary.
  - Rationalize fields and keep layouts simple and clean to improve usability.
  - Avoid free text fields when possible to improve data hygiene and report-ability.
- Standard vs custom objects –
  - Use of Standard Objects versus Custom Objects should be decided based on functional requirements, number of users and out-of-the-box (OOTB) features/functions available for use on Salesforce/force.com.  License cost is also a consideration for using OOTB objects.
  - Where multiple similar data elements (ex. date 1, date 2, name 1, name 2) are necessary, a custom object should be considered for reporting and scalability purposes.  For example, to capture multiple team resources, create a custom object with member and role fields vs. multiple member fields labeled with each role.
- Scalable design –
  - Ensure that designed solutions are scalable and that custom development is only used on an as-needed basis (per use case).
- Custom report testing –
  - Relevant Custom Reports should be tested immediately after changing the relationship type between any two objects.

## hello2

Requirement:

- Entity Relationship Diagram (ERD)
  - Each application shall maintain an ERD (within the Technical Design Document) that shows relationships across all objects used in this application.  This ERD shall be updated for each Release as applicable.  ERD diagrams shall specify primary and foreign keys as well as nature of relationship between objects (ex. 1 to many, many to many).

The below sections speak to the guidelines for Development and Configuration within Salesforce.com.


# hello1

### hello3