---
title: Data Types
layout: default
permalink: pages/datatypes/
category: Overview
---
# Most popular API Methods

The following is a rundown of some of the most popular methods our integrators employ. 

## Customer and Supplier Data
The AIQ API can retrieve and create essential customer and supplier data. 

Use the `GetCustomer` or `GetSupplier` method to:
-	Verify that the customer/supplier code on a sales transaction exists in AccountsIQ.
-	Set customer/supplier defaults such as tax codes when creating or importing transactions.
-	Get the customer/supplier account ID to use it in other API calls.

The AIQ API can also help create customer accounts during implementation or updating of the AIQ system. 

Use the `UpdateCustomer` method to:
-	Create customers based on a client’s source data automatically.
-	Perform part of an initial batch import from a previous system.

## Batch Invoice Data
We tailor AIQ API integrations to meet our customer’s needs. For many integrations, this means creating batch sales invoices and sales receipts, and then allocating them using separate API methods, one transaction at a time, using methods such as the following:

-	`CreateBatchSalesInvoiceGetBackTransactionID`
-	`CreateBatchPurchasesInvoiceGetBackTransactionID`
-	`GetNewSalesInvoice `
-	`GetNewPurchasesInvoice`

In other cases, `PostPayAndAllocateSalesInvoices` creates all these operations with one API method for dozens of bulk transactions. This API call can be used when importing a higher volume of transactions as it avoids time-out issues during uploads.

## Reference Data
When loading transactions, the `GetTransactionsByExternalReference` method ensures that the same data has not been loaded twice by ensuring that the transaction does not already exist in the system. This can happen when a client mistakenly uploads the same file again. 

### See More:
- [About our API](/index/)
- [Key Advantages of APIs](/pages/advantages/)
- [Integrate with AIQ](/pages/integration/)
- [Business Use Cases](/pages/usecases/)