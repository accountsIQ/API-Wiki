---
title: Sales Invoicing
layout: default
permalink: sales.html
category: Business Use Cases
---
# Sales Invoicing Integrations

Any business, especially those with high volumes of sales, can benefit from integrating their sales invoicing process. Schedule transactions to flow automatically from your chosen CRM into AIQ, without your sales team ever having to leave their system. 

Entering data in one place, not only prevents time wasting double-entry, it also reduces the risk of data records not being in agreement. In addition, regular syncing schedules can ensure you are always working with the most current data.

## Our Integration Partners
Sales invoicing is the most popular way our integrators use our API. Sales invoicing integrations are often also part of a complete pay-to-purchase routine that includes handling [receipts, allocations, and payments](payment.html). 

The following are some of our partner integrators who use our API for sales invoicing:

- [Arlo](https://www.accountsiq.com/arlo-training-management-system/)
- [Chaser](https://www.accountsiq.com/features/integrations/chaser/)
- [Fourth](https://www.accountsiq.com/features/integrations/fourth/)
- [Fusebill](https://www.accountsiq.com/features/integrations/fusebill/)
- [iCompleat](https://www.accountsiq.com/features/integrations/icompleat/)
- [iSAMS](https://www.accountsiq.com/features/integrations/isams/)
- [Lightyear](https://www.accountsiq.com/features/integrations/lightyear/)
- [Salesforce](https://www.accountsiq.com/features/integrations/salesforce/)

In addition, our development team offer managed integrations. If you would like to explore this customised option further, please get in touch at [sales@accountsIQ.com](mailto:sales@accountsIQ.com) or [support@accountsIQ.com](mailto:support@accountsIQ.com).

## Integration First Steps
Prior to creating invoices, complete the following where necessary.

### Create Customers 
Before you can proceed with invoicing customers, they must be present in the system. You can use the following to add and update customer records.

- [`GetNewCustomerFromDefaults`](https://github.com/accountsIQ/API-Wiki/wiki/GetNewCustomerFromDefaults): This lets you create a new customer using the defaults that already exist in the system. However, the customer is not yet saved.
- [`UpdateCustomer`](https://github.com/accountsIQ/API-Wiki/wiki/UpdateCustomer): Use this to save the customer you just created or updated. 

### Check Customer Credit
It is important to check if your customers have sufficient credit to decide if you want to sell to them.

- [`GetCustomersStatement`](https://github.com/accountsIQ/API-Wiki/wiki/GetCustomersStatement): This lets you see the customer's credit record in your CRM. View payment history, outstanding payments, balances, and any aging. You can use this to decide whether keep this customer. 
- [`GetAccountBalanceInformation`](https://github.com/accountsIQ/API-Wiki/wiki/GetAccountBalanceInformation): Use this if you just want to keep credit limits in sync and don’t need the extra information that `GetCustomerStatement` provides.

### Check if an Invoice already exists 
If you try to create an invoice that already exists you could get an error. 

- [`GetInvoicesByExternalReference`](https://github.com/accountsIQ/API-Wiki/wiki/GetInvoicesByExternalReference): Use this to check if an invoice already exists before creating a new one.
  
It is best practice to use external references where possible as they track transactions and help avoid duplication. An external reference can be named the same as in the other system, meaning that the transaction can be tracked easily in both systems. 

## Standard Invoicing 
Once you have completed the preliminaries, you are now ready to invoice your customers.

### Best Practice: Use Transaction IDs
Use endpoints that return transaction IDs where possible. Recording the transaction ID in the third-party system creates another level of traceability in your CRM, along with the corresponding external reference. These can be matched for validation. 

Once the transaction ID is recorded in the third-party system, you cannot modify that invoice, or the systems will be out of sync.

### Batch Invoices
Batch invoices go straight to the transaction tables rather than going to the invoice table first, making them slightly faster than item invoices. 

> AIQ Help:
> 
> - [How does Batch Sales Invoicing work?](https://aiq.helpjuice.com/sales-system/283452-how-does-batch-invoicing-work?from_search=116655046)

Batch invoicing is recommended if you follow VAT calculations from another system, as it avoids the slight rounding that can occur with item invoices.

- [`GetNewBatchSalesInvoice`](https://github.com/accountsIQ/API-Wiki/wiki/GetNewBatchSalesInvoice):  This creates a new unposted batch invoice with the customer’s defaults. You cannot edit batch invoices. 
- [`CreateBatchSalesInvoiceGetBackTransactionID`](https://github.com/accountsIQ/API-Wiki/wiki/CreateBatchSalesInvoiceGetBackTransactionID): After creating a batch, use this to post it. 
  
### Item Invoices
Use item invoicing if you need extra header details, such as order numbers, delivery dates, line notes, or item codes. Item codes can be useful as they let you store defaults against them.

>AIQ Help:
>
>- [Sales Item Invoices](https://aiq.helpjuice.com/sales-system/642689-sales-item-invoices-credit-note?from_search=116660221)

- [`GetNewSalesInvoice`](https://github.com/accountsIQ/API-Wiki/wiki/GetNewSalesInvoice): The first gives you with a new template invoice with the defaults of the customer code you provided. You can then modify data and create invoice lines. 
- [`SaveInvoiceGetBackInvoiceID`](https://github.com/accountsIQ/API-Wiki/wiki/SaveInvoiceGetBackInvoiceID): This saves the invoice and returns the transaction ID. However, it has not been posted yet.
- [`PostInvoiceGetBackTransactionID`](https://github.com/accountsIQ/API-Wiki/wiki/PostInvoiceGetBackTransactionID): Use this to post the transaction you created.

### Customised Invoices and Statements
With the API, you can attach a detailed invoice breakdown for the customer in CSV or Excel format. This is useful if you are invoicing a customer for multiple jobs but still want a summarised invoice. You can then send on the invoice and attachment to the customer.

- [`AttachDocument`](https://github.com/accountsIQ/API-Wiki/wiki/AttachDocument): When you create an invoice, use this to attach an Excel or CSV file. 
- [`GetInvoicePDFByTransactionID`](https://github.com/accountsIQ/API-Wiki/wiki/GetInvoicePDFByTransactionID): This lets you retrieve a PDF of the invoice. If you have an emailing facility in your CRM, you could opt to email it via that option. 

## Back-to-Back Invoicing 
Back-to-back invoicing refers to a situation where a purchase and sales invoice are raised at the same time. 

For example, an employment agency could raise:

- a purchase order to pay a contract for labour.
- a sales invoice with a percentage markup to bill the customer. 

### Use BI Codes
If your invoicing requires complex transactions, BI codes (called Departments in the API) can help manage this process. Setting up and managing complex BI structures via the API is much more manageable than doing it manually. 

> AIQ Help:
> 
> - [How do I Implement Extended Business Analysis?](https://aiq.helpjuice.com/en_GB/analysis/289280-how-do-i-implement-extended-business-analysis)
> - [Extended Business Analysis for Job or Project Analysis](https://aiq.helpjuice.com/en_GB/analysis/289415-how-do-i-implement-job-or-project-analysis-using-extended-business-analysis)

BI Codes can have up to six BI dimensions, each with as many elements as needed. They can be based on data from the customer, item code, a third-party system, or a combination.  

BI Codes are linked to transaction lines which in turn link them to dimensions and analysis codes via the BI Setup. This underpins all advanced reporting in the system.

If a third-party system doesn’t have a GL code to post from, use non-stock items to set default BI and GL codes, even if you don’t use them on the invoice.

- [`GetAnalysisDimensionSetup`](https://github.com/accountsIQ/API-Wiki/wiki/GetAnalysisDimensionSetup): This returns the analysis setup.
- [`GetDepartmentById`](https://github.com/accountsIQ/API-Wiki/wiki/GetDepartmentById): This lets you search by BI Code.
- [`GetDepartmentList`](https://github.com/accountsIQ/API-Wiki/wiki/GetDepartmentList): This returns available BI Codes, both active and inactive.
- [`GetDepartmentsByAnalysisCode`](https://github.com/accountsIQ/API-Wiki/wiki/GetDepartmentsByAnalysisCode):This lets you search by dimension.
- [`UpdateDepartment`](https://github.com/accountsIQ/API-Wiki/wiki/UpdateDepartment): This modifies the description and active status of a Department. Use this when you wish to retire a code or update its description.

## Deferred Revenue
Deferred revenue refers to when a company bills a customer in full but wants to record the revenue over multiple periods. When the company receives the revenue in one go, they can split it into twelve parts to account for it being earned over the course of the year.

>AIQ Help:
>
>- [General Ledger Deferred Revenue Postings and Spreadings](https://aiq.helpjuice.com/general-ledger/335271-general-ledger-deferred-revue-postings?from_search=116655309)

### Use a Deferred Revenue Journal
Deferred revenue can be accounted for with a deferred revenue journal. 

First, create a standard invoice for the full amount with today’s date (see _Standard Invoicing_, above). Then post it to a reserved or deferred revenue journal and create twelve journal entries. To account for the income over the year, take one journal entry back each month.

- [`CreateGeneralJournalGetBackTransactionID`](https://github.com/accountsIQ/API-Wiki/wiki/CreateGeneralJournalGetBackTransactionID): This creates new GL journal.

## Intercompany transactions
Intercompany transactions cannot be created automatically via the API. You must create them in two separate steps. 

>AIQ Help:
>
>- [How do I create Inter-company Transaction?](https://aiq.helpjuice.com/intercompany/282303-how-do-i-create-inter-company-transactions?from_search=116655828)

First, get a list of valid intercompany connections so you can replicate the relevant one. Then create a sales invoice in one entity and a corresponding purchase invoice in the other entity.

- [`GetInterCompanyConnectionList`](https://github.com/accountsIQ/API-Wiki/wiki/GetInterCompanyConnectionList): This returns a list of valid intercompany connections. Using the data from the intercompany connection list helps you replicate the connection.
- [`GetNewSalesInvoice`](https://github.com/accountsIQ/API-Wiki/wiki/GetNewSalesInvoice): The first gives you with a new template invoice with the defaults of the customer code you provided. You can then modify data and create invoice lines. 
- [`GetNewPurchasesInvoice`](https://github.com/accountsIQ/API-Wiki/wiki/GetNewPurchasesInvoice): This creates a new invoice with the supplier defaults.
- [`SaveInvoiceGetBackInvoiceID`](https://github.com/accountsIQ/API-Wiki/wiki/SaveInvoiceGetBackInvoiceID): This saves the invoice and returns the transaction ID. However, it has not been posted yet.
- [`PostInvoiceGetBackTransactionID`](https://github.com/accountsIQ/API-Wiki/wiki/PostInvoiceGetBackTransactionID): Use this to post the transaction you created.









