---
title: Guidelines
layout: default
permalink: pages/guidelines/
category: Developing
---
# Development Guidelines

## Sandbox
Before you begin developing with AIQ API, you need access to the following: 
- **A sandbox:** This can either be a blank demo company or a copy of a live entity. You need explicit permission from the customer for the latter option.
- **Credentials:** This consist of two tokens. AIQ provides a partner token. A user generates a user token within the live company which developers can use to impersonate them.

## Client Libraries
Currently, we do not offer client libraries. We can, however, make available a Postman collection with sample requests. We also have a sample C# project that we can provide on request.

## Sample API Requests 
View a library of XML samples of API requests and responses: [Integration_1_1 Web Service](https://uk1.accountsiq.com/system/dashboard/integration/integration_1_1.asmx).

## PHP Proxies
PHP may require more work to generate a proxy to connect to the API. 

The simplest way to integrate using PHP is to:
1.	First, generate a set of proxy classes from our WSDL using a tool such as wsdl2php. 
2.	Next, you should be able to generate a set of classes by pointing it to the Staging Environment.
3.	Finally, require_once the generated include PHP files and follow the C# examples.

If you require further assistance, please send a mail to [integration@accountsiq.com ](mailto:integration@accountsiq.com).

## Clearing Testing Data
If you have created testing data in the system and want to clear it for retesting, email integration@accountsiq.com specifying what you want done to which company.

## Going Live
If you have finished developing the integration link and want to go live:
1.	Email [integration@accountsiq.com ](mailto:integration@accountsiq.com) requesting a live production partner key.
2.	If you are in a staging environment: 
- Switch your web reference to the live production web service URL. Your users will then need to provide you or your software with their user integration key.
If you are not in a staging environment:
- Allow for the user to select the correct region and change the endpoint URL accordingly.

### See More:
- [Specifications](/pages/specifications/)
- [Authentication](/pages/authentication/)
- [Troubleshooting](/pages/troubleshooting/)