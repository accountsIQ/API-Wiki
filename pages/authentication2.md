---
title: Authentication 2.0
layout: default
permalink: authentication2.html
category: Developing
---

# Authentication 2.0

## Login Requirements WSDL 2.0

The newest version of our API, comes with a new endpoint, and a simplified login experience with OAuth 2.0 authentication.

Our API management has also been streamlined. Within our system, customer administrators can create and manage integration applications and invite developers to the new Developer Portal. None of this requires AIQ or developer assistance. In the Developer Portal, developers can manage their APIs.

To learn more, including migrating from our older endpoints, see the links below.

>AIQ Help
>
>- [Integration Application and Invite](https://aiq.helpjuice.com/en_GB/manage-integrations/2079829-integrations-application-and-invite)
>- [Manage Integrations Using the Developer Portal and New API Endpoint](https://aiq.helpjuice.com/en_GB/manage-integrations/using-the-developer-portal-and-new-api-endpoint)

## Version 2.0 Examples

To get authenticated you will need a Client Id and Client Secret.

### Getting the Token - C#
```
Integration_2_0 ws = new Integration_2_0();
var token = ws.TokenGet(<clientId>, <clientSecret>);

 if (tokenGetResponse != null && tokenGetResponse.Result != null)
 {
     this.AccessToken = tokenGetResponse.Result.AccessToken;
     this.RefreshToken = tokenGetResponse.Result.RefreshToken;
 }
 else
 {
     throw new Exception("TokenGet Failed! Could not get an Access Token");
 }
```
### Using the Token - C#
Before you can call a method, you need to set the Token and the Entity ID in the header.
```
// Set the header to take the token and the entity ID
ws.AiqSoapHeaderValue = new AiqSoapHeader { AccessToken = this.AccessToken, Entity = this.CompanyID };

// Note each method in Version 2.0 has a token as its first parameter. This is here for compatibility and should be left blank, as the token is already set in the header
var result = ws.GetCurrencies(string.Empty);
```
### Refreshing the Token -  C#
When you token expires, you will need to refresh it by calling TokenRefresh.
```
...
ws.TokenRefresh(clientId, clientSecret, this.RefreshToken);

 if (tokenRefreshResponse != null && tokenRefreshResponse.Result != null)
 {
     this.AccessToken = tokenRefreshResponse.Result.AccessToken;
     this.RefreshToken = tokenRefreshResponse.Result.RefreshToken;
 }
 else
 {
     throw new Exception("TokenRefresh Failed!");
 }
 ```