---
title: Payroll
layout: default
permalink: payroll.html
category: Business Use Cases
---

# Integrating Payroll
Minimise payroll administration by integrating a specialised payroll system with AIQ. With an integration, you  can process payrolls at group level.The integration pulls the appropriate employee details from the AIQ accounts.

Payroll integration is especially beneficial for large multi-entity companies with multiple payrolls. While the manual journal import facility in AccountsIQ can handle payrolls, this process would have to be repeated for each entity. Integrating payroll at group level eliminates this issue.

## Our Partners
AccountsIQ offers an integration with [BrightPay](https://www.accountsiq.com/features/integrations/brightpay/) to manage your payroll efficiently. 

However, if you have a payroll system and are interested in integrating it with AIQ, we offer custom integration. Please contact us at [sales@accountsIQ.com](mailto:sales@accountsIQ.com) or [support@accountsIQ.com](mailto:support@accountsIQ.com) for further information.

## Using GL Journals for Payroll
Payrolls are effectively a monthly journal. Create a GL Journal with the relevant transactions.

>AIQ Help:
>
>- [Reusing Journals for Wages and Salaries](https://aiq.helpjuice.com/en_GB/general-ledger/289604-how-do-i-use-the-journal-template-feature-example-wages-and-salaries)

Ordinarily, journals are not related to employee salaries as it is all done in summary, with net pay, gross pay, pension contributions and so on. 

- [`CreateGeneralJournalGetBackTransactionID`](https://github.com/accountsIQ/API-Wiki/wiki/CreateGeneralJournalGetBackTransactionID): Create a multiline journal with your GL account codes and BI codes.This will also post it to the transaction table and return the ID of the newly created transaction. 

