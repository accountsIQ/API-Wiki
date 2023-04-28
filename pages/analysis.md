---
title: Business Analysis
layout: default
permalink: analysis.html
category: Business Use Cases
---

# Integrating Analysis Systems
Pull data from AccountsIQ into your preferred analysis software to produce live dashboards, enhanced with your business line data. See if your company is on target in terms of both cash flow and budgeting and adjust your business decisions accordingly.

If your company is multi-entity, analysis tools are especially useful as you can analyse performance from multiple perspectives, such as comparing different branches, regions, or product sales. Then tweak analysis parameters to gain predictive insights.

## Our Partners
We currently have an integration with [ProForecast](https://www.accountsiq.com/features/integrations/proforecast/) that lets you bring in accounting data from AIQ, set the relevant budgets and targets and then refresh this data with actuals as often as necessary. 

If there is another system you want to integrate with, we also offer custom integrations to meet your requirements. Contact us at [sales@accountsIQ.com](mailto:sales@accountsIQ.com) or [support@accountsIQ.com](mailto:support@accountsIQ.com) for more details.

## Cashflow Forecasting Systems
You can pull data out of AccountsIQ into a cash forecasting system. In addition, we have an OData end point for some data. The following endpoints can help create the desired data set.

>AIQ Help:
>
>- [OData Connection Setup](https://aiq.helpjuice.com/odata/odata-connection-setup?from_search=116658632)
>- [Creating an OData Connection](https://aiq.helpjuice.com/en_GB/odata/1190738-creating-an-odata-connection)
>- [Using an Odata Connection](https://aiq.helpjuice.com/en_GB/odata/using-an-odata-connection)

- [`GetTransactions`](https://github.com/accountsIQ/API-Wiki/wiki/GetTransaction): This returns an existing transaction from the system given its unique transaction identifier.
- [`GetTransactionsBy`](https://github.com/accountsIQ/API-Wiki/wiki/GetTransactionsBy): This returns a filtered list of transactions. This lets you search by date. You can use it to update a data set.
- [`GetTransactionsByExternalReference`](https://github.com/accountsIQ/API-Wiki/wiki/GetTransactionsByExternalReference): This returns a filtered list of transactions matching this reference based on the external reference.
- [`GetChartOfAccounts`](https://github.com/accountsIQ/API-Wiki/wiki/GetChartOfAccounts): You can also extract data by account. This returns a list of all financial accounts in the general ledger for the current company.
- [`GetAccountsWithTransactionsCreatedBetween`](https://github.com/accountsIQ/API-Wiki/wiki/GetAccountsWithTransactionsCreatedBetween): This returns a summary of customer/supplier activity by date and transaction type. This allows a third-party system to check if a set of customers or suppliers has had any transactions of interest since the last check. This can be run against all customers/suppliers or a selected sub-range.
- [`GetAccountBalanceInformation`](https://github.com/accountsIQ/API-Wiki/wiki/GetAccountBalanceInformation): Get the balance and credit limits at the specified date so you can analyse your cashflow situation.
- [`GetCustomersStatement`](https://github.com/accountsIQ/API-Wiki/wiki/GetCustomersStatement): This shows the current debt broken down by invoice and due date, making it very useful for cashflow forecasting as you can find out when you are going to get paid. If you have multiple entities, you can extract all the data across all the different entities into a CSV file, then feed the data into a third-party system. 

## Budgeting Systems
For budgeting systems, instead of importing transaction data into a third-party system, you can let AIQ do the analysis and then extract those results. 

For basic budgeting, such as overhead spending, GL level analysis might be sufficient. If your analysis system doesn’t need to drill down to transaction level, extracting trial balances could return a detailed enough analysis.

>AIQ Help:
>
>- [How Do I Set Up and Maintain General Ledger Accounts?](https://aiq.helpjuice.com/en_GB/general-ledger/287341-how-do-i-setup-and-maintain-general-ledger-accounts)

- [`GetTrialBalanceForPeriod`](https://github.com/accountsIQ/API-Wiki/wiki/GetTrialBalanceForPeriod): This returns the pre-calculated reporting dataset for the trial balance report based on period values.
- [`GetTrialBalanceFromStartOfPeriod`](https://github.com/accountsIQ/API-Wiki/wiki/GetTrialBalanceFromStartOfPeriod): This returns the trial balance movements for a company since the start of a period, giving a point in time balance in the middle of the period. While `GetTrialBalanceForPeriod` gets full period totals, this gets the balance at any point in the period by going back to the transactions themselves. However, it is slower.
  
## P&L Reporting using BI Codes
Using BI Codes (called Departments in the API) gives you extra control over how you can analyse your data. 

> Learn More:
> 
> - [How do I Implement Extended Business Analysis?](https://aiq.helpjuice.com/en_GB/analysis/289280-how-do-i-implement-extended-business-analysis)
> - [Extended Business Analysis for Job or Project Analysis](https://aiq.helpjuice.com/en_GB/analysis/289415-how-do-i-implement-job-or-project-analysis-using-extended-business-analysis)

For example, when raising sales and purchase invoices, the customer can be used as part of the BI Code, so that P&L can be done by customer. This is possible if every invoice is tied to a project and that project is tied to a customer. 

Alternatively, instead of customers, you could analyse by supplier or product.

### Creating BI Codes via the API 
If you have a complex BI code structure and are tracking by customers and projects, you need to be able to create new BI Codes as new projects or customers come on board. Setting up and managing complex BI structures via the API is much more manageable than doing it manually. 

BI Codes can have up to six BI dimensions, each with as many elements as needed. They can be based on data from the customer, item code, a third-party system, or a combination.  

BI Codes are linked to transaction lines which in turn link them to dimensions and analysis codes via the BI Setup. This underpins all advanced reporting in the system.

If a third-party system doesn’t have a GL code to post from, use non-stock items to set default BI and GL codes, even if you don’t use them on the invoice.

- [`GetAnalysisDimensionSetup`](https://github.com/accountsIQ/API-Wiki/wiki/GetAnalysisDimensionSetup): This returns the entire BI setup with each BI Dimension and their underlying codes.
- [`GetDepartmentById`](https://github.com/accountsIQ/API-Wiki/wiki/GetDepartmentById): This lets you search by BI Code.
- [`GetDepartmentList`](https://github.com/accountsIQ/API-Wiki/wiki/GetDepartmentList): This returns available BI Codes, both active and inactive.
- [`GetDepartmentsByAnalysisCode`](https://github.com/accountsIQ/API-Wiki/wiki/GetDepartmentsByAnalysisCode): This lets you search by dimension.
- [`UpdateDepartment`](https://github.com/accountsIQ/API-Wiki/wiki/UpdateDepartment): This modifies the description and active status of a Department. Use this when you wish to retire a code or update the description.


