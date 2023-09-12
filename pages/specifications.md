---
title: Specifications
layout: default
permalink: specifications.html
category: Developing
---

# Specifications 

## Languages
AIQ API is language-independent. You can use it with languages such as Java, C#, VB.NET, and PHP. In our documentation, we only provide code examples in C# and VB.NET.

## Protocol
AIQ API uses SOAP 1.1.

## Open API 
AIQ API meets OpenAPI specifications.

## WSDL File 
The WSDL file is the same across all regions, but the endpoint differs by region. 

In the relevant WSDL version, enter the `{regioncode}` found in your client's URL:
- us1
- eu1
- eu2
- uk1

**Version 1.1:** `https://{regioncode}.accountsiq.com/system/dashboard/integration/integration_1_1.asmx?wsdl`

**Version 2.0:** `https://{regioncode}.accountsiq.com/system/dashboard/integration/integration_2_0.asmx?wsdl`

When using the WSDL file, it is recommended to refresh the file. However, as we only make backward compatible changes, this is not mandatory.

### See More:
- [Guidelines](guidelines.html)
- [Authentication](authentication1.html)
- [Authentication](authentication2.html)
- [Troubleshooting](troubleshooting.html)
