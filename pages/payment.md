---
title: Receipts and Allocations Integrations
layout: default
permalink: payment.html
category: Business Use Cases
---
# Receipts and Allocations Integrations

Create a complete purchase-to-pay routine with an AccountsIQ integration. [Invoices](sales.html) created in your third-party system can be fed into AIQ and settled in either system. You can create receipts and manage full or partial allocations, then pay via the required method. 

Not only does this reduce staff workload by avoiding data entry in multiple systems, it also reduces error as different systems will all have the same records.

## Our Integration Partners
We have several options within AccountsIQ for dealing with payments:

- [GoCardless](https://gocardless.com/)
- [SmartDebit](https://www.accountsiq.com/features/integrations/smartdebit/)
- [Stripe](https://www.accountsiq.com/features/integrations/stripe-payments/)
  
Stripe is the most commonly used option. Stripe can identify the invoice and its customer and then create a receipt. The receipt and invoice then get allocated against each other.

Our API can read and write data to Stripe to create payments for customers to make in their third-party system, or we can read data from the Stripe API to create payments in AccountsIQ. 

If you are interested in any of these solutions, please contact us at [sales@accountsIQ.com](mailto:sales@accountsIQ.com) or [support@accountsIQ.com](mailto:support@accountsIQ.com).

## The Payment Process
The following can be used to identify a customer invoice, create a receipt from that invoice, and then allocate the invoice and receipt against each other.

>AIQ Help:
>
>- [How do I Process Sales Receipts and Allocations?](https://aiq.helpjuice.com/sales-system/-how-do-i-process-sales-receipts-and-allocation?from_search=116656252)

### Identifying Invoices
- [`GetTransaction`](https://github.com/accountsIQ/API-Wiki/wiki/GetTransaction): This retrieves an existing transaction from the system by its unique transaction identifier.
- [`GetInvoicesBy`](https://github.com/accountsIQ/API-Wiki/wiki/GetInvoicesBy): This can filter invoices by a range of parameters.
- [`GetInvoicesByCustomerCode`](https://github.com/accountsIQ/API-Wiki/wiki/GetInvoicesByCustomerCode): This returns a list of sales invoices created for a particular customer.

### Creating Receipts
- [`SaveSalesReceiptGetBackTransactionID`](https://github.com/accountsIQ/API-Wiki/wiki/SaveSalesReceiptGetBackTransactionID): This creates a receipt in an entity for the customer. It creates a movement between the customer’s bank and the debtor control account.
- [`GetSalesReceiptPDFByTransactionID`](https://github.com/accountsIQ/API-Wiki/wiki/GetSalesReceiptPDFByTransactionID): This returns a PDF version of the sales receipt. You can use your third-party system to then email it to the customer.

### Allocating Receipts and Invoices
- [`AllocateTransactions`](https://github.com/accountsIQ/API-Wiki/wiki/AllocateTransactions): Allocate an outstanding receipt and a sales invoice to each other.
- [`AllocateTransactionsWithDiscount`](https://github.com/accountsIQ/API-Wiki/wiki/AllocateTransactionsWithDiscount): Create a discount during the allocation process.
- [`PostPayandAllocateSalesInvoice`](https://github.com/accountsIQ/API-Wiki/wiki/PostPayAndAllocateSalesInvoice): Use this to complete the full allocation process in one go. It verifies that the invoice and sales receipt do not already exist in the system, posts a sales batch and corresponding full or partial receipts (AR), and then allocates the receipts and invoice to each other.
- [`UnallocateTransactions`](https://github.com/accountsIQ/API-Wiki/wiki/UnallocateTransactions): This deallocates a set of allocated transactions.

## Creating Refunds 
Credits and debits are used as part of any sales or purchasing integration because if you cancel an invoice in your CRM, you need to account for this in AccountsIQ. 

As you cannot cancel posted transactions in AccountsIQ, you must use credit and debit notes for a cancelling effect. 

>AIQ Help:
>
>- [Sales Debit and Credit Journals](https://aiq.helpjuice.com/sales-system/282189-sales-journals-incomplete?from_search=116656588)
- [Customer and Supplier Refunds](https://aiq.helpjuice.com/purchasing/customer-and-supplier-refunds?from_search=116656849)


### Using Credit Notes
This process involves copying the invoice, turning it into a credit note, saving it, and then allocating it to the invoice.

- [`GetNewSalesCreditNote`](https://github.com/accountsIQ/API-Wiki/wiki/GetNewSalesCreditNote): This creates a new credit note based on the customer’s account defaults.
- [`SaveCreditNote`](https://github.com/accountsIQ/API-Wiki/wiki/SaveCreditNote): This saves a modified credit note.
- [`PostCreditNotesGetBackTransactionIDs`](https://github.com/accountsIQ/API-Wiki/wiki/PostCreditNotesGetBackTransactionIDs): This posts existing credit notes to the transaction table and returns their unique transaction IDs.
- [`GetInvoice`](https://github.com/accountsIQ/API-Wiki/wiki/GetInvoice): This returns an invoice given its unique identifier.
- [`GetCreditNote`](https://github.com/accountsIQ/API-Wiki/wiki/GetCreditNote): Retrieve the credit note given its unique identifier.
- [`AllocateTransactions`](https://github.com/accountsIQ/API-Wiki/wiki/AllocateTransactions): This allocates the credit note and invoice against each other. 

### Using a GL Debit Journal
You can also use a GL Sales Debit Journal to create refunds.

- [`GetGLDefaults`](https://github.com/accountsIQ/API-Wiki/wiki/GetGLDefaults): This returns all defaults to create a new GL account if you do not have one set up.
- [`SaveGLDefaults`](https://github.com/accountsIQ/API-Wiki/wiki/SaveGLDefaults): This saves and modifies the GL defaults.
- [`PostSalesDebitJournalGetBackTransactionID`](https://github.com/accountsIQ/API-Wiki/wiki/PostSalesDebitJournalGetBackTransactionID): Create a receipt, then use this to create a sales debit journal for refunding purposes.

