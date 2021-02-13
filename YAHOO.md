# Using ImportJSON to pull data from Yahoo Finance in Google Sheets
The following documentation is a comprehensive guide on how to use ImportJSON to display financial data from Yahoo Finance in your Google Sheets. Follow the steps below to get started!

## Getting Started
1. Go to bradjasper's [ImportJSON.gs](https://github.com/bradjasper/ImportJSON/blob/master/ImportJSON.gs) file and copy the script
2. In Google Sheets open Script Editor in the Tools menu
3. Remove the existing script and paste in the script from the **ImportJSON.gs** file
```javascript
function myFunction() {

}
```
4. Rename the project to 'ImportJSON' and click Save
5. Select the ImportJSON function and click Run to execute the code in the Script Editor
6. You will now be prompted to give permissions to the function (you will get an error because myFunction was removed... this is okay!)
7. Congratulations! You can now use the `=ImportJSON(`[URL](#URL),[Query](#Query),[Options](#Options)`)` function in your google sheets
  
  
### URL
The URL is the web address of the dataset you are looking for.
> `=ImportJSON(`**URL**`,Query,Options)`

For Yahoo Finance the URL would look like the following, where **Symbol** is the stock symbol and **Module** is the data. Replace **Module** with any high level Yahoo Finance module from the [Modules List](#Modules).
> `http://query2.finance.yahoo.com/v10/finance/quoteSummary/`**Symbol**`?modules=`**Module**


For Example:

If your Google Sheet contains the symbol of a stock in cell **A1** , you could use the following formula in another cell to get *ALL* of the stock's "Key Statistics" from the Key Statistics module:
> `=ImportJSON("http://query2.finance.yahoo.com/v10/finance/quoteSummary/"&`**A1**`&"?modules=defaultKeyStatistics","/quoteSummary/result/defaultKeyStatistics","")`
  
  
### Query
The query points to the exact location of data you'd like to display.
> `=ImportJSON(URL,`**Query**`,Options)`

All Yahoo Finance queries start with `/quoteSummary/result/` and then you must select a "Module" that contains the data you are looking for. Replace **Module** with any high level module from the [Modules List](#Modules) and/or the exact location of the nested data you are looking for.

For Example:

> `/quoteSummary/result/defaultKeyStatistics/price/raw`
  
  
### Options
Options can be used to alter the output of the data. You can enter multiple options seperated by commas.
> `=ImportJSON(URL,Query,`**Options**`)`

- **noInherit**: Don't inherit values from parent elements
- **noTruncate**: Don't truncate values
- **rawHeaders**: Don't prettify headers
- **noHeaders**: Don't include headers, only the data
- **allHeaders**: Include all headers from the query parameter in the order they are listed
- **debugLocation**: Prepend each value with the row & column it belongs in

For Example:
If your Google Sheet contains the symbol of a stock in cell **A1**, you could use the following formula in another cell to get *only* the stock price:
> =ImportJSON(`"http://query2.finance.yahoo.com/v10/finance/quoteSummary/`"&**A1**&"?modules=defaultKeyStatistics","/quoteSummary/result/defaultKeyStatistics/price/raw","noInheret,noTruncate,noHeaders")
  
  
  
  
# Modules
Yahoo Finance sorts company information into modules. Use the following table to locate the module containing data you're looking for.
Description | Module Name
------------|------------
[Asset Profile](#asset-profile) | assetProfile
[Balance Sheet History (Annual)](#balance-sheet-history-annual) | balanceSheetHistory
[Balance Sheet History (Quarterly)](#balance-sheet-history-quarterly) | balanceSheetHistoryQuarterly
[Calendar Events](#calendar-events) | calendarEvents
[Cash Flow Statement History (Annual)](#cash-flow-statement-history-annual) | cashflowStatementHistory
[Cash Flow Statement History (Quarterly)](#cash-flow-statement-history-quarterly) | cashflowStatementHistoryQuarterly
[Key Statistics](#key-statistics) | defaultKeyStatistics
[Earnigs](#earnings) | earnings
[Earnings History](#earnigs-history) | earningsHistory
[Earnings Trend](#earnings-trend) | earningsTrend
[ESG Scores](#esg-scores) | esgScores
[Financial Data](#financial-data) | financialData
[Fund Ownership](#fund-ownership) | fundOwnership
[Income Statement History (Annual)](#income-statement-history-annual) | incomeStatementHistory
[Income Statement History (Quarterly)](#income-statement-history-quarterly) | incomeStatementHistoryQuarterly
[Index Trend](#index-trend) | indexTrend
[Industry Trend](#industry-trend) | indexTrend
[Insider Holders](#industry-holders) | insiderHolders
[Insider Transactions](#insider-transactions) | insiderTransactions
[Institution Owenership](#institution-ownership) | institutionOwnership
[Major Direct Holders](#major-direct-holders) | majorDirectHolders
[Major Holders Breakdown](#major-holders-breakdown) | majorHoldersBreakdown
[Net Share Purchase Activity](#net-share-purchase-activity) | netSharePurchaseActivity
[Page Views](#page-views) | pageViews
[Price](#price) | price
[Quote Type](#quote-type) | quoteType
[Recommendation Trend](#recommendation-trend) | recommendationTrend
[SEC Filings](#sec-filings) | secFilings
[Sector Trend](#sector-trend) | sectorTrend
[Summary Detail](#summary-detail) | summaryDetail
[Summary Profile](#summary-profile) | summaryProfile
[Upgrade Downgrade History](#upgrade-downgrade-history) | upgradeDowngradeHistory


## Data Formats
Most modules will contain nested data that may be formatted in mutiple ways. Note the differences in the formats below:  
/`raw` *(raw value only)*  
/`fmt` *(formatted as truncated string)*  
/`longfmt` *(formatted as string)*  


## Asset Profile
The **assetProfile** module displays data from the company's [Profile](https://finance.yahoo.com/quote/AAPL/profile?p=AAPL)  

**Query:**  
`/quoteSummary/result/assetProfile` + **Nested Data** (*optional*)  

**Nested Data:**  
> *Company Address: Street*  
> /`address1`  
> 
> *Company Address: City*  
> /`city`  
> 
> *Company Address: Zip Code*  
> /`zip`  
> 
> *Company Address: Country*  
> /`country`  
> 
> *Company Phone Number*  
> /`phone`  
> 
> *Company Fax*  
> /`fax`  
> 
> *Company Website*  
> /`website`  
> 
> *Company Market Industry*  
> /`industry`  
> 
> *Company Market Sector*  
> /`sector`  
> 
> *Company Business Summary*  
> /`longBusinessSummary`  
> 
> *Company Full-Time Employees*  
> /`fullTimeEmployees`  
> 
> *Company Officers*  
> /`companyOfficers`  


## Balance Sheet History (Annual)
The **balanceSheetHistory** module displays data from the company's [Annual Balance Sheet](https://finance.yahoo.com/quote/AAPL/balance-sheet?p=AAPL). (*Navigate to Annual tab*)  
Learn more about financial statements on [Investopedia](https://www.investopedia.com/terms/f/financial-statements.asp)  
Learn more about corporate balance sheets on [Investopedia](https://www.investopedia.com/articles/04/031004.asp/)  

**Query:**  
`/quoteSummary/result/balanceSheetHistory` + **Nested Data** (*optional*)  

**Nested Data:**  
> *Balance Sheet Statements (All Data)*  
> /`balanceSheetStatements`  
> 
> *Maximum number of seconds results of the Balance Sheets Statements query can be cached*  
> /`balanceSheetStatements`/`maxAge`  
> 
> *Balance Sheets Statements End Date*  
> /`balanceSheetStatements`/`endDate`  
> /`balanceSheetStatements`/`endDate`/`raw`  
> /`balanceSheetStatements`/`endDate`/`fmt`  
> 
> *Balance Sheets Statements Cash*  
> /`balanceSheetStatements`/`cash`  
> /`balanceSheetStatements`/`cash`/`raw`  
> /`balanceSheetStatements`/`cash`/`fmt`  
> /`balanceSheetStatements`/`cash`/`longfmt`  
> 
> *Balance Sheets Statements Short Term Investments*  
> /`balanceSheetStatements`/`shortTermInvestments`  
> /`balanceSheetStatements`/`shortTermInvestments`/`raw`  
> /`balanceSheetStatements`/`shortTermInvestments`/`fmt`  
> /`balanceSheetStatements`/`shortTermInvestments`/`longfmt`  
> 
> *Balance Sheets Statements SNet Receivables*  
> /`balanceSheetStatements`/`netReceivables`  
> /`balanceSheetStatements`/`netReceivables`/`raw`  
> /`balanceSheetStatements`/`netReceivables`/`fmt`  
> /`balanceSheetStatements`/`netReceivables`/`longfmt`  
> 
> *Balance Sheets Statements Inventory*  
> /`balanceSheetStatements`/`inventory`  
> /`balanceSheetStatements`/`inventory`/`raw`  
> /`balanceSheetStatements`/`inventory`/`fmt`  
> /`balanceSheetStatements`/`inventory`/`longfmt`  
> 
> *Balance Sheets Statements Total Current Assets*  
> /`balanceSheetStatements`/`totalCurrentAssets`  
> /`balanceSheetStatements`/`totalCurrentAssets`/`raw`  
> /`balanceSheetStatements`/`totalCurrentAssets`/`fmt`  
> /`balanceSheetStatements`/`totalCurrentAssets`/`longfmt`  
> 
> *Balance Sheets Statements Property Plant Equipment*  
> /`balanceSheetStatements`/`propertyPlantEquipment`  
> /`balanceSheetStatements`/`propertyPlantEquipment`/`raw`  
> /`balanceSheetStatements`/`propertyPlantEquipment`/`fmt`  
> /`balanceSheetStatements`/`propertyPlantEquipment`/`longfmt`  
> 
> *Balance Sheets Statements Goodwill*  
> /`balanceSheetStatements`/`goodwill`  
> /`balanceSheetStatements`/`goodwill`/`raw`  
> /`balanceSheetStatements`/`goodwill`/`fmt`  
> /`balanceSheetStatements`/`goodwill`/`longfmt`  
> 
> *Balance Sheets Statements Intangible Assets*  
> /`balanceSheetStatements`/`intangibleAssets`  
> /`balanceSheetStatements`/`intangibleAssets`/`raw`  
> /`balanceSheetStatements`/`intangibleAssets`/`fmt`  
> /`balanceSheetStatements`/`intangibleAssets`/`longfmt`  
> 
> *Balance Sheets Statements Other Assets*  
> /`balanceSheetStatements`/`otherAssets`  
> /`balanceSheetStatements`/`otherAssets`/`raw`  
> /`balanceSheetStatements`/`otherAssets`/`fmt`  
> /`balanceSheetStatements`/`otherAssets`/`longfmt`  
> 
> *Balance Sheets Statements Deferred Long Term Asset Charges*  
> /`balanceSheetStatements`/`deferredLongTermAssetCharges`  
> /`balanceSheetStatements`/`deferredLongTermAssetCharges`/`raw`  
> /`balanceSheetStatements`/`deferredLongTermAssetCharges`/`fmt`  
> /`balanceSheetStatements`/`deferredLongTermAssetCharges`/`longfmt`  
> 
> *Balance Sheets Statements Total Assets*  
> /`balanceSheetStatements`/`totalAssets`  
> /`balanceSheetStatements`/`totalAssets`/`raw`  
> /`balanceSheetStatements`/`totalAssets`/`fmt`  
> /`balanceSheetStatements`/`totalAssets`/`longfmt`  
> 
> *Balance Sheets Statements Accounts Payable*  
> /`balanceSheetStatements`/`accountsPayable`  
> /`balanceSheetStatements`/`accountsPayable`/`raw`  
> /`balanceSheetStatements`/`accountsPayable`/`fmt`  
> /`balanceSheetStatements`/`accountsPayable`/`longfmt`  
> 
> *Balance Sheets Statements Other Current Liabilities*  
> /`balanceSheetStatements`/`otherCurrentLiab`  
> /`balanceSheetStatements`/`otherCurrentLiab`/`raw`  
> /`balanceSheetStatements`/`otherCurrentLiab`/`fmt`  
> /`balanceSheetStatements`/`otherCurrentLiab`/`longfmt`  
> 
> *Balance Sheets Statements Long Term Debt*  
> /`balanceSheetStatements`/`longTermDebt`  
> /`balanceSheetStatements`/`longTermDebt`/`raw`  
> /`balanceSheetStatements`/`longTermDebt`/`fmt`  
> /`balanceSheetStatements`/`longTermDebt`/`longfmt`  
> 
> *Balance Sheets Statements Other Liabilities*  
> /`balanceSheetStatements`/`otherLiab`  
> /`balanceSheetStatements`/`otherLiab`/`raw`  
> /`balanceSheetStatements`/`otherLiab`/`fmt`  
> /`balanceSheetStatements`/`otherLiab`/`longfmt`  
> 
> *Balance Sheets Statements Total Current Liabilities*  
> /`balanceSheetStatements`/`totalCurrentLiabilities`  
> /`balanceSheetStatements`/`totalCurrentLiabilities`/`raw`  
> /`balanceSheetStatements`/`totalCurrentLiabilities`/`fmt`  
> /`balanceSheetStatements`/`totalCurrentLiabilities`/`longfmt`  
> 
> *Balance Sheets Statements Total Liabilities*  
> /`balanceSheetStatements`/`totalLiab`  
> /`balanceSheetStatements`/`totalLiab`/`raw`  
> /`balanceSheetStatements`/`totalLiab`/`fmt`  
> /`balanceSheetStatements`/`totalLiab`/`longfmt`  
> 
> *Balance Sheets Statements Common Stock*  
> /`balanceSheetStatements`/`commonStock`  
> /`balanceSheetStatements`/`commonStock`/`raw`  
> /`balanceSheetStatements`/`commonStock`/`fmt`  
> /`balanceSheetStatements`/`commonStock`/`longfmt`  
> 
> *Balance Sheets Statements Retained Earnings*  
> /`balanceSheetStatements`/`retainedEarnings`  
> /`balanceSheetStatements`/`retainedEarnings`/`raw`  
> /`balanceSheetStatements`/`retainedEarnings`/`fmt`  
> /`balanceSheetStatements`/`retainedEarnings`/`longfmt`  
> 
> *Balance Sheets Statements Treasurey Stock*  
> /`balanceSheetStatements`/`treasuryStock`  
> /`balanceSheetStatements`/`treasuryStock`/`raw`  
> /`balanceSheetStatements`/`treasuryStock`/`fmt`  
> /`balanceSheetStatements`/`treasuryStock`/`longfmt`  
> 
> *Balance Sheets Statements Capital Surplus*  
> /`balanceSheetStatements`/`capitalSurplus`  
> /`balanceSheetStatements`/`capitalSurplus`/`raw`  
> /`balanceSheetStatements`/`capitalSurplus`/`fmt`  
> /`balanceSheetStatements`/`capitalSurplus`/`longfmt`  
> 
> *Balance Sheets Statements Other Stock Holder Equity*  
> /`balanceSheetStatements`/`otherStockholderEquity`  
> /`balanceSheetStatements`/`otherStockholderEquity`/`raw`  
> /`balanceSheetStatements`/`otherStockholderEquity`/`fmt`  
> /`balanceSheetStatements`/`otherStockholderEquity`/`longfmt`  
> 
> *Balance Sheets Statements Total Stock Holder Equity*  
> /`balanceSheetStatements`/`totalStockholderEquity`  
> /`balanceSheetStatements`/`totalStockholderEquity`/`raw`  
> /`balanceSheetStatements`/`totalStockholderEquity`/`fmt`  
> /`balanceSheetStatements`/`totalStockholderEquity`/`longfmt`  
> 
> *Balance Sheets Statements Net Tangible Assets*  
> /`balanceSheetStatements`/`netTangibleAssets`  
> /`balanceSheetStatements`/`netTangibleAssets`/`raw`  
> /`balanceSheetStatements`/`netTangibleAssets`/`fmt`  
> /`balanceSheetStatements`/`netTangibleAssets`/`longfmt`  
> 
> *Balance Sheets Statements Short Long Term Debt*  
> /`balanceSheetStatements`/`shortLongTermDebt`  
> /`balanceSheetStatements`/`shortLongTermDebt`/`raw`  
> /`balanceSheetStatements`/`shortLongTermDebt`/`fmt`  
> /`balanceSheetStatements`/`shortLongTermDebt`/`longfmt`
> 
> *Maximum number of seconds results of the Balance Sheets History query can be cached*  
> /`maxAge`


## Balance Sheet History (Quarterly)
The **balanceSheetHistory** module displays data from the company's [Quarterly Balance Sheet](https://finance.yahoo.com/quote/AAPL/balance-sheet?p=AAPL). (*Navigate to Quarterly tab*)  
Learn more about financial statements on [Investopedia](https://www.investopedia.com/terms/f/financial-statements.asp)  
Learn more about corporate balance sheets on [Investopedia](https://www.investopedia.com/articles/04/031004.asp/)  

**Query:**  
`/quoteSummary/result/balanceSheetHistoryQuarterly` + **Nested Data** (*optional*)  

**Nested Data:**  
> *Balance Sheet Statements (All Data)*  
> /`balanceSheetStatements`  
> 
> *Maximum number of seconds results of the balanceSheetsStatements query can be cached*  
> /`balanceSheetStatements`/`maxAge`  
> 
> *Balance Sheets Statements End Date*  
> /`balanceSheetStatements`/`endDate`  
> /`balanceSheetStatements`/`endDate`/`raw`  
> /`balanceSheetStatements`/`endDate`/`fmt`  
> 
> *Balance Sheets Statements Cash*  
> /`balanceSheetStatements`/`cash`  
> /`balanceSheetStatements`/`cash`/`raw`  
> /`balanceSheetStatements`/`cash`/`fmt`  
> /`balanceSheetStatements`/`cash`/`longfmt`  
> 
> *Balance Sheets Statements Short Term Investments*  
> /`balanceSheetStatements`/`shortTermInvestments`  
> /`balanceSheetStatements`/`shortTermInvestments`/`raw`  
> /`balanceSheetStatements`/`shortTermInvestments`/`fmt`  
> /`balanceSheetStatements`/`shortTermInvestments`/`longfmt`  
> 
> *Balance Sheets Statements SNet Receivables*  
> /`balanceSheetStatements`/`netReceivables`  
> /`balanceSheetStatements`/`netReceivables`/`raw`  
> /`balanceSheetStatements`/`netReceivables`/`fmt`  
> /`balanceSheetStatements`/`netReceivables`/`longfmt`  
> 
> *Balance Sheets Statements Inventory*  
> /`balanceSheetStatements`/`inventory`  
> /`balanceSheetStatements`/`inventory`/`raw`  
> /`balanceSheetStatements`/`inventory`/`fmt`  
> /`balanceSheetStatements`/`inventory`/`longfmt`  
> 
> *Balance Sheets Statements Total Current Assets*  
> /`balanceSheetStatements`/`totalCurrentAssets`  
> /`balanceSheetStatements`/`totalCurrentAssets`/`raw`  
> /`balanceSheetStatements`/`totalCurrentAssets`/`fmt`  
> /`balanceSheetStatements`/`totalCurrentAssets`/`longfmt`  
> 
> *Balance Sheets Statements Property Plant Equipment*  
> /`balanceSheetStatements`/`propertyPlantEquipment`  
> /`balanceSheetStatements`/`propertyPlantEquipment`/`raw`  
> /`balanceSheetStatements`/`propertyPlantEquipment`/`fmt`  
> /`balanceSheetStatements`/`propertyPlantEquipment`/`longfmt`  
> 
> *Balance Sheets Statements Goodwill*  
> /`balanceSheetStatements`/`goodwill`  
> /`balanceSheetStatements`/`goodwill`/`raw`  
> /`balanceSheetStatements`/`goodwill`/`fmt`  
> /`balanceSheetStatements`/`goodwill`/`longfmt`  
> 
> *Balance Sheets Statements Intangible Assets*  
> /`balanceSheetStatements`/`intangibleAssets`  
> /`balanceSheetStatements`/`intangibleAssets`/`raw`  
> /`balanceSheetStatements`/`intangibleAssets`/`fmt`  
> /`balanceSheetStatements`/`intangibleAssets`/`longfmt`  
> 
> *Balance Sheets Statements Other Assets*  
> /`balanceSheetStatements`/`otherAssets`  
> /`balanceSheetStatements`/`otherAssets`/`raw`  
> /`balanceSheetStatements`/`otherAssets`/`fmt`  
> /`balanceSheetStatements`/`otherAssets`/`longfmt`  
> 
> *Balance Sheets Statements Deferred Long Term Asset Charges*  
> /`balanceSheetStatements`/`deferredLongTermAssetCharges`  
> /`balanceSheetStatements`/`deferredLongTermAssetCharges`/`raw`  
> /`balanceSheetStatements`/`deferredLongTermAssetCharges`/`fmt`  
> /`balanceSheetStatements`/`deferredLongTermAssetCharges`/`longfmt`  
> 
> *Balance Sheets Statements Total Assets*  
> /`balanceSheetStatements`/`totalAssets`  
> /`balanceSheetStatements`/`totalAssets`/`raw`  
> /`balanceSheetStatements`/`totalAssets`/`fmt`  
> /`balanceSheetStatements`/`totalAssets`/`longfmt`  
> 
> *Balance Sheets Statements Accounts Payable*  
> /`balanceSheetStatements`/`accountsPayable`  
> /`balanceSheetStatements`/`accountsPayable`/`raw`  
> /`balanceSheetStatements`/`accountsPayable`/`fmt`  
> /`balanceSheetStatements`/`accountsPayable`/`longfmt`  
> 
> *Balance Sheets Statements Other Current Liabilities*  
> /`balanceSheetStatements`/`otherCurrentLiab`  
> /`balanceSheetStatements`/`otherCurrentLiab`/`raw`  
> /`balanceSheetStatements`/`otherCurrentLiab`/`fmt`  
> /`balanceSheetStatements`/`otherCurrentLiab`/`longfmt`  
> 
> *Balance Sheets Statements Long Term Debt*  
> /`balanceSheetStatements`/`longTermDebt`  
> /`balanceSheetStatements`/`longTermDebt`/`raw`  
> /`balanceSheetStatements`/`longTermDebt`/`fmt`  
> /`balanceSheetStatements`/`longTermDebt`/`longfmt`  
> 
> *Balance Sheets Statements Other Liabilities*  
> /`balanceSheetStatements`/`otherLiab`  
> /`balanceSheetStatements`/`otherLiab`/`raw`  
> /`balanceSheetStatements`/`otherLiab`/`fmt`  
> /`balanceSheetStatements`/`otherLiab`/`longfmt`  
> 
> *Balance Sheets Statements Total Current Liabilities*  
> /`balanceSheetStatements`/`totalCurrentLiabilities`  
> /`balanceSheetStatements`/`totalCurrentLiabilities`/`raw`  
> /`balanceSheetStatements`/`totalCurrentLiabilities`/`fmt`  
> /`balanceSheetStatements`/`totalCurrentLiabilities`/`longfmt`  
> 
> *Balance Sheets Statements Total Liabilities*  
> /`balanceSheetStatements`/`totalLiab`  
> /`balanceSheetStatements`/`totalLiab`/`raw`  
> /`balanceSheetStatements`/`totalLiab`/`fmt`  
> /`balanceSheetStatements`/`totalLiab`/`longfmt`  
> 
> *Balance Sheets Statements Common Stock*  
> /`balanceSheetStatements`/`commonStock`  
> /`balanceSheetStatements`/`commonStock`/`raw`  
> /`balanceSheetStatements`/`commonStock`/`fmt`  
> /`balanceSheetStatements`/`commonStock`/`longfmt`  
> 
> *Balance Sheets Statements Retained Earnings*  
> /`balanceSheetStatements`/`retainedEarnings`  
> /`balanceSheetStatements`/`retainedEarnings`/`raw`  
> /`balanceSheetStatements`/`retainedEarnings`/`fmt`  
> /`balanceSheetStatements`/`retainedEarnings`/`longfmt`  
> 
> *Balance Sheets Statements Treasurey Stock*  
> /`balanceSheetStatements`/`treasuryStock`  
> /`balanceSheetStatements`/`treasuryStock`/`raw`  
> /`balanceSheetStatements`/`treasuryStock`/`fmt`  
> /`balanceSheetStatements`/`treasuryStock`/`longfmt`  
> 
> *Balance Sheets Statements Capital Surplus*  
> /`balanceSheetStatements`/`capitalSurplus`  
> /`balanceSheetStatements`/`capitalSurplus`/`raw`  
> /`balanceSheetStatements`/`capitalSurplus`/`fmt`  
> /`balanceSheetStatements`/`capitalSurplus`/`longfmt`  
> 
> *Balance Sheets Statements Other Stock Holder Equity*  
> /`balanceSheetStatements`/`otherStockholderEquity`  
> /`balanceSheetStatements`/`otherStockholderEquity`/`raw`  
> /`balanceSheetStatements`/`otherStockholderEquity`/`fmt`  
> /`balanceSheetStatements`/`otherStockholderEquity`/`longfmt`  
> 
> *Balance Sheets Statements Total Stock Holder Equity*  
> /`balanceSheetStatements`/`totalStockholderEquity`  
> /`balanceSheetStatements`/`totalStockholderEquity`/`raw`  
> /`balanceSheetStatements`/`totalStockholderEquity`/`fmt`  
> /`balanceSheetStatements`/`totalStockholderEquity`/`longfmt`  
> 
> *Balance Sheets Statements Net Tangible Assets*  
> /`balanceSheetStatements`/`netTangibleAssets`  
> /`balanceSheetStatements`/`netTangibleAssets`/`raw`  
> /`balanceSheetStatements`/`netTangibleAssets`/`fmt`  
> /`balanceSheetStatements`/`netTangibleAssets`/`longfmt`  
> 
> *Balance Sheets Statements Short Long Term Debt*  
> /`balanceSheetStatements`/`shortLongTermDebt`  
> /`balanceSheetStatements`/`shortLongTermDebt`/`raw`  
> /`balanceSheetStatements`/`shortLongTermDebt`/`fmt`  
> /`balanceSheetStatements`/`shortLongTermDebt`/`longfmt`
> 
> *Maximum number of seconds results of the balanceSheetHistoryQuarterly query can be cached*  
> /`maxAge`


## Calendar Events
The calendarEvents module displays data from the company's [Upcoming Earnings & Dividends](https://finance.yahoo.com/quote/AAPL/analysis?p=AAPL) (Growth Estimates)  

**Query:**  
`/quoteSummary/result/calendarEvents` + **Nested Data** (*optional*)  

**Nested Data:**  
> *Maximum number of seconds results of the calendarEvents query can be cached*  
> /`maxAge`  
> 
> *Upcoming Earnings (All Data)*  
> /`earnings`  
> 
> *Upcoming Earnings Date*  
> /`earnings`/`earningsDate`  
> /`earnings`/`earningsDate`/`raw`  
> /`earnings`/`earningsDate`/`fmt`  
> 
> *Upcoming Earnings Average*  
> /`earnings`/`earningsAverage`  
> /`earnings`/`earningsAverage`/`raw`  
> /`earnings`/`earningsAverage`/`fmt`  
> 
> *Upcoming Earnings Low*  
> /`earnings`/`earningsLow`  
> /`earnings`/`earningsLow`/`raw`  
> /`earnings`/`earningsLow`/`fmt`  
> 
> *Upcoming Earnings High*  
> /`earnings`/`earningsHigh`  
> /`earnings`/`earningsHigh`/`raw`  
> /`earnings`/`earningsHigh`/`fmt`  
> 
> *Upcoming Revenue Average*  
> /`earnings`/`revenueAverage`  
> /`earnings`/`revenueAverage`/`raw`  
> /`earnings`/`revenueAverage`/`fmt`  
> /`earnings`/`revenueAverage`/`longfmt`  
> 
> *Upcoming Revenue Low*  
> /`earnings`/`revenueLow`  
> /`earnings`/`revenueLow`/`raw`  
> /`earnings`/`revenueLow`/`fmt`  
> /`earnings`/`revenueLow`/`longfmt`  
> 
> *Upcoming Revenue High*  
> /`earnings`/`revenueHigh`  
> /`earnings`/`revenueHigh`/`raw`  
> /`earnings`/`revenueHigh`/`fmt`  
> /`earnings`/`revenueHigh`/`longfmt`  
> 
> *Upcoming Ex-dividend Date*  
> /`exDividendDate`  
> /`exDividendDate`/`raw`  
> /`exDividendDate`/`fmt`  
> 
> *Upcoming Dividend Date*  
> /`exDividendDate`  
> /`exDividendDate`/`raw`  
> /`exDividendDate`/`fmt`  


## Cash Flow Statement History (Annual)
The cashflowStatementHistory module displays data from the company's [Annual Cash Flow](https://finance.yahoo.com/quote/AAPL/cash-flow?p=AAPL) (*Navigate to Annual tab*)  
Learn more about financial statements on [Investopedia](https://www.investopedia.com/terms/f/financial-statements.asp)  
Learn more about cash flow on [Investopedia](https://www.investopedia.com/investing/read-corporate-cash-flow-statement/)  

**Query:**  
`/quoteSummary/result/cashflowStatementHistory` + **Nested Data** (*optional*)  

**Nested Data:**  
> *Cash Flow Statements (All Data)*  
> /`cashflowStatements`  
> 
> *Maximum number of seconds results of the cashflowStatements query can be cached*  
> /`cashflowStatements`/`maxAge`  
> 
> *Cash Flow Statements End Date*  
> /`cashflowStatements`/`endDate`  
> /`cashflowStatements`/`endDate`/`raw`  
> /`cashflowStatements`/`endDate`/`fmt`  
> 
> *Cash Flow Statements Net Income*  
> /`cashflowStatements`/`netIncome`  
> /`cashflowStatements`/`netIncome`/`raw`  
> /`cashflowStatements`/`netIncome`/`fmt`  
> /`cashflowStatements`/`netIncome`/`longfmt`  
> 
> *Cash Flow Statements Depreciation*  
> /`cashflowStatements`/`depreciation`  
> /`cashflowStatements`/`depreciation`/`raw`  
> /`cashflowStatements`/`depreciation`/`fmt`  
> /`cashflowStatements`/`depreciation`/`longfmt`  
> 
> *Cash Flow Statements change to Net Income*  
> /`cashflowStatements`/`changeToNetIncome`  
> /`cashflowStatements`/`changeToNetIncome`/`raw`  
> /`cashflowStatements`/`changeToNetIncome`/`fmt`  
> /`cashflowStatements`/`changeToNetIncome`/`longfmt`  
> 
> *Cash Flow Statements change to Accounts Receivables*  
> /`cashflowStatements`/`changeToAccountReceivables`  
> /`cashflowStatements`/`changeToAccountReceivables`/`raw`  
> /`cashflowStatements`/`changeToAccountReceivables`/`fmt`  
> /`cashflowStatements`/`changeToAccountReceivables`/`longfmt`  
> 
> *Cash Flow Statements change to Liabilities*  
> /`cashflowStatements`/`changeToLiabilities`  
> /`cashflowStatements`/`changeToLiabilities`/`raw`  
> /`cashflowStatements`/`changeToLiabilities`/`fmt`  
> /`cashflowStatements`/`changeToLiabilities`/`longfmt`  
> 
> *Cash Flow Statements change to Inventory*  
> /`cashflowStatements`/`changeToInventory`  
> /`cashflowStatements`/`changeToInventory`/`raw`  
> /`cashflowStatements`/`changeToInventory`/`fmt`  
> /`cashflowStatements`/`changeToInventory`/`longfmt`  
> 
> *Cash Flow Statements change to Operating Activities*  
> /`cashflowStatements`/`changeToOperatingActivities`  
> /`cashflowStatements`/`changeToOperatingActivities`/`raw`  
> /`cashflowStatements`/`changeToOperatingActivities`/`fmt`  
> /`cashflowStatements`/`changeToOperatingActivities`/`longfmt`  
> 
> *Cash Flow Statements Total Cash from Operating Activities*  
> /`cashflowStatements`/`totalCashFromOperatingActivities`  
> /`cashflowStatements`/`totalCashFromOperatingActivities`/`raw`  
> /`cashflowStatements`/`totalCashFromOperatingActivities`/`fmt`  
> /`cashflowStatements`/`totalCashFromOperatingActivities`/`longfmt`  
> 
> *Cash Flow Statements Capital Expenditures*  
> /`cashflowStatements`/`capitalExpenditures`  
> /`cashflowStatements`/`capitalExpenditures`/`raw`  
> /`cashflowStatements`/`capitalExpenditures`/`fmt`  
> /`cashflowStatements`/`capitalExpenditures`/`longfmt`  
> 
> *Cash Flow Statements Investments*  
> /`cashflowStatements`/`investments`  
> /`cashflowStatements`/`investments`/`raw`  
> /`cashflowStatements`/`investments`/`fmt`  
> /`cashflowStatements`/`investments`/`longfmt`  
> 
> *Cash Flow Statements Total Cash Flow from Investment Activites*  
> /`cashflowStatements`/`totalCashflowsFromInvestingActivities`  
> /`cashflowStatements`/`totalCashflowsFromInvestingActivities`/`raw`  
> /`cashflowStatements`/`totalCashflowsFromInvestingActivities`/`fmt`  
> /`cashflowStatements`/`totalCashflowsFromInvestingActivities`/`longfmt`  
> 
> *Cash Flow Statements Dividends Paid*  
> /`cashflowStatements`/`dividendsPaid`  
> /`cashflowStatements`/`dividendsPaid`/`raw`  
> /`cashflowStatements`/`dividendsPaid`/`fmt`  
> /`cashflowStatements`/`dividendsPaid`/`longfmt`  
> 
> *Cash Flow Statements Total Cash from Financing Activities*  
> /`cashflowStatements`/`totalCashFromFinancingActivities`  
> /`cashflowStatements`/`totalCashFromFinancingActivities`/`raw`  
> /`cashflowStatements`/`totalCashFromFinancingActivities`/`fmt`  
> /`cashflowStatements`/`totalCashFromFinancingActivities`/`longfmt`  
> 
> *Cash Flow Statements Change in Cash*  
> /`cashflowStatements`/`changeInCash`  
> /`cashflowStatements`/`changeInCash`/`raw`  
> /`cashflowStatements`/`changeInCash`/`fmt`  
> /`cashflowStatements`/`changeInCash`/`longfmt`  
> 
> *Cash Flow Statements Repurchase of Stock*  
> /`cashflowStatements`/`repurchaseOfStock`  
> /`cashflowStatements`/`repurchaseOfStock`/`raw`  
> /`cashflowStatements`/`repurchaseOfStock`/`fmt`  
> /`cashflowStatements`/`repurchaseOfStock`/`longfmt`  
> 
> *Cash Flow Statements Issuance of Stock*  
> /`cashflowStatements`/`issuanceOfStock`  
> /`cashflowStatements`/`issuanceOfStock`/`raw`  
> /`cashflowStatements`/`issuanceOfStock`/`fmt`  
> /`cashflowStatements`/`issuanceOfStock`/`longfmt`  
> 
> *Cash Flow Statements Net Borrowings*  
> /`cashflowStatements`/`netBorrowings`  
> /`cashflowStatements`/`netBorrowings`/`raw`  
> /`cashflowStatements`/`netBorrowings`/`fmt`  
> /`cashflowStatements`/`netBorrowings`/`longfmt`  
> 
> *Cash Flow Statements Other Cash Flows From Financing Activities*  
> /`cashflowStatements`/`otherCashflowsFromFinancingActivities`  
> /`cashflowStatements`/`otherCashflowsFromFinancingActivities`/`raw`  
> /`cashflowStatements`/`otherCashflowsFromFinancingActivities`/`fmt`  
> /`cashflowStatements`/`otherCashflowsFromFinancingActivities`/`longfmt`  
> 
> *Cash Flow Statements Other Cash Flows From Investing Activities*  
> /`cashflowStatements`/`otherCashflowsFromInvestingActivities`  
> /`cashflowStatements`/`otherCashflowsFromInvestingActivities`/`raw`  
> /`cashflowStatements`/`otherCashflowsFromInvestingActivities`/`fmt`  
> /`cashflowStatements`/`otherCashflowsFromInvestingActivities`/`longfmt`  
> 
> *Maximum number of seconds results of the cashflowStatementHistory query can be cached*  
> /`maxAge`  


## Cash Flow Statement History (Quarterly)
The cashflowStatementHistoryQuarterly module displays data from the company's [Quarterly Cash Flow](https://finance.yahoo.com/quote/AAPL/cash-flow?p=AAPL) (*Navigate to Quarterly tab*)  
Learn more about financial statements on [Investopedia](https://www.investopedia.com/terms/f/financial-statements.asp)  
Learn more about cash flow on [Investopedia](https://www.investopedia.com/investing/read-corporate-cash-flow-statement/)  

**Query:**  
`/quoteSummary/result/cashflowStatementHistoryQuarterly` + **Nested Data** (*optional*)  

**Nested Data:**  
> *Cash Flow Statements (All Data)*  
> /`cashflowStatements`  
> 
> *Maximum number of seconds results of the cashflowStatements query can be cached*  
> /`cashflowStatements`/`maxAge`  
> 
> *Cash Flow Statements End Date*  
> /`cashflowStatements`/`endDate`  
> /`cashflowStatements`/`endDate`/`raw`  
> /`cashflowStatements`/`endDate`/`fmt`  
> 
> *Cash Flow Statements Net Income*  
> /`cashflowStatements`/`netIncome`  
> /`cashflowStatements`/`netIncome`/`raw`  
> /`cashflowStatements`/`netIncome`/`fmt`  
> /`cashflowStatements`/`netIncome`/`longfmt`  
> 
> *Cash Flow Statements Depreciation*  
> /`cashflowStatements`/`depreciation`  
> /`cashflowStatements`/`depreciation`/`raw`  
> /`cashflowStatements`/`depreciation`/`fmt`  
> /`cashflowStatements`/`depreciation`/`longfmt`  
> 
> *Cash Flow Statements change to Net Income*  
> /`cashflowStatements`/`changeToNetIncome`  
> /`cashflowStatements`/`changeToNetIncome`/`raw`  
> /`cashflowStatements`/`changeToNetIncome`/`fmt`  
> /`cashflowStatements`/`changeToNetIncome`/`longfmt`  
> 
> *Cash Flow Statements change to Accounts Receivables*  
> /`cashflowStatements`/`changeToAccountReceivables`  
> /`cashflowStatements`/`changeToAccountReceivables`/`raw`  
> /`cashflowStatements`/`changeToAccountReceivables`/`fmt`  
> /`cashflowStatements`/`changeToAccountReceivables`/`longfmt`  
> 
> *Cash Flow Statements change to Liabilities*  
> /`cashflowStatements`/`changeToLiabilities`  
> /`cashflowStatements`/`changeToLiabilities`/`raw`  
> /`cashflowStatements`/`changeToLiabilities`/`fmt`  
> /`cashflowStatements`/`changeToLiabilities`/`longfmt`  
> 
> *Cash Flow Statements change to Inventory*  
> /`cashflowStatements`/`changeToInventory`  
> /`cashflowStatements`/`changeToInventory`/`raw`  
> /`cashflowStatements`/`changeToInventory`/`fmt`  
> /`cashflowStatements`/`changeToInventory`/`longfmt`  
> 
> *Cash Flow Statements change to Operating Activities*  
> /`cashflowStatements`/`changeToOperatingActivities`  
> /`cashflowStatements`/`changeToOperatingActivities`/`raw`  
> /`cashflowStatements`/`changeToOperatingActivities`/`fmt`  
> /`cashflowStatements`/`changeToOperatingActivities`/`longfmt`  
> 
> *Cash Flow Statements Total Cash from Operating Activities*  
> /`cashflowStatements`/`totalCashFromOperatingActivities`  
> /`cashflowStatements`/`totalCashFromOperatingActivities`/`raw`  
> /`cashflowStatements`/`totalCashFromOperatingActivities`/`fmt`  
> /`cashflowStatements`/`totalCashFromOperatingActivities`/`longfmt`  
> 
> *Cash Flow Statements Capital Expenditures*  
> /`cashflowStatements`/`capitalExpenditures`  
> /`cashflowStatements`/`capitalExpenditures`/`raw`  
> /`cashflowStatements`/`capitalExpenditures`/`fmt`  
> /`cashflowStatements`/`capitalExpenditures`/`longfmt`  
> 
> *Cash Flow Statements Investments*  
> /`cashflowStatements`/`investments`  
> /`cashflowStatements`/`investments`/`raw`  
> /`cashflowStatements`/`investments`/`fmt`  
> /`cashflowStatements`/`investments`/`longfmt`  
> 
> *Cash Flow Statements Total Cash Flow from Investment Activites*  
> /`cashflowStatements`/`totalCashflowsFromInvestingActivities`  
> /`cashflowStatements`/`totalCashflowsFromInvestingActivities`/`raw`  
> /`cashflowStatements`/`totalCashflowsFromInvestingActivities`/`fmt`  
> /`cashflowStatements`/`totalCashflowsFromInvestingActivities`/`longfmt`  
> 
> *Cash Flow Statements Dividends Paid*  
> /`cashflowStatements`/`dividendsPaid`  
> /`cashflowStatements`/`dividendsPaid`/`raw`  
> /`cashflowStatements`/`dividendsPaid`/`fmt`  
> /`cashflowStatements`/`dividendsPaid`/`longfmt`  
> 
> *Cash Flow Statements Total Cash from Financing Activities*  
> /`cashflowStatements`/`totalCashFromFinancingActivities`  
> /`cashflowStatements`/`totalCashFromFinancingActivities`/`raw`  
> /`cashflowStatements`/`totalCashFromFinancingActivities`/`fmt`  
> /`cashflowStatements`/`totalCashFromFinancingActivities`/`longfmt`  
> 
> *Cash Flow Statements Change in Cash*  
> /`cashflowStatements`/`changeInCash`  
> /`cashflowStatements`/`changeInCash`/`raw`  
> /`cashflowStatements`/`changeInCash`/`fmt`  
> /`cashflowStatements`/`changeInCash`/`longfmt`  
> 
> *Cash Flow Statements Repurchase of Stock*  
> /`cashflowStatements`/`repurchaseOfStock`  
> /`cashflowStatements`/`repurchaseOfStock`/`raw`  
> /`cashflowStatements`/`repurchaseOfStock`/`fmt`  
> /`cashflowStatements`/`repurchaseOfStock`/`longfmt`  
> 
> *Cash Flow Statements Issuance of Stock*  
> /`cashflowStatements`/`issuanceOfStock`  
> /`cashflowStatements`/`issuanceOfStock`/`raw`  
> /`cashflowStatements`/`issuanceOfStock`/`fmt`  
> /`cashflowStatements`/`issuanceOfStock`/`longfmt`  
> 
> *Cash Flow Statements Net Borrowings*  
> /`cashflowStatements`/`netBorrowings`  
> /`cashflowStatements`/`netBorrowings`/`raw`  
> /`cashflowStatements`/`netBorrowings`/`fmt`  
> /`cashflowStatements`/`netBorrowings`/`longfmt`  
> 
> *Cash Flow Statements Other Cash Flows From Financing Activities*  
> /`cashflowStatements`/`otherCashflowsFromFinancingActivities`  
> /`cashflowStatements`/`otherCashflowsFromFinancingActivities`/`raw`  
> /`cashflowStatements`/`otherCashflowsFromFinancingActivities`/`fmt`  
> /`cashflowStatements`/`otherCashflowsFromFinancingActivities`/`longfmt`  
> 
> *Cash Flow Statements Other Cash Flows From Investing Activities*  
> /`cashflowStatements`/`otherCashflowsFromInvestingActivities`  
> /`cashflowStatements`/`otherCashflowsFromInvestingActivities`/`raw`  
> /`cashflowStatements`/`otherCashflowsFromInvestingActivities`/`fmt`  
> /`cashflowStatements`/`otherCashflowsFromInvestingActivities`/`longfmt`  
> 
> *Maximum number of seconds results of the cashflowStatementHistory query can be cached*  
> /`maxAge`  


## Key Statistics
The defaultKeyStatistics module displays data from the company's [Statistics](https://finance.yahoo.com/quote/AAPL/cash-flow?p=AAPL)  
Learn more about performing a fundamental analysis of a company on [Investopedia](https://www.investopedia.com/terms/f/fundamentalanalysis.asp)  

**Query:**  
`/quoteSummary/result/defaultKeyStatistics` + **Nested Data** (*optional*)  

**Nested Data:**  
> *Maximum number of seconds results of the defaultKeyStatistics query can be cached*  
> /`maxAge`  
> 
> *Price Hint*  
> /`priceHint`  
> /`priceHint`/`raw`  
> /`priceHint`/`fmt`  
> /`priceHint`/`longfmt`  
> 
> *Enterprise Value*  
> /`enterpriseValue`  
> /`enterpriseValue`/`raw`  
> /`enterpriseValue`/`fmt`  
> /`enterpriseValue`/`longfmt`  
