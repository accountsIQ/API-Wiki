---
title: A-Z
layout: default
permalink: pages/a-z/
category: Glossary
---
# A-Z

## A
**Allocatable Transactions:**
Transactions that are eligible for allocation.

To cancel each other out, you must match a transaction from Column A with its equivalent from Column B:

<table>
    <tr>
        <th>A</th>
        <th>B</th>
    </tr>    
    <tr>
        <td>Sales Invoice</td>
        <td>Sales Credit Note</td>
    </tr>
    <tr>
        <td>Sales Payment (Refund)</td>
        <td>Sales Receipt</td>
    </tr>
    <tr>
        <td>Sales Debit Journal</td>
        <td>Sales Credit Journal</td>
    </tr>
    <tr>
        <td>Purchases Invoice</td>
        <td>Purchases Credit Note</td>
    </tr>
    <tr>
        <td>Purchases Receipt</td>
        <td>Purchases Payment (Refund)</td>
    </tr>
    <tr>
        <td>Purchase Credit Journal</td>
        <td>Purchase Debit Journal</td>
    </tr>
</table>

## B

**Batch Invoice:**
A batch invoice is an invoice whose lines do not hold a reference to a stock item. This means the creation of a batch invoice does not involve stock movement / transactions. A batch invoice is directly posted to the transactions table while a Product Invoice must be posted to hit the transactions journal.

**Business Documents:**
A business document is one of the following documents:

- Purchases Delivery
- Purchases Invoice & Purchases Debit Note
- Purchases Order
- Sales Delivery
- Sales Invoice & Sales Credit Note
- Sales Order
- Sales Quote

## C

**Customer:**
A customer organizes a regroupment of Entities. A customer can be an accountancy practice with business companies for entities, a franchisor with franchisees for entities.

## E

**Entity:**
An entity is a representation of a client company and belongs to a customer. 

## P

**Product Invoice:**
A product invoice involves an item for each of its line. It can be created, modified and only later on posted to the transaction journal. For an invoice which does not need this workflow, please see Batch Invoice. Product invoices also support stock movements.

## R

**Required Accounts:**
Required accounts are a set of General Ledger accounts with pre-defined functions that the system will be using. Examples of those are the sales debtors control account, FX gains & losses, Open Stock, etc.

**Retrospective Ageing:**
A retrospective ageing is an ageing report that enables the user to see the system in the same state as it was back at a given date: transaction appear or not according to their date and allocation are present or absent according to their date.

## S

**Service Invoices:**
All lines in a service invoice reference services or non-stock items. Unlike a Batch Invoice it does not directly impact the ledger with monetary movements. Instead, it supports a pro-forma workflow, and can be checked prior to posting to the ledger.

## T

**Transaction Types:**
The following transaction types exist in the AccountsIQ system:
- BC: Bank Credit Journal
- BD: Bank Debit Journal
- BP: Bank Payment
- BR: Bank Receipt
- DP: Purchases Discount
- DS: Sales Discount
- GA: Accrual
- GP: Prepayment
- ST: Stock Transfer
- GC/GD: General Journal
- PC: Purchases Credit Journal
- PD: Purchases Debit Journal
- PI: Purchases Invoice
- PN: Purchases Credit Note
- PP: Purchases Payment (Refund)
- PR: Purchases Receipt
- PX: Purchases Currency Fluctuation
- SC: Sales Credit Journal
- SD: Sales Debit Journal
- SI: Sales Invoice
- SN: Sales Credit Note
- SP: Sales Payment (Refund)
- SR: Sales Receipt
- SX: Sales Currency Fluctuation
