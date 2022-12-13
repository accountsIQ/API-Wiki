---
title: Troubleshooting
layout: default
permalink: /pages/troubleshooting/
category: Developing
---

# Troubleshooting 

## Login Errors

Uncaught SoapFault exception: 

`[WSDL] SOAP-ERROR: Parsing WSDL: Couldn't load from ....`

This is likely due to misconfiguring the request. 

The following sample shows how to configure your login request:

### Code Sample: PHP
```
<?php

$wsdlUrl = "https://hostacct.com/system/dashboard/integration/integration_1_1.asmx?wsdl";

$opts = array(
		'ssl' => array( 
			'verify_peer'=>true, 
			'verify_peer_name'=>true,
			'crypto_method' => STREAM_CRYPTO_METHOD_TLS_CLIENT)
);

$params = array(
                'soap_version'=>SOAP_1_1,
                'exceptions'=>true,
                'trace'=>0,
                'cache_wsdl'=>WSDL_CACHE_NONE,
                'stream_context' => stream_context_create($opts)
        );

$client = new SoapClient($wsdlUrl, $params);

$vars = array(
			'companyID'=>'YOUR_COMPANY_ID',
			'partnerKey'=>'YOUR_PARTNER_KEY',
			'userKey'=>'YOUR_USER_KEY');
			
$result = $client->Login($vars);

echo $result->LoginResult

?>
```
The LoginResult is your authentication token to be used in all subsequent API calls.


## Sales Receipt Errors
If you receive an error message, check that you have included the following mandatory variables:
- `BankAccountCode` 
- `CheckReference `
- `CustomerCode` 

## Sales Order Errors
If you receive an error message, check that the following are correct:
-	`Author User ID` should be null. 
-	`Creation Date` should be null. 
-	`CurrencyCode` is mandatory.
-	`Hold` should be 0.
-	`OrderDate` is mandatory.
-	`OrderID` should be blank.
-	"N/A" is not a recognised value. Use null (xsi:nil="true") instead. 
-	`QuoteID` should be null. Do not specify a row version number.
-	`Status` should be null.

In each line:
-	`CreationDate` should be null. Do not specify a row version number. 
-	`OpeningStockGLAccountCode` is mandatory.
-	`OrderItemIDshould` be 0.
-	`QuoteItemID` should be null.

## Bulk Processing Speed
**Issue:** I need to create, populate, and post thousands of invoices. How can I speed up the process? 

**Solution:** 
Use bulk methods instead of single methods. Similar operations exist for purchases. 
The bulk methods can support thousands of records a second. You can identify the bulk methods by their plural names:
-	Use `GetNewSalesInvoices` instead of `GetNewSalesInvoice` 
-	Use `PostInvoicesGetBackTransactionIDs` instead of `PostInvoiceGetBackTransactionID` 

## Creating a Customer Account
**Issue:** The customer I am trying to create is not saving.

**Solution:**
There can be multiple reasons for this. Check the following:
-	The customer code is specified.
-	The customer code is upper case.
-	The BankCode  exists in the system (The `BankCode` is the General Ledger code representing the bank in the system whereas the `BankAccountCode` is the physical bank account number in the bank branch).
-	The referral ID is not specified through the API. It must be left blank/null.

### Code Sample: C#
```
      private void CreateNewCustomer()
      {
	      Integration_1_1.Integration_1_1 ws = new Integration_1_1.Integration_1_1();
	      String auth = ws.Login(companyID, partnerKey, userKey);

	      if (auth != null)
	      {
		      Integration_1_1.Customer customer = new Integration_1_1.Customer();

		      customer.Name = "ABC Account 01";
		      customer.Address1 = "this is my address 1";
		      customer.Address2 = "this is my address 2";
		      customer.City = "this is my city";
		      customer.County_State = "this is my county";
		      customer.Country = "this is my country";
		      customer.PostCode = "this is my postcode";
		      customer.Contact = "Contact";
		      customer.Email = "abc@02.com";
		      customer.Fax = "0123459";
		      customer.Phone = "0123457";

		      // This will not work because the account code was not set, and the system does not generate them
		      // dynamically
		      Integration_1_1.WSResult2OfBoolean result = ws.UpdateCustomer(auth, customer, true);
		      Assert.IsNotNull(result);
		      Assert.AreEqual(true, result.Result);
	      }
      }
```

## Populating Customer Record Fields
**Issue:** I want to create a new customer but I don’t know how to populate all fields in the customer record.

**Solution:** Use the `GetNewCustomerFromDefaults` method. This returns the shell of a customer pre-populated with all the default values. This is a useful method for creating a test customer.
 
## Creating a New Order/Invoice

**Issue:** I created a new order/invoice. I then retrieved it to check it was saved and updated it again, but this failed.

**Solution:** Send back the modified values in the retrieved order/invoice not the original. Otherwise, the values set during saving, such as `RowVersionNumber`, will not match.

## Getting a Due Date for an Invoice

First, using the `GetSupplier` or `GetCustomer` method, interrogate the supplier or customer and find the `CreditTermID`.

### JSON Sample
```
"CreditTermID": "1": This needs to be matched to the output (an array of credit terms) from GetCreditTermList.

            {
                "Code": "1",
                "Description": "30 Days",
                "RowVersionNumber": "etHg5LRlYP4+UwTlPmufOSyLPWX/PSJckYmL/Pcqo8lGPpiBm6bYB08CiezrssIu",
                "CreditDays": 30,
                "EndOfMonth": false,
                "Checker": {
                    "IdLength": 50,
                    "CodeLength": 50,
                    "DescriptionLength": 200,
                    "AuthorLength": 200,
                    "CreditDayLength": 255
                }
            }
```

In this where the Code matches the supplier/customers `CreditTermID` you have two key pieces of information:
-	the number of days (`CreditDays`)
-	whether `EndOfMonth` is set to true or false. If false then it is invoice date plus the no of days, but if `EndOfMonth` is true that is then set from the last day of the month in which the invoice date falls.

### See More:
- [Specifications](/pages/specifications/)
- [Guidelines](/pages/guidelines/)
- [Authentication](/pages/authentication/)
