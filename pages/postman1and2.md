---
title: Installing Postman collection for AIQ SOAP API Version 1.1 
layout: default
permalink: postman-collection.html
category: Developing
---
# Installing the AIQ Postman Collection

## AIQ SOAP API Version 1.1 

1. To request a Postman collection to this API, please email [integration@accountsiq.com](mailto:integration@accountsiq.com) and provide the location the AIQ deployment is on and the Provider you are requesting to connect with via the API. 
2. You will need a:
- **PartnerKey:** Provided from onboarding or support. 
- **UserKey:** Generated within the AIQ deployment – See the Integration section in this [How To Video](https://www.youtube.com/watch?v=L03AUQEMuZU).
- **Entity** to connect get data from. 
3. Make sure you have the correct Postman Collection file based on you AIQ Deployment location:
- **Europe 1:** [AccountsIQ-EU1-1_1.postman_collection.json](assets\postman-collection\AccountsIQ-EU1-1_1.postman_collection.json)
- **Europe 2:** [AccountsIQ-EU2-1_1.postman_collection.json](assets\postman-collection\AccountsIQ-EU2-1_1.postman_collection.json)
- **United Kingdom:** [AccountsIQ-UK1-1_1.postman_collection.json](assets\postman-collection\AccountsIQ-UK1-1_1.postman_collection.json)
- **United States:** [AccountsIQ-US1-1_1.postman_collection.json](assets\postman-collection\AccountsIQ-US1-1_1.postman_collection.json)
1. Click the **Import** button and locate the collection file. ![postman10](assets\images\postman10.png)
2. Drag and drop or select the file. ![postman11](assets\images\postman11.png)
3. Click on the collection to open it. ![postman12](assets\images\postman12.png)
4. In the **Current Value** fields, set your Company Id, PartnerKey and UserKey. Leave the remaining variables unedited: ![postman13](assets\images\postman13.png)
- Company Id -> coID 
- Partner Key -> partnerKey 
- UserKey -> userKey 
1. Save the variables. ![postman14](assets\images\postman14.png)
2. Search and Open the Login Method and send the request. This will get a token and set it to memory.
3.  Now call any method. The token is automatically added to the call. 
4.  Once the token expires, call the Login Method again. 

### See More:
- [Authentication 1.1](authentication1.html)

## AIQ SOAP API Version 2.0 

1. To request a Postman collection to this API, please email [integration@accountsiq.com](mailto:integration@accountsiq.com) and provide the location the AIQ deployment is on and the Provider you are requesting to connect with via the API. 
 2. You will need:
- The Developer Portal. See: [How to create an Integration Application](https://aiq.helpjuice.com/en_GB/manage-integrations/2079829-integrations-application-and-invite) 
- An integration application to access via a Client Id and Secret. See: [Using the developer portal](https://aiq.helpjuice.com/en_GB/manage-integrations/using-the-developer-portal-and-new-api-endpoint) 
3. Make sure you have the correct file based on you AIQ Deployment location:
- **Europe 1:** [AccountsIQ-EU1-2_0.postman_collection.json](assets\postman-collection\AccountsIQ-EU1-2_0.postman_collection.json)
- **Europe 2:** [AccountsIQ-EU2-2_0.postman_collection.json](assets\postman-collection\AccountsIQ-EU2-2_0.postman_collection.json)
- **United Kingdom:** [AccountsIQ-UK1-2_0.postman_collection.json](assets\postman-collection\AccountsIQ-UK1-2_0.postman_collection.json)
- **United States:**  [AccountsIQ-US1-2_0.postman_collection.json](assets\postman-collection\AccountsIQ-US1-2_0.postman_collection.json)
4. Click the **Import** button and locate the collection file. ![postman10](assets\images\postman10.png)
5. Drag and drop or select the file. ![postman11](assets\images\postman11.png)
6. Click on the collection to open it. ![postman15](assets\images\postman15.png)
7. In the **Current Value** fields, set your Entity, Client ID and Secret. Leave the remaining variables unedited: ![postman17](assets\images\postman17.png)
- Entity  -> aiq_client_id 
- Client ID -> aiq_client_secret 
- Secret -> aiq_client_secret 
8. Save the variables. ![postman14](assets\images\postman14.png)
9. Search and Open the `TokenGet` Method  and send the request. This will get a token and set it to memory as well as a Refresh token.
10.  Now call any method. The token is automatically added to the call. 
11.  Once the token expires, call `TokenRefresh` to get a new set of tokens. 

### See More:
- [Authentication 2.0](authentication2.html)