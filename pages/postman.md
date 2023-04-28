---
title: Postman Collection
layout: default
permalink: postman-collection.html
category: Developing
---

# Using the Postman Collection

On request, AIQ offers a postman collection with sample requests.

## Step One: Set up JSON File
1.	In Postman open or create your preferred Workspace.
2.	Click **Import**: ![postman1](assets\images\postman1.png)
3.	Upload the Postman collection JSON file (AccountsIQ SOAP API.postman_collection.json).
4.	The following details should be presented: ![postman2](assets\images\postman2.png)
5.	Click **Import**.
6.	Go to the **Collections tab** on the left-hand side and open the newly imported collection **AccountsIQ SOAP API**: ![postman3](assets\images\postman3.png)
7.	In the **Variables** tab change the **Current Value** of the two available variables to your AccountsIQ URL: ![postman4](assets\images\postman4.png)  

    If you are not sure what URL to connect to, visit your AccountsIQ login page and take note of the URL in the address bar: ![postman5](assets\images\postman5.png)

## Step Two: Set up Environment File
1.	Click **Import**: ![postman6](assets\images\postman6.png)
2.	Upload the Environment file (Company Environment.postman_environment.json)
3.	At the top-right hand corner, in the dropdown change **No Environment** to **Company Environment**.  
4.	Click the eye icon and select **Edit** to edit the newly imported company environment: ![postman7](assets\images\postman7.png)
5.	Set the three variables as follows:
- CoID: The company ID provided by AccountsIQ.
- partnerKey: Provided by AccountsIQ.
- userKey: Generated from within AccountsIQ by going to **Setup** > **Company Details & Settings** > **Integration** tab, entering the user’s password and clicking **Request User Key**.

## Step Three: Send Login request
1.	Select the `Login` request and go to the **Tests** tab. The tab should contain the code below. This code ensures that running the Login method populates the `aiqToken` variable used by all other requests.

    ```
    const response = xml2Json(responseBody);
    const token = response["soap:Envelope"]["soap:Body"]["LoginResponse"]["LoginResult"];

    pm.environment.set("aiqToken", token);
    ```

2.	Click **Send**. In the results body, you should see an XML response that contains a non-blank `<LoginResult>` tag. If the result does not contain a newly generated token, one of the three variables from step two is incorrect and needs to be corrected.


    Any other request within the collection can now be performed for the next 20 minutes, until the login token expires, and the Login request needs to be re-run. When the token reaches its expiry time, the result of any other API call will contain the value `<HasExpired>true</HasExpired>` within the response body.

## Step Four: Send Further Requests
1.	Select the request you wish to send (for example, `GetCustomerList`) which has the method ‘POST’ beside it (not the example request!! which has ‘e.g.’ in front of it): ![postman8](assets\images\postman8.png)
2.	Open the Body of the request to edit the request parameters: ![postman9](assets\images\postman9.png)
- Never remove the `<token>{{aiqToken}}</token>` parameter as this is used to authenticate each request.
- Any unused optional parameters should be removed rather than left blank.
- Each endpoint has an example (marked with 'e.g.') which can be used find all available parameters for a given request.
