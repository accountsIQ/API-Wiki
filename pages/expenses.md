---
title: Integrating Expenses
layout: default
permalink: expenses.html
category: Business Use Cases
---
# Integrating Expenses
Integrate expenses so that approved transactions can flow directly into AccountsIQ and be settled there. Not only will this significantly cut down on administration by eliminating the need for paperwork and double entry, it will keep your records in agreement. 

Expense integrations are especially beneficial for multi-entity companies, as it allows expense management at group level. This means they can purchase one instance of a software, rather than multiple, use it for the whole group and then split the expenses by entity.

## Our Partners
AIQ has several partners that offer expense tracking and approval solutions:

- [Concur](https://www.accountsiq.com/features/integrations/concur/)
- [Expensify](https://www.accountsiq.com/features/integrations/expensify/)
- [ExpenseIn](https://www.accountsiq.com/features/integrations/expensein/)
- Payhawk
- Pleo
- Zoho

If your company uses these or another solution and would like to integrate it with AIQ, we offer custom integrations. Contact our team at at [sales@accountsIQ.com](mailto:sales@accountsIQ.com) or [support@accountsIQ.com](mailto:support@accountsIQ.com) for more details.

## Invoicing vs Sundry Payments
There are two categories of expenses that will determine which approach you take:

- **Out-of-pocket:** Use purchase invoicing. Employees must be set up as suppliers first. 
- **Not out-of-pocket:** Use either purchase invoicing or sundry bank payments. With sundry payments you don’t have to set up employees as suppliers.

>AIQ Help:
>
>- [How does Purchase Invoicing Work?](https://aiq.helpjuice.com/purchasing/285995-how-does-the-purchase-un-ordered-product-invoice-work?from_search=116657627)
- [Sundry Bank Payments](https://aiq.helpjuice.com/bank-system/282176-sundry-bank-payments-incomplete?from_search=116657258)

### Using Purchase Invoicing for expenses
First, set up your employees as suppliers.

- [`UpdateSupplier`](https://github.com/accountsIQ/API-Wiki/wiki/UpdateSupplier): Use this to create a new supplier with your employee’s details.
  
Next, record the invoice against your employee, and pay them later. We recommend using batch invoicing to control for VAT more easily and particularly when you have cash out-of-pocket expenses.

- [`GetNewPurchasesInvoice`](https://github.com/accountsIQ/API-Wiki/wiki/GetNewPurchasesInvoices): This creates a new invoice with the supplier defaults (i.e., the employee).
- [`SaveInvoiceGetBackInvoiceID`](https://github.com/accountsIQ/API-Wiki/wiki/SaveInvoiceGetBackInvoiceID): This saves a modified invoice.
- [`PostInvoiceGetBackTransactionID`](https://github.com/accountsIQ/API-Wiki/wiki/PostInvoiceGetBackTransactionID): This posts an invoice.
- [`GetNewBatchPurchasesInvoice`](https://github.com/accountsIQ/API-Wiki/wiki/GetNewBatchPurchasesInvoice): This fills the invoice with the supplier defaults (i.e., the employee). It does not save or post the batch.
- [`CreateBatchPurchasesInvoice`](https://github.com/accountsIQ/API-Wiki/wiki/CreateBatchPurchasesInvoice): This posts the batch to the transaction table.
- [`SavePurchasePayment`](https://github.com/accountsIQ/API-Wiki/wiki/SavePurchasePayment): This creates a payment in an entity for the indicated supplier. It will create a movement between the supplier's bank and the supplier's creditor control account.

### Using Sundry bank payments for expenses
The sundry bank payment is a non-supplier VAT aware transaction, so you don't need to set your employees up a supplier, but you can still claim VAT if it is present and correct. 

- [`SaveSundryReceiptPaymentsGetBackTransactionIDs`](https://github.com/accountsIQ/API-Wiki/wiki/SaveSundryReceiptPaymentsGetBackTransactionIDs): This creates a sundry payment in an entity for the indicated bank and creates a movement between the bank and GL account.

## Using Credit Cards

>AIQ Help:
>
>- [How Do I Manage My Employee Credit Cards and other Out-of-pocket Expenses?](https://aiq.helpjuice.com/bank-system/289778-how-do-i-manage-my-employee-credit-cards-and-other-out-of-pocket-expenses?from_search=116657785)

For credit cards, set up the credit card as a supplier.

- [`UpdateSupplier`](https://github.com/accountsIQ/API-Wiki/wiki/UpdateSupplier): Use this to set up the credit card as a supplier.
  
Record the expenses against it as invoices (see _Using Purchase Invoicing_, above). 

Pay the credit card off through your regular [payment runs](payment.html). Using the credit card statement, reconcile the card (supplier) and the expense claims (supplier invoices).

## Using Prepaid Cards
With prepaid cards (Pleo, Payhawk), there are no out-of-pocket expenses. 

- [`SaveSundryReceiptPaymentsGetBackTransactionIDs`](https://github.com/accountsIQ/API-Wiki/wiki/SaveSundryReceiptPaymentsGetBackTransactionIDs): This creates a sundry payment in an entity for the indicated bank and creates a movement between the bank and GL account.

## Cross-charging and Recharging
Cross-charging and recharging expenses can occur in multi-entity companies. 

>AIQ Help:
>
>- [How Do I Create Inter-Company Transactions?](https://aiq.helpjuice.com/en_GB/intercompany/282303-how-do-i-create-inter-company-transactions)

For example, if an employee from a UK company does business for an Irish company in the same group, expenses in Ireland would go to the UK company who would be able to claim them from the Irish company.

- [`GetInterCompanyConnectionList`](https://github.com/accountsIQ/API-Wiki/wiki/GetInterCompanyConnectionList): This lets you replicate the intercompany connection that exists in AccountsIQ. This way you can create corresponding sales and purchase invoices to do the cross charging and recharging. 


