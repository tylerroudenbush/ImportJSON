# Using ImportJSON to pull data from Yahoo Finance into Google Sheets
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
> =ImportJSON(`"http://query2.finance.yahoo.com/v10/finance/quoteSummary/"`&**A1**&`"?modules=defaultKeyStatistics","/quoteSummary/result/defaultKeyStatistics/price/raw","noInheret,noTruncate,noHeaders")`
  
  
  
  
# Modules
Yahoo Finance sorts company information into modules. Use the following table to locate the module containing data you're looking for.  

| Description | Module Name |
| ------------|------------ |
| [Asset Profile](#asset-profile) | assetProfile |
| [Balance Sheet History (Annual)](#balance-sheet-history-annual) | balanceSheetHistory |
| [Balance Sheet History (Quarterly)](#balance-sheet-history-quarterly) | balanceSheetHistoryQuarterly |
| [Calendar Events](#calendar-events) | calendarEvents |
| [Cash Flow Statement History (Annual)](#cash-flow-statement-history-annual) | cashflowStatementHistory |
| [Cash Flow Statement History (Quarterly)](#cash-flow-statement-history-quarterly) | cashflowStatementHistoryQuarterly |
| [Key Statistics](#key-statistics) | defaultKeyStatistics |
| [Earnings](#earnings) | earnings |
| [Earnings History](#earnings-history) | earningsHistory |
| [Earnings Trend](#earnings-trend) | earningsTrend
| [ESG Scores](#esg-scores) | esgScores |
| [Financial Data](#financial-data) | financialData |
| [Fund Ownership](#fund-ownership) | fundOwnership |
| [Income Statement History (Annual)](#income-statement-history-annual) | incomeStatementHistory |
| [Income Statement History (Quarterly)](#income-statement-history-quarterly) | incomeStatementHistoryQuarterly |
| [Index Trend](#index-trend) | indexTrend |
| [Industry Trend](#industry-trend) | indexTrend |
| [Insider Holders](#insider-holders) | insiderHolders |
| [Insider Transactions](#insider-transactions) | insiderTransactions |
| [Institution Ownership](#institution-ownership) | institutionOwnership |
| [Major Direct Holders](#major-direct-holders) | majorDirectHolders |
| [Major Holders Breakdown](#major-holders-breakdown) | majorHoldersBreakdown |
| [Net Share Purchase Activity](#net-share-purchase-activity) | netSharePurchaseActivity |
| [Page Views](#page-views) | pageViews |
| [Price](#price) | price |
| [Quote Type](#quote-type) | quoteType |
| [Recommendation Trend](#recommendation-trend) | recommendationTrend |
| [SEC Filings](#sec-filings) | secFilings |
| [Sector Trend](#sector-trend) | sectorTrend |
| [Summary Detail](#summary-detail) | summaryDetail |
| [Summary Profile](#summary-profile) | summaryProfile |
| [Upgrade Downgrade History](#upgrade-downgrade-history) | upgradeDowngradeHistory |


## Data Formats
Most modules will contain nested data that may be formatted in mutiple ways. If a specific format is not selected, all available data formats will be displayed.  

**Formatting**  
> /`raw` *(raw value only)*  
> /`fmt` *(formatted as truncated string)*  
> /`longfmt` *(formatted as string)*  


## Asset Profile
The **assetProfile** and module displays "Key Executives" data from the company's [Profile](https://finance.yahoo.com/quote/AAPL/profile?p=AAPL) page.  

**Query:**  
`/quoteSummary/result/assetProfile` + **Nested Data** (*optional*)  

**Nested Data:**  
> **Company Address: Street**  
> /`address1`  
> 
> **Company Address: City**  
> /`city`  
> 
> **Company Address: Zip Code**  
> /`zip`  
> 
> **Company Address: Country**  
> /`country`  
> 
> **Company Phone Number**  
> /`phone`  
> 
> **Company Fax**  
> /`fax`  
> 
> **Company Website**  
> /`website`  
> 
> **Company Market Industry**  
> /`industry`  
> 
> **Company Market Sector**  
> /`sector`  
> 
> **Company Business Summary**  
> /`longBusinessSummary`  
> 
> **Company Full-Time Employees**  
> /`fullTimeEmployees`  
> 
> **Company Officers**  
> /`companyOfficers`  
> 
> **Max Age** *Maximum number of seconds in which results from the assetProfile query can be cached*  
> /`maxAge`  


## Balance Sheet History (Annual)
The **balanceSheetHistory** module displays data from the company's [Annual Balance Sheet](https://finance.yahoo.com/quote/AAPL/balance-sheet?p=AAPL) page. (*Navigate to Annual tab*)  
Learn more about financial statements on [Investopedia](https://www.investopedia.com/terms/f/financial-statements.asp)  
Learn more about corporate balance sheets on [Investopedia](https://www.investopedia.com/articles/04/031004.asp/)  

**Query:**  
`/quoteSummary/result/balanceSheetHistory` + **Nested Data** (*optional*)  

**Nested Data:**  
> **Balance Sheet Statements (All Data)**  
> /`balanceSheetStatements`  
> 
> **Balance Sheet Statements Max Age** *Maximum number of seconds in which results from the balanceSheetStatements query can be cached*  
> /`balanceSheetStatements`/`maxAge`  
> 
> **Balance Sheet Statements End Date**  
> /`balanceSheetStatements`/`endDate`  
> /`balanceSheetStatements`/`endDate`/`raw`  
> /`balanceSheetStatements`/`endDate`/`fmt`  
> 
> **Balance Sheet Statements Cash**  
> /`balanceSheetStatements`/`cash`  
> /`balanceSheetStatements`/`cash`/`raw`  
> /`balanceSheetStatements`/`cash`/`fmt`  
> /`balanceSheetStatements`/`cash`/`longfmt`  
> 
> **Balance Sheet Statements Short Term Investments**  
> /`balanceSheetStatements`/`shortTermInvestments`  
> /`balanceSheetStatements`/`shortTermInvestments`/`raw`  
> /`balanceSheetStatements`/`shortTermInvestments`/`fmt`  
> /`balanceSheetStatements`/`shortTermInvestments`/`longfmt`  
> 
> **Balance Sheet Statements SNet Receivables**  
> /`balanceSheetStatements`/`netReceivables`  
> /`balanceSheetStatements`/`netReceivables`/`raw`  
> /`balanceSheetStatements`/`netReceivables`/`fmt`  
> /`balanceSheetStatements`/`netReceivables`/`longfmt`  
> 
> **Balance Sheet Statements Inventory**  
> /`balanceSheetStatements`/`inventory`  
> /`balanceSheetStatements`/`inventory`/`raw`  
> /`balanceSheetStatements`/`inventory`/`fmt`  
> /`balanceSheetStatements`/`inventory`/`longfmt`  
> 
> **Balance Sheet Statements Total Current Assets**  
> /`balanceSheetStatements`/`totalCurrentAssets`  
> /`balanceSheetStatements`/`totalCurrentAssets`/`raw`  
> /`balanceSheetStatements`/`totalCurrentAssets`/`fmt`  
> /`balanceSheetStatements`/`totalCurrentAssets`/`longfmt`  
> 
> **Balance Sheet Statements Property Plant Equipment**  
> /`balanceSheetStatements`/`propertyPlantEquipment`  
> /`balanceSheetStatements`/`propertyPlantEquipment`/`raw`  
> /`balanceSheetStatements`/`propertyPlantEquipment`/`fmt`  
> /`balanceSheetStatements`/`propertyPlantEquipment`/`longfmt`  
> 
> **Balance Sheet Statements Goodwill**  
> /`balanceSheetStatements`/`goodwill`  
> /`balanceSheetStatements`/`goodwill`/`raw`  
> /`balanceSheetStatements`/`goodwill`/`fmt`  
> /`balanceSheetStatements`/`goodwill`/`longfmt`  
> 
> **Balance Sheet Statements Intangible Assets**  
> /`balanceSheetStatements`/`intangibleAssets`  
> /`balanceSheetStatements`/`intangibleAssets`/`raw`  
> /`balanceSheetStatements`/`intangibleAssets`/`fmt`  
> /`balanceSheetStatements`/`intangibleAssets`/`longfmt`  
> 
> **Balance Sheet Statements Other Assets**  
> /`balanceSheetStatements`/`otherAssets`  
> /`balanceSheetStatements`/`otherAssets`/`raw`  
> /`balanceSheetStatements`/`otherAssets`/`fmt`  
> /`balanceSheetStatements`/`otherAssets`/`longfmt`  
> 
> **Balance Sheet Statements Deferred Long Term Asset Charges**  
> /`balanceSheetStatements`/`deferredLongTermAssetCharges`  
> /`balanceSheetStatements`/`deferredLongTermAssetCharges`/`raw`  
> /`balanceSheetStatements`/`deferredLongTermAssetCharges`/`fmt`  
> /`balanceSheetStatements`/`deferredLongTermAssetCharges`/`longfmt`  
> 
> **Balance Sheet Statements Total Assets**  
> /`balanceSheetStatements`/`totalAssets`  
> /`balanceSheetStatements`/`totalAssets`/`raw`  
> /`balanceSheetStatements`/`totalAssets`/`fmt`  
> /`balanceSheetStatements`/`totalAssets`/`longfmt`  
> 
> **Balance Sheet Statements Accounts Payable**  
> /`balanceSheetStatements`/`accountsPayable`  
> /`balanceSheetStatements`/`accountsPayable`/`raw`  
> /`balanceSheetStatements`/`accountsPayable`/`fmt`  
> /`balanceSheetStatements`/`accountsPayable`/`longfmt`  
> 
> **Balance Sheet Statements Other Current Liabilities**  
> /`balanceSheetStatements`/`otherCurrentLiab`  
> /`balanceSheetStatements`/`otherCurrentLiab`/`raw`  
> /`balanceSheetStatements`/`otherCurrentLiab`/`fmt`  
> /`balanceSheetStatements`/`otherCurrentLiab`/`longfmt`  
> 
> **Balance Sheet Statements Long Term Debt**  
> /`balanceSheetStatements`/`longTermDebt`  
> /`balanceSheetStatements`/`longTermDebt`/`raw`  
> /`balanceSheetStatements`/`longTermDebt`/`fmt`  
> /`balanceSheetStatements`/`longTermDebt`/`longfmt`  
> 
> **Balance Sheet Statements Other Liabilities**  
> /`balanceSheetStatements`/`otherLiab`  
> /`balanceSheetStatements`/`otherLiab`/`raw`  
> /`balanceSheetStatements`/`otherLiab`/`fmt`  
> /`balanceSheetStatements`/`otherLiab`/`longfmt`  
> 
> **Balance Sheet Statements Total Current Liabilities**  
> /`balanceSheetStatements`/`totalCurrentLiabilities`  
> /`balanceSheetStatements`/`totalCurrentLiabilities`/`raw`  
> /`balanceSheetStatements`/`totalCurrentLiabilities`/`fmt`  
> /`balanceSheetStatements`/`totalCurrentLiabilities`/`longfmt`  
> 
> **Balance Sheet Statements Total Liabilities**  
> /`balanceSheetStatements`/`totalLiab`  
> /`balanceSheetStatements`/`totalLiab`/`raw`  
> /`balanceSheetStatements`/`totalLiab`/`fmt`  
> /`balanceSheetStatements`/`totalLiab`/`longfmt`  
> 
> **Balance Sheet Statements Common Stock**  
> /`balanceSheetStatements`/`commonStock`  
> /`balanceSheetStatements`/`commonStock`/`raw`  
> /`balanceSheetStatements`/`commonStock`/`fmt`  
> /`balanceSheetStatements`/`commonStock`/`longfmt`  
> 
> **Balance Sheet Statements Retained Earnings**  
> /`balanceSheetStatements`/`retainedEarnings`  
> /`balanceSheetStatements`/`retainedEarnings`/`raw`  
> /`balanceSheetStatements`/`retainedEarnings`/`fmt`  
> /`balanceSheetStatements`/`retainedEarnings`/`longfmt`  
> 
> **Balance Sheet Statements Treasurey Stock**  
> /`balanceSheetStatements`/`treasuryStock`  
> /`balanceSheetStatements`/`treasuryStock`/`raw`  
> /`balanceSheetStatements`/`treasuryStock`/`fmt`  
> /`balanceSheetStatements`/`treasuryStock`/`longfmt`  
> 
> **Balance Sheet Statements Capital Surplus**  
> /`balanceSheetStatements`/`capitalSurplus`  
> /`balanceSheetStatements`/`capitalSurplus`/`raw`  
> /`balanceSheetStatements`/`capitalSurplus`/`fmt`  
> /`balanceSheetStatements`/`capitalSurplus`/`longfmt`  
> 
> **Balance Sheet Statements Other Stock Holder Equity**  
> /`balanceSheetStatements`/`otherStockholderEquity`  
> /`balanceSheetStatements`/`otherStockholderEquity`/`raw`  
> /`balanceSheetStatements`/`otherStockholderEquity`/`fmt`  
> /`balanceSheetStatements`/`otherStockholderEquity`/`longfmt`  
> 
> **Balance Sheet Statements Total Stock Holder Equity**  
> /`balanceSheetStatements`/`totalStockholderEquity`  
> /`balanceSheetStatements`/`totalStockholderEquity`/`raw`  
> /`balanceSheetStatements`/`totalStockholderEquity`/`fmt`  
> /`balanceSheetStatements`/`totalStockholderEquity`/`longfmt`  
> 
> **Balance Sheet Statements Net Tangible Assets**  
> /`balanceSheetStatements`/`netTangibleAssets`  
> /`balanceSheetStatements`/`netTangibleAssets`/`raw`  
> /`balanceSheetStatements`/`netTangibleAssets`/`fmt`  
> /`balanceSheetStatements`/`netTangibleAssets`/`longfmt`  
> 
> **Balance Sheet Statements Short Long Term Debt**  
> /`balanceSheetStatements`/`shortLongTermDebt`  
> /`balanceSheetStatements`/`shortLongTermDebt`/`raw`  
> /`balanceSheetStatements`/`shortLongTermDebt`/`fmt`  
> /`balanceSheetStatements`/`shortLongTermDebt`/`longfmt`
> 
> **Max Age** *Maximum number of seconds in which results from the Balance Sheets History query can be cached*  
> /`maxAge`


## Balance Sheet History (Quarterly)
The **balanceSheetHistory** module displays data from the company's [Quarterly Balance Sheet](https://finance.yahoo.com/quote/AAPL/balance-sheet?p=AAPL) page. (*Navigate to Quarterly tab*)  
Learn more about financial statements on [Investopedia](https://www.investopedia.com/terms/f/financial-statements.asp)  
Learn more about corporate balance sheets on [Investopedia](https://www.investopedia.com/articles/04/031004.asp/)  

**Query:**  
`/quoteSummary/result/balanceSheetHistoryQuarterly` + **Nested Data** (*optional*)  

**Nested Data:**  
> **Balance Sheet Statements (All Data)**  
> /`balanceSheetStatements`  
> 
> **Balance Sheet Statements Max Age** *Maximum number of seconds in which results from the balanceSheetsStatements query can be cached*  
> /`balanceSheetStatements`/`maxAge`  
> 
> **Balance Sheet Statements End Date**  
> /`balanceSheetStatements`/`endDate`  
> /`balanceSheetStatements`/`endDate`/`raw`  
> /`balanceSheetStatements`/`endDate`/`fmt`  
> 
> **Balance Sheet Statements Cash**  
> /`balanceSheetStatements`/`cash`  
> /`balanceSheetStatements`/`cash`/`raw`  
> /`balanceSheetStatements`/`cash`/`fmt`  
> /`balanceSheetStatements`/`cash`/`longfmt`  
> 
> **Balance Sheet Statements Short Term Investments**  
> /`balanceSheetStatements`/`shortTermInvestments`  
> /`balanceSheetStatements`/`shortTermInvestments`/`raw`  
> /`balanceSheetStatements`/`shortTermInvestments`/`fmt`  
> /`balanceSheetStatements`/`shortTermInvestments`/`longfmt`  
> 
> **Balance Sheet Statements SNet Receivables**  
> /`balanceSheetStatements`/`netReceivables`  
> /`balanceSheetStatements`/`netReceivables`/`raw`  
> /`balanceSheetStatements`/`netReceivables`/`fmt`  
> /`balanceSheetStatements`/`netReceivables`/`longfmt`  
> 
> **Balance Sheet Statements Inventory**  
> /`balanceSheetStatements`/`inventory`  
> /`balanceSheetStatements`/`inventory`/`raw`  
> /`balanceSheetStatements`/`inventory`/`fmt`  
> /`balanceSheetStatements`/`inventory`/`longfmt`  
> 
> **Balance Sheet Statements Total Current Assets**  
> /`balanceSheetStatements`/`totalCurrentAssets`  
> /`balanceSheetStatements`/`totalCurrentAssets`/`raw`  
> /`balanceSheetStatements`/`totalCurrentAssets`/`fmt`  
> /`balanceSheetStatements`/`totalCurrentAssets`/`longfmt`  
> 
> **Balance Sheet Statements Property Plant Equipment**  
> /`balanceSheetStatements`/`propertyPlantEquipment`  
> /`balanceSheetStatements`/`propertyPlantEquipment`/`raw`  
> /`balanceSheetStatements`/`propertyPlantEquipment`/`fmt`  
> /`balanceSheetStatements`/`propertyPlantEquipment`/`longfmt`  
> 
> **Balance Sheet Statements Goodwill**  
> /`balanceSheetStatements`/`goodwill`  
> /`balanceSheetStatements`/`goodwill`/`raw`  
> /`balanceSheetStatements`/`goodwill`/`fmt`  
> /`balanceSheetStatements`/`goodwill`/`longfmt`  
> 
> **Balance Sheet Statements Intangible Assets**  
> /`balanceSheetStatements`/`intangibleAssets`  
> /`balanceSheetStatements`/`intangibleAssets`/`raw`  
> /`balanceSheetStatements`/`intangibleAssets`/`fmt`  
> /`balanceSheetStatements`/`intangibleAssets`/`longfmt`  
> 
> **Balance Sheet Statements Other Assets**  
> /`balanceSheetStatements`/`otherAssets`  
> /`balanceSheetStatements`/`otherAssets`/`raw`  
> /`balanceSheetStatements`/`otherAssets`/`fmt`  
> /`balanceSheetStatements`/`otherAssets`/`longfmt`  
> 
> **Balance Sheet Statements Deferred Long Term Asset Charges**  
> /`balanceSheetStatements`/`deferredLongTermAssetCharges`  
> /`balanceSheetStatements`/`deferredLongTermAssetCharges`/`raw`  
> /`balanceSheetStatements`/`deferredLongTermAssetCharges`/`fmt`  
> /`balanceSheetStatements`/`deferredLongTermAssetCharges`/`longfmt`  
> 
> **Balance Sheet Statements Total Assets**  
> /`balanceSheetStatements`/`totalAssets`  
> /`balanceSheetStatements`/`totalAssets`/`raw`  
> /`balanceSheetStatements`/`totalAssets`/`fmt`  
> /`balanceSheetStatements`/`totalAssets`/`longfmt`  
> 
> **Balance Sheet Statements Accounts Payable**  
> /`balanceSheetStatements`/`accountsPayable`  
> /`balanceSheetStatements`/`accountsPayable`/`raw`  
> /`balanceSheetStatements`/`accountsPayable`/`fmt`  
> /`balanceSheetStatements`/`accountsPayable`/`longfmt`  
> 
> **Balance Sheet Statements Other Current Liabilities**  
> /`balanceSheetStatements`/`otherCurrentLiab`  
> /`balanceSheetStatements`/`otherCurrentLiab`/`raw`  
> /`balanceSheetStatements`/`otherCurrentLiab`/`fmt`  
> /`balanceSheetStatements`/`otherCurrentLiab`/`longfmt`  
> 
> **Balance Sheet Statements Long Term Debt**  
> /`balanceSheetStatements`/`longTermDebt`  
> /`balanceSheetStatements`/`longTermDebt`/`raw`  
> /`balanceSheetStatements`/`longTermDebt`/`fmt`  
> /`balanceSheetStatements`/`longTermDebt`/`longfmt`  
> 
> **Balance Sheet Statements Other Liabilities**  
> /`balanceSheetStatements`/`otherLiab`  
> /`balanceSheetStatements`/`otherLiab`/`raw`  
> /`balanceSheetStatements`/`otherLiab`/`fmt`  
> /`balanceSheetStatements`/`otherLiab`/`longfmt`  
> 
> **Balance Sheet Statements Total Current Liabilities**  
> /`balanceSheetStatements`/`totalCurrentLiabilities`  
> /`balanceSheetStatements`/`totalCurrentLiabilities`/`raw`  
> /`balanceSheetStatements`/`totalCurrentLiabilities`/`fmt`  
> /`balanceSheetStatements`/`totalCurrentLiabilities`/`longfmt`  
> 
> **Balance Sheet Statements Total Liabilities**  
> /`balanceSheetStatements`/`totalLiab`  
> /`balanceSheetStatements`/`totalLiab`/`raw`  
> /`balanceSheetStatements`/`totalLiab`/`fmt`  
> /`balanceSheetStatements`/`totalLiab`/`longfmt`  
> 
> **Balance Sheet Statements Common Stock**  
> /`balanceSheetStatements`/`commonStock`  
> /`balanceSheetStatements`/`commonStock`/`raw`  
> /`balanceSheetStatements`/`commonStock`/`fmt`  
> /`balanceSheetStatements`/`commonStock`/`longfmt`  
> 
> **Balance Sheet Statements Retained Earnings**  
> /`balanceSheetStatements`/`retainedEarnings`  
> /`balanceSheetStatements`/`retainedEarnings`/`raw`  
> /`balanceSheetStatements`/`retainedEarnings`/`fmt`  
> /`balanceSheetStatements`/`retainedEarnings`/`longfmt`  
> 
> **Balance Sheet Statements Treasurey Stock**  
> /`balanceSheetStatements`/`treasuryStock`  
> /`balanceSheetStatements`/`treasuryStock`/`raw`  
> /`balanceSheetStatements`/`treasuryStock`/`fmt`  
> /`balanceSheetStatements`/`treasuryStock`/`longfmt`  
> 
> **Balance Sheet Statements Capital Surplus**  
> /`balanceSheetStatements`/`capitalSurplus`  
> /`balanceSheetStatements`/`capitalSurplus`/`raw`  
> /`balanceSheetStatements`/`capitalSurplus`/`fmt`  
> /`balanceSheetStatements`/`capitalSurplus`/`longfmt`  
> 
> **Balance Sheet Statements Other Stock Holder Equity**  
> /`balanceSheetStatements`/`otherStockholderEquity`  
> /`balanceSheetStatements`/`otherStockholderEquity`/`raw`  
> /`balanceSheetStatements`/`otherStockholderEquity`/`fmt`  
> /`balanceSheetStatements`/`otherStockholderEquity`/`longfmt`  
> 
> **Balance Sheet Statements Total Stock Holder Equity**  
> /`balanceSheetStatements`/`totalStockholderEquity`  
> /`balanceSheetStatements`/`totalStockholderEquity`/`raw`  
> /`balanceSheetStatements`/`totalStockholderEquity`/`fmt`  
> /`balanceSheetStatements`/`totalStockholderEquity`/`longfmt`  
> 
> **Balance Sheet Statements Net Tangible Assets**  
> /`balanceSheetStatements`/`netTangibleAssets`  
> /`balanceSheetStatements`/`netTangibleAssets`/`raw`  
> /`balanceSheetStatements`/`netTangibleAssets`/`fmt`  
> /`balanceSheetStatements`/`netTangibleAssets`/`longfmt`  
> 
> **Balance Sheet Statements Short Long Term Debt**  
> /`balanceSheetStatements`/`shortLongTermDebt`  
> /`balanceSheetStatements`/`shortLongTermDebt`/`raw`  
> /`balanceSheetStatements`/`shortLongTermDebt`/`fmt`  
> /`balanceSheetStatements`/`shortLongTermDebt`/`longfmt`
> 
> **Max Age** *Maximum number of seconds in which results from the balanceSheetHistoryQuarterly query can be cached*  
> /`maxAge`


## Calendar Events
The **calendarEvents** module displays data from the company's [Upcoming Earnings & Dividends](https://finance.yahoo.com/quote/AAPL/analysis?p=AAPL) page. (Growth Estimates)  

**Query:**  
`/quoteSummary/result/calendarEvents` + **Nested Data** (*optional*)  

**Nested Data:**  
> **Max Age** *Maximum number of seconds in which results from the calendarEvents query can be cached*  
> /`maxAge`  
> 
> **Upcoming Earnings (All Data)**  
> /`earnings`  
> 
> **Upcoming Earnings Date**  
> /`earnings`/`earningsDate`  
> /`earnings`/`earningsDate`/`raw`  
> /`earnings`/`earningsDate`/`fmt`  
> 
> **Upcoming Earnings Average**  
> /`earnings`/`earningsAverage`  
> /`earnings`/`earningsAverage`/`raw`  
> /`earnings`/`earningsAverage`/`fmt`  
> 
> **Upcoming Earnings Low**  
> /`earnings`/`earningsLow`  
> /`earnings`/`earningsLow`/`raw`  
> /`earnings`/`earningsLow`/`fmt`  
> 
> **Upcoming Earnings High**  
> /`earnings`/`earningsHigh`  
> /`earnings`/`earningsHigh`/`raw`  
> /`earnings`/`earningsHigh`/`fmt`  
> 
> **Upcoming Revenue Average**  
> /`earnings`/`revenueAverage`  
> /`earnings`/`revenueAverage`/`raw`  
> /`earnings`/`revenueAverage`/`fmt`  
> /`earnings`/`revenueAverage`/`longfmt`  
> 
> **Upcoming Revenue Low**  
> /`earnings`/`revenueLow`  
> /`earnings`/`revenueLow`/`raw`  
> /`earnings`/`revenueLow`/`fmt`  
> /`earnings`/`revenueLow`/`longfmt`  
> 
> **Upcoming Revenue High**  
> /`earnings`/`revenueHigh`  
> /`earnings`/`revenueHigh`/`raw`  
> /`earnings`/`revenueHigh`/`fmt`  
> /`earnings`/`revenueHigh`/`longfmt`  
> 
> **Upcoming Ex-dividend Date**  
> /`exDividendDate`  
> /`exDividendDate`/`raw`  
> /`exDividendDate`/`fmt`  
> 
> **Upcoming Dividend Date**  
> /`exDividendDate`  
> /`exDividendDate`/`raw`  
> /`exDividendDate`/`fmt`  


## Cash Flow Statement History (Annual)
The **cashflowStatementHistory** module displays data from the company's [Annual Cash Flow](https://finance.yahoo.com/quote/AAPL/cash-flow?p=AAPL) page. (*Navigate to Annual tab*)  
Learn more about financial statements on [Investopedia](https://www.investopedia.com/terms/f/financial-statements.asp)  
Learn more about cash flow on [Investopedia](https://www.investopedia.com/investing/read-corporate-cash-flow-statement/)  

**Query:**  
`/quoteSummary/result/cashflowStatementHistory` + **Nested Data** (*optional*)  

**Nested Data:**  
> **Cash Flow Statements (All Data)**  
> /`cashflowStatements`  
> 
> **Cash Flow Statements Max Age** *Maximum number of seconds in which results from the cashflowStatements query can be cached*  
> /`cashflowStatements`/`maxAge`  
> 
> **Cash Flow Statements End Date**  
> /`cashflowStatements`/`endDate`  
> /`cashflowStatements`/`endDate`/`raw`  
> /`cashflowStatements`/`endDate`/`fmt`  
> 
> **Cash Flow Statements Net Income**  
> /`cashflowStatements`/`netIncome`  
> /`cashflowStatements`/`netIncome`/`raw`  
> /`cashflowStatements`/`netIncome`/`fmt`  
> /`cashflowStatements`/`netIncome`/`longfmt`  
> 
> **Cash Flow Statements Depreciation**  
> /`cashflowStatements`/`depreciation`  
> /`cashflowStatements`/`depreciation`/`raw`  
> /`cashflowStatements`/`depreciation`/`fmt`  
> /`cashflowStatements`/`depreciation`/`longfmt`  
> 
> **Cash Flow Statements change to Net Income**  
> /`cashflowStatements`/`changeToNetIncome`  
> /`cashflowStatements`/`changeToNetIncome`/`raw`  
> /`cashflowStatements`/`changeToNetIncome`/`fmt`  
> /`cashflowStatements`/`changeToNetIncome`/`longfmt`  
> 
> **Cash Flow Statements change to Accounts Receivables**  
> /`cashflowStatements`/`changeToAccountReceivables`  
> /`cashflowStatements`/`changeToAccountReceivables`/`raw`  
> /`cashflowStatements`/`changeToAccountReceivables`/`fmt`  
> /`cashflowStatements`/`changeToAccountReceivables`/`longfmt`  
> 
> **Cash Flow Statements change to Liabilities**  
> /`cashflowStatements`/`changeToLiabilities`  
> /`cashflowStatements`/`changeToLiabilities`/`raw`  
> /`cashflowStatements`/`changeToLiabilities`/`fmt`  
> /`cashflowStatements`/`changeToLiabilities`/`longfmt`  
> 
> **Cash Flow Statements change to Inventory**  
> /`cashflowStatements`/`changeToInventory`  
> /`cashflowStatements`/`changeToInventory`/`raw`  
> /`cashflowStatements`/`changeToInventory`/`fmt`  
> /`cashflowStatements`/`changeToInventory`/`longfmt`  
> 
> **Cash Flow Statements change to Operating Activities**  
> /`cashflowStatements`/`changeToOperatingActivities`  
> /`cashflowStatements`/`changeToOperatingActivities`/`raw`  
> /`cashflowStatements`/`changeToOperatingActivities`/`fmt`  
> /`cashflowStatements`/`changeToOperatingActivities`/`longfmt`  
> 
> **Cash Flow Statements Total Cash from Operating Activities**  
> /`cashflowStatements`/`totalCashFromOperatingActivities`  
> /`cashflowStatements`/`totalCashFromOperatingActivities`/`raw`  
> /`cashflowStatements`/`totalCashFromOperatingActivities`/`fmt`  
> /`cashflowStatements`/`totalCashFromOperatingActivities`/`longfmt`  
> 
> **Cash Flow Statements Capital Expenditures**  
> /`cashflowStatements`/`capitalExpenditures`  
> /`cashflowStatements`/`capitalExpenditures`/`raw`  
> /`cashflowStatements`/`capitalExpenditures`/`fmt`  
> /`cashflowStatements`/`capitalExpenditures`/`longfmt`  
> 
> **Cash Flow Statements Investments**  
> /`cashflowStatements`/`investments`  
> /`cashflowStatements`/`investments`/`raw`  
> /`cashflowStatements`/`investments`/`fmt`  
> /`cashflowStatements`/`investments`/`longfmt`  
> 
> **Cash Flow Statements Total Cash Flow from Investment Activites**  
> /`cashflowStatements`/`totalCashflowsFromInvestingActivities`  
> /`cashflowStatements`/`totalCashflowsFromInvestingActivities`/`raw`  
> /`cashflowStatements`/`totalCashflowsFromInvestingActivities`/`fmt`  
> /`cashflowStatements`/`totalCashflowsFromInvestingActivities`/`longfmt`  
> 
> **Cash Flow Statements Dividends Paid**  
> /`cashflowStatements`/`dividendsPaid`  
> /`cashflowStatements`/`dividendsPaid`/`raw`  
> /`cashflowStatements`/`dividendsPaid`/`fmt`  
> /`cashflowStatements`/`dividendsPaid`/`longfmt`  
> 
> **Cash Flow Statements Total Cash from Financing Activities**  
> /`cashflowStatements`/`totalCashFromFinancingActivities`  
> /`cashflowStatements`/`totalCashFromFinancingActivities`/`raw`  
> /`cashflowStatements`/`totalCashFromFinancingActivities`/`fmt`  
> /`cashflowStatements`/`totalCashFromFinancingActivities`/`longfmt`  
> 
> **Cash Flow Statements Change in Cash**  
> /`cashflowStatements`/`changeInCash`  
> /`cashflowStatements`/`changeInCash`/`raw`  
> /`cashflowStatements`/`changeInCash`/`fmt`  
> /`cashflowStatements`/`changeInCash`/`longfmt`  
> 
> **Cash Flow Statements Repurchase of Stock**  
> /`cashflowStatements`/`repurchaseOfStock`  
> /`cashflowStatements`/`repurchaseOfStock`/`raw`  
> /`cashflowStatements`/`repurchaseOfStock`/`fmt`  
> /`cashflowStatements`/`repurchaseOfStock`/`longfmt`  
> 
> **Cash Flow Statements Issuance of Stock**  
> /`cashflowStatements`/`issuanceOfStock`  
> /`cashflowStatements`/`issuanceOfStock`/`raw`  
> /`cashflowStatements`/`issuanceOfStock`/`fmt`  
> /`cashflowStatements`/`issuanceOfStock`/`longfmt`  
> 
> **Cash Flow Statements Net Borrowings**  
> /`cashflowStatements`/`netBorrowings`  
> /`cashflowStatements`/`netBorrowings`/`raw`  
> /`cashflowStatements`/`netBorrowings`/`fmt`  
> /`cashflowStatements`/`netBorrowings`/`longfmt`  
> 
> **Cash Flow Statements Other Cash Flows From Financing Activities**  
> /`cashflowStatements`/`otherCashflowsFromFinancingActivities`  
> /`cashflowStatements`/`otherCashflowsFromFinancingActivities`/`raw`  
> /`cashflowStatements`/`otherCashflowsFromFinancingActivities`/`fmt`  
> /`cashflowStatements`/`otherCashflowsFromFinancingActivities`/`longfmt`  
> 
> **Cash Flow Statements Other Cash Flows From Investing Activities**  
> /`cashflowStatements`/`otherCashflowsFromInvestingActivities`  
> /`cashflowStatements`/`otherCashflowsFromInvestingActivities`/`raw`  
> /`cashflowStatements`/`otherCashflowsFromInvestingActivities`/`fmt`  
> /`cashflowStatements`/`otherCashflowsFromInvestingActivities`/`longfmt`  
> 
> **Max Age** *Maximum number of seconds in which results from the cashflowStatementHistory query can be cached*  
> /`maxAge`  


## Cash Flow Statement History (Quarterly)
The **cashflowStatementHistoryQuarterly** module displays data from the company's [Quarterly Cash Flow](https://finance.yahoo.com/quote/AAPL/cash-flow?p=AAPL) page. (*Navigate to Quarterly tab*)  
Learn more about financial statements on [Investopedia](https://www.investopedia.com/terms/f/financial-statements.asp)  
Learn more about cash flow on [Investopedia](https://www.investopedia.com/investing/read-corporate-cash-flow-statement/)  

**Query:**  
`/quoteSummary/result/cashflowStatementHistoryQuarterly` + **Nested Data** (*optional*)  

**Nested Data:**  
> **Cash Flow Statements (All Data)**  
> /`cashflowStatements`  
> 
> **Cash Flow Statements Max Age** *Maximum number of seconds in which results from the cashflowStatements query can be cached*  
> /`cashflowStatements`/`maxAge`  
> 
> **Cash Flow Statements End Date**  
> /`cashflowStatements`/`endDate`  
> /`cashflowStatements`/`endDate`/`raw`  
> /`cashflowStatements`/`endDate`/`fmt`  
> 
> **Cash Flow Statements Net Income**  
> /`cashflowStatements`/`netIncome`  
> /`cashflowStatements`/`netIncome`/`raw`  
> /`cashflowStatements`/`netIncome`/`fmt`  
> /`cashflowStatements`/`netIncome`/`longfmt`  
> 
> **Cash Flow Statements Depreciation**  
> /`cashflowStatements`/`depreciation`  
> /`cashflowStatements`/`depreciation`/`raw`  
> /`cashflowStatements`/`depreciation`/`fmt`  
> /`cashflowStatements`/`depreciation`/`longfmt`  
> 
> **Cash Flow Statements change to Net Income**  
> /`cashflowStatements`/`changeToNetIncome`  
> /`cashflowStatements`/`changeToNetIncome`/`raw`  
> /`cashflowStatements`/`changeToNetIncome`/`fmt`  
> /`cashflowStatements`/`changeToNetIncome`/`longfmt`  
> 
> **Cash Flow Statements change to Accounts Receivables**  
> /`cashflowStatements`/`changeToAccountReceivables`  
> /`cashflowStatements`/`changeToAccountReceivables`/`raw`  
> /`cashflowStatements`/`changeToAccountReceivables`/`fmt`  
> /`cashflowStatements`/`changeToAccountReceivables`/`longfmt`  
> 
> **Cash Flow Statements change to Liabilities**  
> /`cashflowStatements`/`changeToLiabilities`  
> /`cashflowStatements`/`changeToLiabilities`/`raw`  
> /`cashflowStatements`/`changeToLiabilities`/`fmt`  
> /`cashflowStatements`/`changeToLiabilities`/`longfmt`  
> 
> **Cash Flow Statements change to Inventory**  
> /`cashflowStatements`/`changeToInventory`  
> /`cashflowStatements`/`changeToInventory`/`raw`  
> /`cashflowStatements`/`changeToInventory`/`fmt`  
> /`cashflowStatements`/`changeToInventory`/`longfmt`  
> 
> **Cash Flow Statements change to Operating Activities**  
> /`cashflowStatements`/`changeToOperatingActivities`  
> /`cashflowStatements`/`changeToOperatingActivities`/`raw`  
> /`cashflowStatements`/`changeToOperatingActivities`/`fmt`  
> /`cashflowStatements`/`changeToOperatingActivities`/`longfmt`  
> 
> **Cash Flow Statements Total Cash from Operating Activities**  
> /`cashflowStatements`/`totalCashFromOperatingActivities`  
> /`cashflowStatements`/`totalCashFromOperatingActivities`/`raw`  
> /`cashflowStatements`/`totalCashFromOperatingActivities`/`fmt`  
> /`cashflowStatements`/`totalCashFromOperatingActivities`/`longfmt`  
> 
> **Cash Flow Statements Capital Expenditures**  
> /`cashflowStatements`/`capitalExpenditures`  
> /`cashflowStatements`/`capitalExpenditures`/`raw`  
> /`cashflowStatements`/`capitalExpenditures`/`fmt`  
> /`cashflowStatements`/`capitalExpenditures`/`longfmt`  
> 
> **Cash Flow Statements Investments**  
> /`cashflowStatements`/`investments`  
> /`cashflowStatements`/`investments`/`raw`  
> /`cashflowStatements`/`investments`/`fmt`  
> /`cashflowStatements`/`investments`/`longfmt`  
> 
> **Cash Flow Statements Total Cash Flow from Investment Activites**  
> /`cashflowStatements`/`totalCashflowsFromInvestingActivities`  
> /`cashflowStatements`/`totalCashflowsFromInvestingActivities`/`raw`  
> /`cashflowStatements`/`totalCashflowsFromInvestingActivities`/`fmt`  
> /`cashflowStatements`/`totalCashflowsFromInvestingActivities`/`longfmt`  
> 
> **Cash Flow Statements Dividends Paid**  
> /`cashflowStatements`/`dividendsPaid`  
> /`cashflowStatements`/`dividendsPaid`/`raw`  
> /`cashflowStatements`/`dividendsPaid`/`fmt`  
> /`cashflowStatements`/`dividendsPaid`/`longfmt`  
> 
> **Cash Flow Statements Total Cash from Financing Activities**  
> /`cashflowStatements`/`totalCashFromFinancingActivities`  
> /`cashflowStatements`/`totalCashFromFinancingActivities`/`raw`  
> /`cashflowStatements`/`totalCashFromFinancingActivities`/`fmt`  
> /`cashflowStatements`/`totalCashFromFinancingActivities`/`longfmt`  
> 
> **Cash Flow Statements Change in Cash**  
> /`cashflowStatements`/`changeInCash`  
> /`cashflowStatements`/`changeInCash`/`raw`  
> /`cashflowStatements`/`changeInCash`/`fmt`  
> /`cashflowStatements`/`changeInCash`/`longfmt`  
> 
> **Cash Flow Statements Repurchase of Stock**  
> /`cashflowStatements`/`repurchaseOfStock`  
> /`cashflowStatements`/`repurchaseOfStock`/`raw`  
> /`cashflowStatements`/`repurchaseOfStock`/`fmt`  
> /`cashflowStatements`/`repurchaseOfStock`/`longfmt`  
> 
> **Cash Flow Statements Issuance of Stock**  
> /`cashflowStatements`/`issuanceOfStock`  
> /`cashflowStatements`/`issuanceOfStock`/`raw`  
> /`cashflowStatements`/`issuanceOfStock`/`fmt`  
> /`cashflowStatements`/`issuanceOfStock`/`longfmt`  
> 
> **Cash Flow Statements Net Borrowings**  
> /`cashflowStatements`/`netBorrowings`  
> /`cashflowStatements`/`netBorrowings`/`raw`  
> /`cashflowStatements`/`netBorrowings`/`fmt`  
> /`cashflowStatements`/`netBorrowings`/`longfmt`  
> 
> **Cash Flow Statements Other Cash Flows From Financing Activities**  
> /`cashflowStatements`/`otherCashflowsFromFinancingActivities`  
> /`cashflowStatements`/`otherCashflowsFromFinancingActivities`/`raw`  
> /`cashflowStatements`/`otherCashflowsFromFinancingActivities`/`fmt`  
> /`cashflowStatements`/`otherCashflowsFromFinancingActivities`/`longfmt`  
> 
> **Cash Flow Statements Other Cash Flows From Investing Activities**  
> /`cashflowStatements`/`otherCashflowsFromInvestingActivities`  
> /`cashflowStatements`/`otherCashflowsFromInvestingActivities`/`raw`  
> /`cashflowStatements`/`otherCashflowsFromInvestingActivities`/`fmt`  
> /`cashflowStatements`/`otherCashflowsFromInvestingActivities`/`longfmt`  
> 
> **Max Age** *Maximum number of seconds in which results from the cashflowStatementHistory query can be cached*  
> /`maxAge`  


## Key Statistics
The **defaultKeyStatistics** module displays data from the company's [Statistics](https://finance.yahoo.com/quote/AAPL/cash-flow?p=AAPL) and [Holders](https://finance.yahoo.com/quote/AAPL/holders?p=AAPL) pages.  
Learn more about performing a fundamental analysis of a company on [Investopedia](https://www.investopedia.com/terms/f/fundamentalanalysis.asp)  

**Query:**  
`/quoteSummary/result/defaultKeyStatistics` + **Nested Data** (*optional*)  

**Nested Data:**  
> **Max Age** *Maximum number of seconds in which results from the defaultKeyStatistics query can be cached*  
> /`maxAge`  
> 
> **Price Hint**  
> /`priceHint`  
> /`priceHint`/`raw`  
> /`priceHint`/`fmt`  
> /`priceHint`/`longfmt`  
> 
> **Enterprise Value** *[more](https://www.investopedia.com/terms/e/enterprisevalue.asp)*  
> /`enterpriseValue`  
> /`enterpriseValue`/`raw`  
> /`enterpriseValue`/`fmt`  
> /`enterpriseValue`/`longfmt`  
> 
> **Forward P/E** *[more](https://www.investopedia.com/terms/f/forwardpe.asp)*  
> /`forwardPE`  
> /`forwardPE`/`raw`  
> /`forwardPE`/`fmt`  
> 
> **Profit Margins** *[more](https://www.investopedia.com/terms/p/profitmargin.asp)*  
> /`profitMargins`  
> /`profitMargins`/`raw`  
> /`profitMargins`/`fmt`  
> 
> **Float Shares** *[more](https://www.investopedia.com/articles/basics/03/030703.asp)*  
> /`floatShares`  
> /`floatShares`/`raw`  
> /`floatShares`/`fmt`  
> /`floatShares`/`longFmt`  
> 
> **Shares Outstanding** *[more](https://www.investopedia.com/terms/o/outstandingshares.asp)*  
> /`sharesOutstanding`  
> /`sharesOutstanding`/`raw`  
> /`sharesOutstanding`/`fmt`  
> /`sharesOutstanding`/`longFmt`  
> 
> **Shares Short** *[more](https://www.investopedia.com/terms/s/shortinterest.asp)*  
> /`sharesShort`  
> /`sharesShort`/`raw`  
> /`sharesShort`/`fmt`  
> /`sharesShort`/`longFmt`  
> 
> **Shares Short Prior Month**  
> /`sharesShortPriorMonth`  
> /`sharesShortPriorMonth`/`raw`  
> /`sharesShortPriorMonth`/`fmt`  
> /`sharesShortPriorMonth`/`longFmt`  
> 
> **Shares Short Previous Month**  
> /`sharesShortPreviousMonthDate`  
> /`sharesShortPreviousMonthDate`/`raw`  
> /`sharesShortPreviousMonthDate`/`fmt`  
> 
> **Short Interest Date**  
> /`dateShortInterest`  
> /`dateShortInterest`/`raw`  
> /`dateShortInterest`/`fmt`  
> 
> **Percent of Shares Outstanding**  
> /`sharesPercentSharesOut`  
> /`sharesPercentSharesOut`/`raw`  
> /`sharesPercentSharesOut`/`fmt`  
> 
> **Percent of Shares Held by Insiders**  
> /`heldPercentInsiders`  
> /`heldPercentInsiders`/`raw`  
> /`heldPercentInsiders`/`fmt`  
> 
> **Percent of Shares Held by Institutions**  
> /`heldPercentInstitutions`  
> /`heldPercentInstitutions`/`raw`  
> /`heldPercentInstitutions`/`fmt`  
> 
> **Short Ratio** *[more](https://www.investopedia.com/terms/s/shortinterestratio.asp)*  
> /`shortRatio`  
> /`shortRatio`/`raw`  
> /`shortRatio`/`fmt`  
> 
> **Short Percent of Float**  
> /`shortPercentOfFloat`  
> /`shortPercentOfFloat`/`raw`  
> /`shortPercentOfFloat`/`fmt`  
> 
> **Beta** *[more](https://www.investopedia.com/terms/b/beta.asp)*  
> /`beta`  
> /`beta`/`raw`  
> /`beta`/`fmt`  
> 
> **Category**  
> /`category`  
> 
> **Book Value** *[more](https://www.investopedia.com/terms/b/bookvalue.asp)*  
> /`bookValue`  
> /`bookValue`/`raw`  
> /`bookValue`/`fmt`  
> 
> **Price to Book Ratio** *[more](https://www.investopedia.com/terms/p/price-to-bookratio.asp)*  
> /`priceToBook`  
> /`priceToBook`/`raw`  
> /`priceToBook`/`fmt`  
> 
> **Fund Family**  
> /`fundFamily`  
> 
> **Legal Type**  
> /`legalType`  
> 
> **Last Fiscal Year End Date**  
> /`lastFiscalYearEnd`  
> /`lastFiscalYearEnd`/`raw`  
> /`lastFiscalYearEnd`/`fmt`  
> 
> **Next Fiscal Year End Date**  
> /`nextFiscalYearEnd`  
> /`nextFiscalYearEnd`/`raw`  
> /`nextFiscalYearEnd`/`fmt`  
> 
> **Most Recent Quarter Date**  
> /`mostRecentQuarter`  
> /`mostRecentQuarter`/`raw`  
> /`mostRecentQuarter`/`fmt`  
> 
> **Quarterly Growth Earnings**  
> /`earningsQuarterlyGrowth`  
> /`earningsQuarterlyGrowth`/`raw`  
> /`earningsQuarterlyGrowth`/`fmt`  
> 
> **Net Income Applicable To Common Shares**  
> /`netIncomeToCommon`  
> /`netIncomeToCommon`/`raw`  
> /`netIncomeToCommon`/`fmt`  
> /`netIncomeToCommon`/`longFmt`  
> 
> **Trailing EPS** *[more](https://www.investopedia.com/terms/t/trailingeps.asp#:~:text=Trailing%20earnings%20per%20share%20(EPS)%20is%20a%20company's%20earnings%20generated,period%20or%20four%20earnings%20releases.)*  
> /`trailingEps`  
> /`trailingEps`/`raw`  
> /`trailingEps`/`fmt`  
> 
> **Forward EPS** *[more](https://www.investopedia.com/terms/f/fowardlookingearnings.asp)*  
> /`forwardEps`  
> /`forwardEps`/`raw`  
> /`forwardEps`/`fmt`  
> 
> **PEG Ratio** *[more](https://www.investopedia.com/terms/p/pegratio.asp)*  
> /`pegRatio`  
> /`pegRatio`/`raw`  
> /`pegRatio`/`fmt`  
> 
> **Stock Split Factor** *[more](https://www.investopedia.com/ask/answers/what-stock-split-why-do-stocks-split/#:~:text=All%20publicly%2Dtraded%20companies%20have,of%20shares%20that%20are%20outstanding.&text=For%20example%2C%20in%20a%202,2%2Dfor%2D1%20split.)*  
> /`lastSplitFactor`  
> 
> **Last Split Date** *[more](https://www.investopedia.com/ask/answers/what-stock-split-why-do-stocks-split/#:~:text=All%20publicly%2Dtraded%20companies%20have,of%20shares%20that%20are%20outstanding.&text=For%20example%2C%20in%20a%202,2%2Dfor%2D1%20split.)*  
> /`lastSplitDate`  
> /`lastSplitDate`/`raw`  
> /`lastSplitDate`/`fmt`  
> 
> **Enterprise to Revenue** *[more](https://www.investopedia.com/terms/e/ev-revenue-multiple.asp)*  
> /`enterpriseToRevenue`  
> /`enterpriseToRevenue`/`raw`  
> /`enterpriseToRevenue`/`fmt`  
> 
> **EBITDA/EV Multiple** *[more](https://www.investopedia.com/terms/e/ebitda-ev-multiple.asp)*  
> /`enterpriseToEbitda`  
> /`enterpriseToEbitda`/`raw`  
> /`enterpriseToEbitda`/`fmt`  
> 
> **52 Week Change in Percent** *[more](https://www.investopedia.com/terms/n/netchange.asp)*  
> /`52WeekChange`  
> /`52WeekChange`/`raw`  
> /`52WeekChange`/`fmt`  
> 
> **S&P 52 Week Change in Percent** *[more](https://www.investopedia.com/terms/n/netchange.asp)*  
> /`SandP52WeekChange`  
> /`SandP52WeekChange`/`raw`  
> /`SandP52WeekChange`/`fmt`  
> 
> **Last Dividend Value** *[more](https://www.investopedia.com/terms/d/dividend.asp)*  
> /`lastDividendValue`  
> /`lastDividendValue`/`raw`  
> /`lastDividendValue`/`fmt`  
> 
> **Last Dividend Date (Declaration Date)** *[more](https://www.investopedia.com/terms/d/declarationdate.asp)*  
> /`lastDividendDate`  
> /`lastDividendDate`/`raw`  
> /`lastDividendDate`/`fmt`  


## Earnings
The **earnings** module displays data from the company's [Analysis](https://finance.yahoo.com/quote/AAPL/analysis?p=AAPL) page.  
Learn more about company earnings on [Investopedia](https://www.investopedia.com/terms/e/earnings.asp)  

**Query:**  
`/quoteSummary/result/earnings` + **Nested Data** (*optional*)  

**Nested Data:**  
> **Max Age** *Maximum number of seconds in which results from the defaultKeyStatistics query can be cached*  
> /`maxAge`  
> 
> **Quarterly Earnings Date**  
> /`earningsChart`/`quarterly`/`date`  
> 
> **Quarterly Earnings Actual**  
> /`earningsChart`/`quarterly`/`actual`  
> /`earningsChart`/`quarterly`/`actual`/`raw`  
> /`earningsChart`/`quarterly`/`actual`/`fmt`  
> 
> **Quarterly Earnings Estimate**  
> /`earningsChart`/`quarterly`/`estimate`  
> /`earningsChart`/`quarterly`/`estimate`/`raw`  
> /`earningsChart`/`quarterly`/`estimate`/`fmt`  
> 
> **Quarter Earnings Estimate**  
> /`earningsChart`/`currentQuarterEstimate`  
> /`earningsChart`/`currentQuarterEstimate`/`raw`  
> /`earningsChart`/`currentQuarterEstimate`/`fmt`  
> 
> **Quarter Earnings Estimate Date**  
> /`earningsChart`/`currentQuarterEstimateDate`  
> 
> **Quarter Earnings Estimate Date Year**  
> /`earningsChart`/`currentQuarterEstimateYear`  
> 
> **Quarter Earnings Announcement Date**  
> /`earningsChart`/`earningsDate`  
> /`earningsChart`/`earningsDate`/`raw`  
> /`earningsChart`/`earningsDate`/`fmt`  
> 
> **Yearly Financials Date**  
> /`financialsChart`/`yearly`/`date`  
> 
> **Yearly Financials Revenue**  
> /`financialsChart`/`yearly`/`revenue`  
> /`financialsChart`/`yearly`/`revenue`/`raw`  
> /`financialsChart`/`yearly`/`revenue`/`fmt`  
> /`financialsChart`/`yearly`/`revenue`/`longFmt`  
> 
> **Yearly Financials Earnings**  
> /`financialsChart`/`yearly`/`earnings`  
> /`financialsChart`/`yearly`/`earnings`/`raw`  
> /`financialsChart`/`yearly`/`earnings`/`fmt`  
> /`financialsChart`/`yearly`/`earnings`/`longFmt`  
> 
> **Quarterly Financials Date**  
> /`financialsChart`/`quarterly`/`date`  
> 
> **Quarterly Financials Revenue**  
> /`financialsChart`/`quarterly`/`revenue`  
> /`financialsChart`/`quarterly`/`revenue`/`raw`  
> /`financialsChart`/`quarterly`/`revenue`/`fmt`  
> /`financialsChart`/`quarterly`/`revenue`/`longFmt`  
> 
> **Quarterly Financials Earnings**  
> /`financialsChart`/`quarterly`/`earnings`  
> /`financialsChart`/`quarterly`/`earnings`/`raw`  
> /`financialsChart`/`quarterly`/`earnings`/`fmt`  
> /`financialsChart`/`quarterly`/`earnings`/`longFmt`  
> 
> **Financial Currency**  
> /`financialCurrency`  


## Earnings History
The **earningsHistory** module displays data from the company's [Analysis](https://finance.yahoo.com/quote/AAPL/analysis?p=AAPL) page.  
Learn more about company earnings on [Investopedia](https://www.investopedia.com/terms/e/earnings.asp)  

**Query:**  
`/quoteSummary/result/earningsHistory` + **Nested Data** (*optional*)  

**Nested Data:**  
> **Historic Report Max Age** *Maximum number of seconds in which results from the earningsHistory/history query can be cached*  
> /`history`/`maxAge`  
> 
> **Historic EPS Actual**  
> /`history`/`epsActual`  
> /`history`/`epsActual`/`raw  
> /`history`/`epsActual`/`fmt  
> 
> **Historic EPS Estimate**  
> /`history`/`epsEstimate`  
> /`history`/`epsEstimate`/`raw  
> /`history`/`epsEstimate`/`fmt  
> 
> **Historic EPS Difference**  
> /`history`/`epsDifference`  
> /`history`/`epsDifference`/`raw  
> /`history`/`epsDifference`/`fmt  
> 
> **Historic EPS Surprise Percent**  
> /`history`/`surprisePercent`  
> /`history`/`surprisePercent`/`raw`  
> /`history`/`surprisePercent`/`fmt`  
> 
> **Historic EPS Date by Quarter**  
> /`history`/`quarter`  
> /`history`/`quarter`/`raw`  
> /`history`/`quarter`/`fmt`  
> 
> **Historic EPS Date by Period**  
> /`history`/`period`  
> 
> **Max Age** *Maximum number of seconds in which results from the earningsHistory query can be cached*  
> /`maxAge`  


## Earnings Trend
The **earningsTrend** module displays data from the company's [Analysis](https://finance.yahoo.com/quote/AAPL/analysis?p=AAPL) page.  
Learn more about company earnings on [Investopedia](https://www.investopedia.com/terms/e/earnings.asp)  

**Query:**  
`/quoteSummary/result/earningsTrend` + **Nested Data** (*optional*)  

**Nested Data:**  
> **Earnings Trend Max Age** *Maximum number of seconds in which results from the earningsTrend/trend query can be cached*  
> /`trend`/`maxAge`  
> 
> **Earnings Trend Period**  
> /`trend`/`period`  
> 
> **Earnings Trend End Date**  
> /`trend`/`endDate`  
> 
> **Earnings Trend Growth**  
> /`trend`/`growth`  
> /`trend`/`growth`/`raw`  
> /`trend`/`growth`/`fmt`  
> 
> **Earnings Estimate Average**  
> /`trend`/`earningsEstimate`/`avg`  
> /`trend`/`earningsEstimate`/`avg`/`raw`  
> /`trend`/`earningsEstimate`/`avg`/`fmt`  
> 
> **Earnings Estimate Low**  
> /`trend`/`earningsEstimate`/`low`  
> /`trend`/`earningsEstimate`/`low`/`raw`  
> /`trend`/`earningsEstimate`/`low`/`fmt`  
> 
> **Earnings Estimate High**  
> /`trend`/`earningsEstimate`/`high`  
> /`trend`/`earningsEstimate`/`high`/`raw`  
> /`trend`/`earningsEstimate`/`high`/`fmt`  
> 
> **Earnings Estimate Last Year EPS**  
> /`trend`/`earningsEstimate`/`yearAgoEps`  
> /`trend`/`earningsEstimate`/`yearAgoEps`/`raw`  
> /`trend`/`earningsEstimate`/`yearAgoEps`/`fmt`  
> 
> **Earnings Estimate Number of Analysts**  
> /`trend`/`earningsEstimate`/`numberOfAnalysts`  
> /`trend`/`earningsEstimate`/`numberOfAnalysts`/`raw`  
> /`trend`/`earningsEstimate`/`numberOfAnalysts`/`fmt`  
> /`trend`/`earningsEstimate`/`numberOfAnalysts`/`longFmt`  
> 
> **Earnings Estimate Growth**  
> /`trend`/`earningsEstimate`/`growth`  
> /`trend`/`earningsEstimate`/`growth`/`raw`  
> /`trend`/`earningsEstimate`/`growth`/`fmt`  
> 
> **Revenue Estimate Average**  
> /`trend`/`revenueEstimate`/`avg`  
> /`trend`/`revenueEstimate`/`avg`/`raw`  
> /`trend`/`revenueEstimate`/`avg`/`fmt`  
> /`trend`/`revenueEstimate`/`avg`/`longFmt`  
> 
> **Revenue Estimate Low**  
> /`trend`/`revenueEstimate`/`low`  
> /`trend`/`revenueEstimate`/`low`/`raw`  
> /`trend`/`revenueEstimate`/`low`/`fmt`  
> /`trend`/`revenueEstimate`/`low`/`longFmt`  
> 
> **Revenue Estimate High**  
> /`trend`/`revenueEstimate`/`high`  
> /`trend`/`revenueEstimate`/`high`/`raw`  
> /`trend`/`revenueEstimate`/`high`/`fmt`  
> /`trend`/`revenueEstimate`/`high`/`longFmt`  
> 
> **Revenue Estimate Number Analysts**  
> /`trend`/`revenueEstimate`/`numberOfAnalysts`  
> /`trend`/`revenueEstimate`/`numberOfAnalysts`/`raw`  
> /`trend`/`revenueEstimate`/`numberOfAnalysts`/`fmt`  
> /`trend`/`revenueEstimate`/`numberOfAnalysts`/`longFmt`  
> 
> **Revenue Estimate Last Year**  
> /`trend`/`revenueEstimate`/`yearAgoRevenue`  
> /`trend`/`revenueEstimate`/`yearAgoRevenue`/`raw`  
> /`trend`/`revenueEstimate`/`yearAgoRevenue`/`fmt`  
> /`trend`/`revenueEstimate`/`yearAgoRevenue`/`longFmt`  
> 
> **Revenue Estimate Growth**  
> /`trend`/`revenueEstimate`/`growth`  
> /`trend`/`revenueEstimate`/`growth`/`raw`  
> /`trend`/`revenueEstimate`/`growth`/`fmt`  
> 
> **EPS Trend (Current)**  
> /`trend`/`epsTrend`/`current`  
> /`trend`/`epsTrend`/`current`/`raw`  
> /`trend`/`epsTrend`/`current`/`fmt`  
> 
> **EPS Trend (7 Days Ago)**  
> /`trend`/`epsTrend`/`7daysAgo`  
> /`trend`/`epsTrend`/`7daysAgo`/`raw`  
> /`trend`/`epsTrend`/`7daysAgo`/`fmt`  
> 
> **EPS Trend (30 Days Ago)**  
> /`trend`/`epsTrend`/`30daysAgo`  
> /`trend`/`epsTrend`/`30daysAgo`/`raw`  
> /`trend`/`epsTrend`/`30daysAgo`/`fmt`  
> 
> **EPS Trend (60 Days Ago)**  
> /`trend`/`epsTrend`/`60daysAgo`  
> /`trend`/`epsTrend`/`60daysAgo`/`raw`  
> /`trend`/`epsTrend`/`60daysAgo`/`fmt`  
> 
> **EPS Trend (90 Days Ago)**  
> /`trend`/`epsTrend`/`90daysAgo`  
> /`trend`/`epsTrend`/`90daysAgo`/`raw`  
> /`trend`/`epsTrend`/`90daysAgo`/`fmt`  
> 
> **EPS Revisions (Up Last 7 Days)**  
> /`trend`/`epsRevisions`/`upLast7days`  
> /`trend`/`epsRevisions`/`upLast7days`/`raw`  
> /`trend`/`epsRevisions`/`upLast7days`/`fmt`  
> /`trend`/`epsRevisions`/`upLast7days`/`longFmt`  
> 
> **EPS Revisions (Up Last 30 Days)**  
> /`trend`/`epsRevisions`/`upLast30days`  
> /`trend`/`epsRevisions`/`upLast30days`/`raw`  
> /`trend`/`epsRevisions`/`upLast30days`/`fmt`  
> /`trend`/`epsRevisions`/`upLast30days`/`longFmt`  
> 
> **EPS Revisions (Down Last 30 Days)**  
> /`trend`/`epsRevisions`/`downLast30days`  
> /`trend`/`epsRevisions`/`downLast30days`/`raw`  
> /`trend`/`epsRevisions`/`downLast30days`/`fmt`  
> /`trend`/`epsRevisions`/`downLast30days`/`longFmt`  
> 
> **Max Age** *Maximum number of seconds in which results from the earningsTrend query can be cached*  
> /`maxAge`  


## ESG Scores
The **esgScores** module displays "Product Involvement Areas" as part of the ESG Score on the company's [Sustainability](https://finance.yahoo.com/quote/AAPL/analysis?p=AAPL) page.  
Learn more about ESG Scoring on [Investopedia](https://www.investopedia.com/insights/new-approach-esg-scoring/)  

**Query:**  
`/quoteSummary/result/esgScores` + **Nested Data** (*optional*)  

**Nested Data:**  
> **Involvement in Controversial Weapons**  
> /`controversialWeapons`  
> 
> **Involvement in Small Arms**  
> /`smallArms`  
> 
> **Involvement in Fur and Specialty Leather**  
> /`furLeather`  
> 
> **Involvement in Gambling**  
> /`gambling`  
> 
> **Involvement in Geneticall Modified Organism (GMO)**  
> /`gmo`  
> 
> **Involvement in Military Contracting**  
> /`militaryContract`  
> 
> **Involvement in Nuclear**  
> /`nuclear`  
> 
> **Involvement in Pesticides**  
> /`pesticides`  
> 
> **Involvement in Palm Oil**  
> /`palmOil`  
> 
> **Involvement in Thermal Coal**  
> /`coal`  
> 
> **Involvement in Tobacco Products**  
> /`tobacco`  


## Financial Data
The **financialData** module displays information on the company's condensed financials.  
Learn more about condensed financials on [Investopedia](https://www.investopedia.com/terms/c/condensedfinancials.asp)  

**Query:**  
`/quoteSummary/result/financialData` + **Nested Data** (*optional*)  

**Nested Data:**  
> **Max Age** *Maximum number of seconds in which results from the earningsTrend query can be cached*
> /`maxAge`  
> 
> **Current Price**  
> /`currentPrice`  
> /`currentPrice`/`raw`  
> /`currentPrice`/`fmt`  
> 
> **Target High Price**  
> /`targetHighPrice`  
> /`targetHighPrice`/`raw`  
> /`targetHighPrice`/`fmt`  
> 
> **Target Low Price**  
> /`targetLowPrice`  
> /`targetLowPrice`/`raw`  
> /`targetLowPrice`/`fmt`  
> 
> **Target Mean Price**  
> /`targetMeanPrice`  
> /`targetMeanPrice`/`raw`  
> /`targetMeanPrice`/`fmt`  
> 
> **Target Median Price**  
> /`targetMedianPrice`  
> /`targetMedianPrice`/`raw`  
> /`targetMedianPrice`/`fmt`  
> 
> **Recommendation Mean**  
> /`recommendationMean`  
> /`recommendationMean`/`raw`  
> /`recommendationMean`/`fmt`  
> 
> **Recommendation Key**  
> /`recommendationKey`  
> 
> **Number of Analyst Opinions**  
> /`numberOfAnalystOpinions`  
> /`numberOfAnalystOpinions`/`raw`  
> /`numberOfAnalystOpinions`/`fmt`  
> /`numberOfAnalystOpinions`/`longFmt`  
> 
> **Total Cash**  
> /`totalCash`  
> /`totalCash`/`raw`  
> /`totalCash`/`fmt`  
> /`totalCash`/`longFmt`  
> 
> **Total Cash Per Share**  
> /`totalCashPerShare`  
> /`totalCashPerShare`/`raw`  
> /`totalCashPerShare`/`fmt`  
> 
> **EBITDA – Earnings Before Interest, Taxes, Depreciation, and Amortization** *[more](https://www.investopedia.com/terms/e/ebitda.asp)*  
> /`ebitda`  
> /`ebitda`/`raw`  
> /`ebitda`/`fmt`  
> /`ebitda`/`longFmt`  
> 
> **Total Debt**  
> /`totalDebt`  
> /`totalDebt`/`raw`  
> /`totalDebt`/`fmt`  
> /`totalDebt`/`longFmt`  
> 
> **Quick Ratio** *[more](https://www.investopedia.com/terms/q/quickratio.asp)*  
> /`quickRatio`  
> /`quickRatio`/`raw`  
> /`quickRatio`/`fmt`  
> 
> **Current Ratio** *[more](https://www.investopedia.com/terms/c/currentratio.asp)*  
> /`currentRatio`  
> /`currentRatio`/`raw`  
> /`currentRatio`/`fmt`  
> 
> **Total Revenue** *[more](https://www.investopedia.com/terms/r/revenue.asp)*  
> /`totalRevenue`  
> /`totalRevenue`/`raw`  
> /`totalRevenue`/`fmt`  
> /`totalRevenue`/`longFmt`  
> 
> **Debt-to-Equity Ratio (D/E)** *[more](https://www.investopedia.com/terms/d/debtequityratio.asp)*  
> /`debtToEquity`  
> /`debtToEquity`/`raw`  
> /`debtToEquity`/`fmt`  
> 
> **Revenue Per Share**  
> /`revenuePerShare`  
> /`revenuePerShare`/`raw`  
> /`revenuePerShare`/`fmt`  
> 
> **Return On Assets (ROA)** *[more](https://www.investopedia.com/terms/r/returnonassets.asp)*  
> /`returnOnAssets`  
> /`returnOnAssets`/`raw`  
> /`returnOnAssets`/`fmt`  
> 
> **Return On Equity (ROE)** *[more](https://www.investopedia.com/terms/r/returnonequity.asp)*  
> /`returnOnEquity`  
> /`returnOnEquity`/`raw`  
> /`returnOnEquity`/`fmt`  
> 
> **Gross Profits** *[more](https://www.investopedia.com/terms/g/grossprofit.asp)*  
> /`grossProfits`  
> /`grossProfits`/`raw`  
> /`grossProfits`/`fmt`  
> /`grossProfits`/`longFmt`  
> 
> **Free Cash Flow (FCF)** *[more](https://www.investopedia.com/terms/f/freecashflow.asp)*  
> /`freeCashflow`  
> /`freeCashflow`/`raw`  
> /`freeCashflow`/`fmt`  
> /`freeCashflow`/`longFmt`  
> 
> **Operating Cash Flow (OCF)** *[more](https://www.investopedia.com/terms/o/operatingcashflow.asp)*  
> /`operatingCashflow`  
> /`operatingCashflow`/`raw`  
> /`operatingCashflow`/`fmt`  
> /`operatingCashflow`/`longFmt`  
> 
> **Earnings Growth Percent**  
> /`earningsGrowth`  
> /`earningsGrowth`/`raw`  
> /`earningsGrowth`/`fmt`  
> 
> **Revenue Growth Percent**  
> /`revenueGrowth`  
> /`revenueGrowth`/`raw`  
> /`revenueGrowth`/`fmt`  
> 
> **Gross Margins Percent**  
> /`grossMargins`  
> /`grossMargins`/`raw`  
> /`grossMargins`/`fmt`  
> 
> **EBITDA Margin**  
> /`ebitdaMargins`  
> /`ebitdaMargins`/`raw`  
> /`ebitdaMargins`/`fmt`  
> 
> **Operating Margin** *[more](https://www.investopedia.com/terms/o/operatingmargin.asp)*  
> /`operatingMargins`  
> /`operatingMargins`/`raw`  
> /`operatingMargins`/`fmt`  
> 
> **Profit Margin** *[more](https://www.investopedia.com/terms/p/profitmargin.asp)*  
> /`profitMargins`  
> /`profitMargins`/`raw`  
> /`profitMargins`/`fmt`  
> 
> **Financial Currency**  
> /`financialCurrency`  


## Fund Ownership
The **fundOwnership** module displays the company's Top Mutual Fund Holders on the [Holders](https://finance.yahoo.com/quote/AAPL/holders?p=AAPL) page.  
Learn more about common stock funds (Index Funds) on [Investopedia](https://www.investopedia.com/terms/c/common-stock-fund.asp)  

**Query:**  
`/quoteSummary/result/fundOwnership` + **Nested Data** (*optional*)  

**Nested Data:**  
> **Max Age** *Maximum number of seconds in which results from the fundOwnership query can be cached*  
> /`maxAge`  
> 
> **Ownership List  (All Data)**  
> /`ownershipList`  
> 
> **Ownership List Max Age** *Maximum number of seconds in which results from the ownershipList query can be cached*  
> /`ownershipList`/`maxAge`  
> 
> **Ownership List Report Date**  
> /`ownershipList`/`reportDate`  
> /`ownershipList`/`reportDate`/`raw`  
> /`ownershipList`/`reportDate`/`fmt`  
> 
> **Ownership List Organiztion**  
> /`ownershipList`/`organization`  
> 
> **Ownership List Percent Held**  
> /`ownershipList`/`pctHeld`  
> /`ownershipList`/`pctHeld`/`raw`  
> /`ownershipList`/`pctHeld`/`fmt`  
> 
> **Ownership List Position**  
> /`ownershipList`/`position`  
> /`ownershipList`/`position`/`raw`  
> /`ownershipList`/`position`/`fmt`  
> /`ownershipList`/`position`/`longFmt`  
> 
> **Ownership List Value**  
> /`ownershipList`/`value`  
> /`ownershipList`/`value`/`raw`  
> /`ownershipList`/`value`/`fmt`  
> /`ownershipList`/`value`/`longFmt`  


## Income Statement History (Annual)
The **incomeStatementHistory** module displays data from the company's [Income Statement](https://finance.yahoo.com/quote/NVDA/financials?p=NVDA) page. (*Navigate to Annual tab*)  
Learn more about financial statements on [Investopedia](https://www.investopedia.com/terms/f/financial-statements.asp)  
Learn more about corporate income sheets on [Investopedia](https://www.investopedia.com/terms/i/incomestatement.asp)  
Learn how to analyze an income sheet on [Investopedia](https://www.investopedia.com/articles/04/022504.asp)  

**Query:**  
`/quoteSummary/result/incomeStatementHistory` + **Nested Data** (*optional*)  

**Nested Data:**  
> **Income Statements (All Data)**  
> /`incomeStatementHistory`  
> 
> **Income Statements Max Age** *Maximum number of seconds in which results from the incomeStatementHistory query can be cached*  
> /`incomeStatementHistory`/`maxAge` 
> 
> **Income Statements End Date**  
> /`incomeStatementHistory`/`endDate`  
> /`incomeStatementHistory`/`endDate`/`raw`  
> /`incomeStatementHistory`/`endDate`/`fmt`  
> 
> **Income Statements Total Revenue**  
> /`incomeStatementHistory`/`totalRevenue`  
> /`incomeStatementHistory`/`totalRevenue`/`raw`  
> /`incomeStatementHistory`/`totalRevenue`/`fmt`  
> /`incomeStatementHistory`/`totalRevenue`/`longFmt`  
> 
> **Income Statements Cost of Revenue**  
> /`incomeStatementHistory`/`costOfRevenue`  
> /`incomeStatementHistory`/`costOfRevenue`/`raw`  
> /`incomeStatementHistory`/`costOfRevenue`/`fmt`  
> /`incomeStatementHistory`/`costOfRevenue`/`longFmt`  
> 
> **Income Statements Gross Profit**  
> /`incomeStatementHistory`/`grossProfit`  
> /`incomeStatementHistory`/`grossProfit`/`raw`  
> /`incomeStatementHistory`/`grossProfit`/`fmt`  
> /`incomeStatementHistory`/`grossProfit`/`longFmt`  
> 
> **Income Statements Research Development**  
> /`incomeStatementHistory`/`researchDevelopment`  
> /`incomeStatementHistory`/`researchDevelopment`/`raw`  
> /`incomeStatementHistory`/`researchDevelopment`/`fmt`  
> /`incomeStatementHistory`/`researchDevelopment`/`longFmt`  
> 
> **Income Statements Selling General Administrative**  
> /`incomeStatementHistory`/`sellingGeneralAdministrative`  
> /`incomeStatementHistory`/`sellingGeneralAdministrative`/`raw`  
> /`incomeStatementHistory`/`sellingGeneralAdministrative`/`fmt`  
> /`incomeStatementHistory`/`sellingGeneralAdministrative`/`longFmt`  
> 
> **Income Statements Total Operating Expenses**  
> /`incomeStatementHistory`/`totalOperatingExpenses`  
> /`incomeStatementHistory`/`totalOperatingExpenses`/`raw`  
> /`incomeStatementHistory`/`totalOperatingExpenses`/`fmt`  
> /`incomeStatementHistory`/`totalOperatingExpenses`/`longFmt`  
> 
> **Income Statements Operating Income**  
> /`incomeStatementHistory`/`operatingIncome`  
> /`incomeStatementHistory`/`operatingIncome`/`raw`  
> /`incomeStatementHistory`/`operatingIncome`/`fmt`  
> /`incomeStatementHistory`/`operatingIncome`/`longFmt`  
> 
> **Income Statements Total Net Income Expenses (Other)**  
> /`incomeStatementHistory`/`totalOtherIncomeExpenseNet`  
> /`incomeStatementHistory`/`totalOtherIncomeExpenseNet`/`raw`  
> /`incomeStatementHistory`/`totalOtherIncomeExpenseNet`/`fmt`  
> /`incomeStatementHistory`/`totalOtherIncomeExpenseNet`/`longFmt`  
> 
> **Income Statements EBIT**  
> /`incomeStatementHistory`/`ebit`  
> /`incomeStatementHistory`/`ebit`/`raw`  
> /`incomeStatementHistory`/`ebit`/`fmt`  
> /`incomeStatementHistory`/`ebit`/`longFmt`  
> 
> **Income Statements Interest Expense**  
> /`incomeStatementHistory`/`interestExpense`  
> /`incomeStatementHistory`/`interestExpense`/`raw`  
> /`incomeStatementHistory`/`interestExpense`/`fmt`  
> /`incomeStatementHistory`/`interestExpense`/`longFmt`  
> 
> **Income Statements Income Before Tax**  
> /`incomeStatementHistory`/`incomeBeforeTax`  
> /`incomeStatementHistory`/`incomeBeforeTax`/`raw`  
> /`incomeStatementHistory`/`incomeBeforeTax`/`fmt`  
> /`incomeStatementHistory`/`incomeBeforeTax`/`longFmt`  
> 
> **Income Statements Income Tax Expense**  
> /`incomeStatementHistory`/`incomeTaxExpense`  
> /`incomeStatementHistory`/`incomeTaxExpense`/`raw`  
> /`incomeStatementHistory`/`incomeTaxExpense`/`fmt`  
> /`incomeStatementHistory`/`incomeTaxExpense`/`longFmt`  
> 
> **Income Statements Net Income from Continuing Operations**  
> /`incomeStatementHistory`/`netIncomeFromContinuingOps`  
> /`incomeStatementHistory`/`netIncomeFromContinuingOps`/`raw`  
> /`incomeStatementHistory`/`netIncomeFromContinuingOps`/`fmt`  
> /`incomeStatementHistory`/`netIncomeFromContinuingOps`/`longFmt`  
> 
> **Income Statements Net Income**  
> /`incomeStatementHistory`/`netIncome`  
> /`incomeStatementHistory`/`netIncome`/`raw`  
> /`incomeStatementHistory`/`netIncome`/`fmt`  
> /`incomeStatementHistory`/`netIncome`/`longFmt`  
> 
> **Income Statements Net Income Applicable to Common Shares**  
> /`incomeStatementHistory`/`netIncomeApplicableToCommonShares`  
> /`incomeStatementHistory`/`netIncomeApplicableToCommonShares`/`raw`  
> /`incomeStatementHistory`/`netIncomeApplicableToCommonShares`/`fmt`  
> /`incomeStatementHistory`/`netIncomeApplicableToCommonShares`/`longFmt`  
> 
> **Max Age** *Maximum number of seconds in which results from the incomeStatementHistory query can be cached*  
> /`maxAge`  


## Income Statement History (Quarterly)
The **incomeStatementHistoryQuarterly** module displays data from the company's [Income Statement](https://finance.yahoo.com/quote/NVDA/financials?p=NVDA) page. (*Navigate to Quarterly tab*)  
Learn more about financial statements on [Investopedia](https://www.investopedia.com/terms/f/financial-statements.asp)  
Learn more about corporate income sheets on [Investopedia](https://www.investopedia.com/terms/i/incomestatement.asp)  
Learn how to analyze an income sheet on [Investopedia](https://www.investopedia.com/articles/04/022504.asp)  

**Query:**  
`/quoteSummary/result/incomeStatementHistoryQuarterly` + **Nested Data** (*optional*)  

**Nested Data:**  
> **Income Statements (All Data)**  
> /`incomeStatementHistory`  
> 
> **Income Statements Max Age** *Maximum number of seconds in which results from the incomeStatementHistory query can be cached*  
> /`incomeStatementHistory`/`maxAge` 
> 
> **Income Statements End Date**  
> /`incomeStatementHistory`/`endDate`  
> /`incomeStatementHistory`/`endDate`/`raw`  
> /`incomeStatementHistory`/`endDate`/`fmt`  
> 
> **Income Statements Total Revenue**  
> /`incomeStatementHistory`/`totalRevenue`  
> /`incomeStatementHistory`/`totalRevenue`/`raw`  
> /`incomeStatementHistory`/`totalRevenue`/`fmt`  
> /`incomeStatementHistory`/`totalRevenue`/`longFmt`  
> 
> **Income Statements Cost of Revenue**  
> /`incomeStatementHistory`/`costOfRevenue`  
> /`incomeStatementHistory`/`costOfRevenue`/`raw`  
> /`incomeStatementHistory`/`costOfRevenue`/`fmt`  
> /`incomeStatementHistory`/`costOfRevenue`/`longFmt`  
> 
> **Income Statements Gross Profit**  
> /`incomeStatementHistory`/`grossProfit`  
> /`incomeStatementHistory`/`grossProfit`/`raw`  
> /`incomeStatementHistory`/`grossProfit`/`fmt`  
> /`incomeStatementHistory`/`grossProfit`/`longFmt`  
> 
> **Income Statements Research Development**  
> /`incomeStatementHistory`/`researchDevelopment`  
> /`incomeStatementHistory`/`researchDevelopment`/`raw`  
> /`incomeStatementHistory`/`researchDevelopment`/`fmt`  
> /`incomeStatementHistory`/`researchDevelopment`/`longFmt`  
> 
> **Income Statements Selling General Administrative**  
> /`incomeStatementHistory`/`sellingGeneralAdministrative`  
> /`incomeStatementHistory`/`sellingGeneralAdministrative`/`raw`  
> /`incomeStatementHistory`/`sellingGeneralAdministrative`/`fmt`  
> /`incomeStatementHistory`/`sellingGeneralAdministrative`/`longFmt`  
> 
> **Income Statements Total Operating Expenses**  
> /`incomeStatementHistory`/`totalOperatingExpenses`  
> /`incomeStatementHistory`/`totalOperatingExpenses`/`raw`  
> /`incomeStatementHistory`/`totalOperatingExpenses`/`fmt`  
> /`incomeStatementHistory`/`totalOperatingExpenses`/`longFmt`  
> 
> **Income Statements Operating Income**  
> /`incomeStatementHistory`/`operatingIncome`  
> /`incomeStatementHistory`/`operatingIncome`/`raw`  
> /`incomeStatementHistory`/`operatingIncome`/`fmt`  
> /`incomeStatementHistory`/`operatingIncome`/`longFmt`  
> 
> **Income Statements Total Net Income Expenses (Other)**  
> /`incomeStatementHistory`/`totalOtherIncomeExpenseNet`  
> /`incomeStatementHistory`/`totalOtherIncomeExpenseNet`/`raw`  
> /`incomeStatementHistory`/`totalOtherIncomeExpenseNet`/`fmt`  
> /`incomeStatementHistory`/`totalOtherIncomeExpenseNet`/`longFmt`  
> 
> **Income Statements EBIT**  
> /`incomeStatementHistory`/`ebit`  
> /`incomeStatementHistory`/`ebit`/`raw`  
> /`incomeStatementHistory`/`ebit`/`fmt`  
> /`incomeStatementHistory`/`ebit`/`longFmt`  
> 
> **Income Statements Interest Expense**  
> /`incomeStatementHistory`/`interestExpense`  
> /`incomeStatementHistory`/`interestExpense`/`raw`  
> /`incomeStatementHistory`/`interestExpense`/`fmt`  
> /`incomeStatementHistory`/`interestExpense`/`longFmt`  
> 
> **Income Statements Income Before Tax**  
> /`incomeStatementHistory`/`incomeBeforeTax`  
> /`incomeStatementHistory`/`incomeBeforeTax`/`raw`  
> /`incomeStatementHistory`/`incomeBeforeTax`/`fmt`  
> /`incomeStatementHistory`/`incomeBeforeTax`/`longFmt`  
> 
> **Income Statements Income Tax Expense**  
> /`incomeStatementHistory`/`incomeTaxExpense`  
> /`incomeStatementHistory`/`incomeTaxExpense`/`raw`  
> /`incomeStatementHistory`/`incomeTaxExpense`/`fmt`  
> /`incomeStatementHistory`/`incomeTaxExpense`/`longFmt`  
> 
> **Income Statements Net Income from Continuing Operations**  
> /`incomeStatementHistory`/`netIncomeFromContinuingOps`  
> /`incomeStatementHistory`/`netIncomeFromContinuingOps`/`raw`  
> /`incomeStatementHistory`/`netIncomeFromContinuingOps`/`fmt`  
> /`incomeStatementHistory`/`netIncomeFromContinuingOps`/`longFmt`  
> 
> **Income Statements Net Income**  
> /`incomeStatementHistory`/`netIncome`  
> /`incomeStatementHistory`/`netIncome`/`raw`  
> /`incomeStatementHistory`/`netIncome`/`fmt`  
> /`incomeStatementHistory`/`netIncome`/`longFmt`  
> 
> **Income Statements Net Income Applicable to Common Shares**  
> /`incomeStatementHistory`/`netIncomeApplicableToCommonShares`  
> /`incomeStatementHistory`/`netIncomeApplicableToCommonShares`/`raw`  
> /`incomeStatementHistory`/`netIncomeApplicableToCommonShares`/`fmt`  
> /`incomeStatementHistory`/`netIncomeApplicableToCommonShares`/`longFmt`  
> 
> **Max Age** *Maximum number of seconds in which results from the incomeStatementHistory query can be cached*  
> /`maxAge`  


## Index Trend
The **indexTrend** module displays information of how the company's performance (growth) compares to a leading market index, this data can typically be found on the [Analysis](https://finance.yahoo.com/quote/AAPL/analysis?p=AAPL) page.  

**Query:**  
`/quoteSummary/result/indexTrend` + **Nested Data** (*optional*)  

**Nested Data:**  
> **Max Age** *Maximum number of seconds in which results from the indexTrend query can be cached*  
> /`maxAge`  
> 
> **Index Symbol**  
> /`symbol`  
> 
> **Index PE Ratio**  
> /`peRatio`  
> /`peRatio/raw`  
> /`peRatio/fmt`  
> 
> **Index PEG Ratio**  
> /`pegRatio`  
> /`pegRatio/raw`  
> /`pegRatio/fmt`  
> 
> **Estimate Periods**  
> /`estimates/period`  
> 
> **Estimate Growth**  
> /`estimates/growth`  
> /`estimates/growth/raw`  
> /`estimates/growth/fmt`  


## Industry Trend
The **industryTrend** module displays information of how the company's performance (growth) compares to the industry, this data can typically be found on the [Analysis](https://finance.yahoo.com/quote/AAPL/analysis?p=AAPL) page.  

**Query:**  
`/quoteSummary/result/industryTrend` + **Nested Data** (*optional*)  

**Nested Data:**  
> **Max Age** *Maximum number of seconds in which results from the industryTrend query can be cached*  
> /`maxAge`  
> 
> **Symbol**  
> /`symbol`  
> 
> **Estimates**  
> /`estimates`  


## Insider Holders
The **insiderHolders** module displays data from the company's [Insider Roster](https://finance.yahoo.com/quote/AAPL/insider-roster?p=AAPL) page.  
Learn more about insider holders and their transactions on [Investopedia](https://www.investopedia.com/articles/stocks/05/042605.asp)  

**Query:**  
`/quoteSummary/result/insiderHolders` + **Nested Data** (*optional*)  

**Nested Data:**  
> **Insider Holders (All Data)**  
> /`holders`  
> 
> **Insider Holders Max Age** *Maximum number of seconds in which results from the holders query can be cached*  
> /`holders`/`maxAge`  
> 
> **Insider Holders Name**  
> /`holders`/`name`  
> 
> **Insider Holders Relation**  
> /`holders`/`relation`  
> 
> **Insider Holders URL**  
> /`holders`/`url`  
> 
> **Insider Holders Transaction Description**  
> /`holders`/`transactionDescription`  
> 
> **Insider Holders Latest Transaction Date**  
> /`holders`/`latestTransDate`  
> /`holders`/`latestTransDate`/`raw`  
> /`holders`/`latestTransDate`/`fmt`  
> 
> **Insider Holders Position (Direct)**  
> /`holders`/`positionDirect`  
> /`holders`/`positionDirect`/`raw`  
> /`holders`/`positionDirect`/`fmt`  
> /`holders`/`positionDirect`/`longFmt`  
> 
> **Insider Holders Position (Direct) Date**  
> /`holders`/`positionDirectDate`  
> /`holders`/`positionDirectDate`/`raw`  
> /`holders`/`positionDirectDate`/`fmt`  
> 
> **Insider Holders Position (Indirect)**  
> /`holders`/`positionIndirect`  
> /`holders`/`positionIndirect`/`raw`  
> /`holders`/`positionIndirect`/`fmt`  
> /`holders`/`positionIndirect`/`longFmt`  
> **Insider Holders Position (Indirect) Date**  
> /`holders`/`positionIndirectDate`  
> /`holders`/`positionIndirectDate`/`raw`  
> /`holders`/`positionIndirectDate`/`fmt`  
> 
> **Max Age** *Maximum number of seconds in which results from the insiderHolders query can be cached*  
> /`maxAge`  


## Insider Transactions
The **insiderHolders** module displays data from the company's [Insider Transactions](https://finance.yahoo.com/quote/AAPL/insider-transactions?p=AAPL) page. ("Insider Transactions Reported - Last Two Years" Section)  
Learn more about insider and institutional stock ownership on [Investopedia](https://www.investopedia.com/articles/stocks/05/042605.asp)  

**Query:**  
`/quoteSummary/result/insiderTransactions` + **Nested Data** (*optional*)  

**Nested Data:**  
> **Insider Transactions (All Data)**  
> /`transactions`  
> 
> **Insider Transactions Max Age** *Maximum number of seconds in which results from the transactions query can be cached*  
> /`transactions`/`maxAge`  
> 
> **Insider Transactions Shares**  
> /`transactions`/`shares`  
> /`transactions`/`shares`/`raw`  
> /`transactions`/`shares`/`fmt`  
> /`transactions`/`shares`/`longFmt`  
> 
> **Insider Transactions Value**  
> /`transactions`/`value`  
> /`transactions`/`value`/`raw`  
> /`transactions`/`value`/`fmt`  
> /`transactions`/`value`/`longFmt`  
> 
> **Insider Transactions Filer URL**  
> /`transactions`/`filerUrl`  
> 
> **Insider Transactions Transaction Text**  
> /`transactions`/`transactionText`  
> 
> **Insider Transactions Filer Name**  
> /`transactions`/`filerName`  
> 
> **Insider Transactions Filer Relation**  
> /`transactions`/`filerRelation`  
> 
> **Insider Transactions Money Text**  
> /`transactions`/`moneyText`  
> 
> **Insider Transactions Start Date**  
> /`transactions`/`startDate`  
> /`transactions`/`startDate`/`raw`  
> /`transactions`/`startDate`/`fmt`  
> 
> **Insider Transactions Ownership**  
> /`transactions`/`ownership`  
> 
> **Max Age** *Maximum number of seconds in which results from the insiderTransactions query can be cached*  
> /`maxAge`  


## Institution Ownership
The **institutionOwnership** module displays the company's Top Institution Holders on the [Holders](https://finance.yahoo.com/quote/AAPL/holders?p=AAPL) page.  
Learn more about insider and institutional stock ownership on [Investopedia](https://www.investopedia.com/articles/stocks/05/042605.asp)  

**Query:**  
`/quoteSummary/result/institutionOwnership` + **Nested Data** (*optional*)  

**Nested Data:**  
> **Max Age** *Maximum number of seconds in which results from the institutionOwnership query can be cached*  
> /`maxAge`  
> 
> **Ownership List  (All Data)**  
> /`ownershipList`  
> 
> **Ownership List Max Age** *Maximum number of seconds in which results from the ownershipList query can be cached*  
> /`ownershipList`/`maxAge`  
> 
> **Ownership List Report Date**  
> /`ownershipList`/`reportDate`  
> /`ownershipList`/`reportDate`/`raw`  
> /`ownershipList`/`reportDate`/`fmt`  
> 
> **Ownership List Organiztion**  
> /`ownershipList`/`organization`  
> 
> **Ownership List Percent Held**  
> /`ownershipList`/`pctHeld`  
> /`ownershipList`/`pctHeld`/`raw`  
> /`ownershipList`/`pctHeld`/`fmt`  
> 
> **Ownership List Position**  
> /`ownershipList`/`position`  
> /`ownershipList`/`position`/`raw`  
> /`ownershipList`/`position`/`fmt`  
> /`ownershipList`/`position`/`longFmt`  
> 
> **Ownership List Value**  
> /`ownershipList`/`value`  
> /`ownershipList`/`value`/`raw`  
> /`ownershipList`/`value`/`fmt`  
> /`ownershipList`/`value`/`longFmt`  


## Major Direct Holders
The **majorDirectHolders** module does not display any pertinent information at this time.  

**Query:**  
`/quoteSummary/result/majorDirectHolders` + **Nested Data** (*optional*)  

**Nested Data:**  
> **Holders List  (All Data)**  
> /`holders`  
> 
> **Holders List Max Age** *Maximum number of seconds in which results from the holders query can be cached*  
> /`holders`/`maxAge`  


## Major Holders Breakdown
The **majorHoldersBreakdown** module displays the company's Major Holders Breakdown statistics on the [Holders](https://finance.yahoo.com/quote/AAPL/holders?p=AAPL) page.  
Learn more about insider and institutional stock ownership on [Investopedia](https://www.investopedia.com/articles/stocks/05/042605.asp)  

**Query:**  
`/quoteSummary/result/majorHoldersBreakdown` + **Nested Data** (*optional*)  

**Nested Data:**  
> **Max Age** *Maximum number of seconds in which results from the majorHoldersBreakdown query can be cached*  
> /`maxAge`  
> 
> **Insiders Percent Held**  
> /`insidersPercentHeld`  
> /`insidersPercentHeld`/`raw`  
> /`insidersPercentHeld`/`fmt`  
> 
> **Institutions Percent Held**  
> /`institutionsPercentHeld`  
> /`institutionsPercentHeld`/`raw`  
> /`institutionsPercentHeld`/`fmt`  
> 
> **Institutions Float Percent Held**  
> /`institutionsFloatPercentHeld`  
> /`institutionsFloatPercentHeld`/`raw`  
> /`institutionsFloatPercentHeld`/`fmt`  
> 
> **Institutions Count**  
> /`institutionsCount`  
> /`institutionsCount`/`raw`  
> /`institutionsCount`/`fmt`  
> /`institutionsCount`/`longFmt`  


## Net Share Purchase Activity
The **netSharePurchaseActivity** module displays insider data from the company's [Insider Transactions](https://finance.yahoo.com/quote/AAPL/insider-transactions?p=AAPL) page. ("Insider Purchases Last 6 Months" Section)  
Learn more about insider and institutional stock ownership on [Investopedia](https://www.investopedia.com/articles/stocks/05/042605.asp)  

**Query:**  
`/quoteSummary/result/netSharePurchaseActivity` + **Nested Data** (*optional*)  

**Nested Data:**  
> **Max Age** *Maximum number of seconds in which results from the netSharePurchaseActivity query can be cached*  
> /`maxAge`  
> 
> **Net Share Purchase Period (6 months)**  
> /`period`  
> 
> **Insider Purchases Transaction Count**  
> /`buyInfoCount`  
> /`buyInfoCount`/`raw`  
> /`buyInfoCount`/`fmt`  
> /`buyInfoCount`/`longFmt`  
> 
> **Insider Purchases Total Shares**  
> /`buyInfoShares`  
> /`buyInfoShares`/`raw`  
> /`buyInfoShares`/`fmt`  
> /`buyInfoShares`/`longFmt`  
> 
> **Insider Purchase as a Percent of Total Insider Shares Held**  
> /`buyPercentInsiderShares`  
> /`buyPercentInsiderShares`/`raw`  
> /`buyPercentInsiderShares`/`fmt`  
> 
> **Insider Sales Transaction Count**  
> /`sellInfoCount`  
> /`sellInfoCount`/`raw`  
> /`sellInfoCount`/`fmt`  
> /`sellInfoCount`/`longFmt`  
> 
> **Insider Total Shares Sold**  
> /`sellInfoShares`  
> /`sellInfoShares`/`raw`  
> /`sellInfoShares`/`fmt`  
> /`sellInfoShares`/`longFmt`  
> 
> **Insider Shares Sold as a Percent of Total Insider Shares Held**  
> /`sellPercentInsiderShares`  
> /`sellPercentInsiderShares`/`raw`  
> /`sellPercentInsiderShares`/`fmt`  
> 
> **Insider Shares Total Transactions**  
> /`netInfoCount`  
> /`netInfoCount`/`raw`  
> /`netInfoCount`/`fmt`  
> /`netInfoCount`/`longFmt`  
> 
> **Insider Shares Purchased (Sold)**  
> /`netInfoShares`  
> /`netInfoShares`/`raw`  
> /`netInfoShares`/`fmt`  
> /`netInfoShares`/`longFmt`  
> 
> **Insider Shares Purchased (Sold) as a Percent of Total Insider Shares Held**  
> /`netPercentInsiderShares`  
> /`netPercentInsiderShares`/`raw`  
> /`netPercentInsiderShares`/`fmt`  
> 
> **Total Insider Shares Held**  
> /`totalInsiderShares`  
> /`totalInsiderShares`/`raw`  
> /`totalInsiderShares`/`fmt`  
> /`totalInsiderShares`/`longFmt`  


## Page Views
The **pageViews** module displays visitor trend data from all the company's quote pages. Visit the quote [Summary](https://finance.yahoo.com/quote/AAPL/insider-transactions?p=AAPL) page and look for the "Visitors trend" information.  

**Query:**  
`/quoteSummary/result/pageViews` + **Nested Data** (*optional*)  

**Nested Data:**  
>  **Short Term Trend (2 Weeks)**  
> /`shortTermTrend`  
> 
>  **Mid Term Trend (10 Weeks)**  
> /`midTermTrend`  
> 
>  **Long Term Trend (9 Months)**  
> /`longTermTrend`  
> 
> **Max Age** *Maximum number of seconds in which results from the pageViews query can be cached*  
> /`maxAge`  


## Price
The **price** module displays general stock price data.  

**Query:**  
`/quoteSummary/result/price` + **Nested Data** (*optional*)  

**Nested Data:**  
> **Max Age** *Maximum number of seconds in which results from the price query can be cached*  
> /`maxAge`  
> 
> **Pre-Market Data Source**  
> /`preMarketSource`  
> 
> **Post-Market Price Change by Percent**  
> /`postMarketChangePercent`  
> /`postMarketChangePercent`/`raw`  
> /`postMarketChangePercent`/`fmt`  
> 
> **Post-Market Price Change by Value**  
> /`postMarketChange`  
> /`postMarketChange`/`raw`  
> /`postMarketChange`/`fmt`  
> 
> **Post-Market Time**  
> /`postMarketTime`  
> 
> **Post-Market Price**  
> /`postMarketPrice`  
> /`postMarketPrice`/`raw`  
> /`postMarketPrice`/`fmt`  
> 
> **Post-Market Data Source**  
> /`postMarketSource`  
> 
> **Regular Market Price Change by Percent**  
> /`regularMarketChangePercent`  
> /`regularMarketChangePercent`/`raw`  
> /`regularMarketChangePercent`/`fmt`  
> 
> **Regular Market Change by Value**  
> /`regularMarketChange`  
> /`regularMarketChange`/`raw`  
> /`regularMarketChange`/`fmt`  
> 
> **Regular Market Time**  
> /`regularMarketTime`  
> 
> **Price Hint**  
> /`priceHint`  
> /`priceHint`/`raw`  
> /`priceHint`/`fmt`  
> /`priceHint`/`longFmt`  
> 
> **Regular Market Current Price**  
> /`regularMarketPrice`  
> /`regularMarketPrice`/`raw`  
> /`regularMarketPrice`/`fmt`  
> 
> **Regular Market Day's High Price**  
> /`regularMarketDayHigh`  
> /`regularMarketDayHigh`/`raw`  
> /`regularMarketDayHigh`/`fmt`  
> 
> **Regular Market Day's Low Price**  
> /`regularMarketDayLow`  
> /`regularMarketDayLow`/`raw`  
> /`regularMarketDayLow`/`fmt`  
> 
> **Regular Market Volume**  
> /`regularMarketVolume`  
> /`regularMarketVolume`/`raw`  
> /`regularMarketVolume`/`fmt`  
> /`regularMarketVolume`/`longFmt`  
> 
> **Regular Market Previous Close Price**  
> /`regularMarketPreviousClose`  
> /`regularMarketPreviousClose`/`raw`  
> /`regularMarketPreviousClose`/`fmt`  
> 
> **Regular Market Data Source**  
> /`regularMarketSource`  
> 
> **Regular Market Open Price**  
> /`regularMarketOpen`  
> /`regularMarketOpen`/`raw`  
> /`regularMarketOpen`/`fmt`  
> 
> **Stock Market Exchange**  
> /`exchange`  
> 
> **Stock Market Exchange Name**  
> /`exchangeName`  
> 
> **Stock Market Exchange Data Delayed By**  
> /`exchangeDataDelayedBy`  
> 
> **Stock Market**  
> /`marketState`  
> 
> **Stock Quote Type**  
> /`quoteType`  
> 
> **Stock Symbol**  
> /`symbol`  
> 
> **Stock Underlying Symbol**  
> /`underlyingSymbol`  
> 
> **Stock Name**  
> /`shortName`  
> 
> **Stock Long Name**  
> /`longName`  
> 
> **Stock Exchange Currency**  
> /`currency`  
> 
> **Stock Quote Source Name**  
> /`quoteSourceName`  
> 
> **Stock Exchange Currency Symbol**  
> /`currencySymbol`  
> 
> **Stock Exchange Currency (From)**  
> /`fromCurrency`  
> 
> **Stock Exchange Currency (To)**  
> /`toCurrency`  
> 
> **Last Market**  
> /`lastMarket`  
> 
> **Stock Market Cap**  
> /`marketCap`  
> /`marketCap`/`raw`  
> /`marketCap`/`fmt`  
> /`marketCap`/`longFmt`  


## Quote Type
The **quoteType** module displays general company data as it relates to the market.  

**Query:**  
`/quoteSummary/result/quoteType` + **Nested Data** (*optional*)  

**Nested Data:**  
> **Stock Market Exchange**  
> /`exchange`  
> 
> **Stock Quote Type**  
> /`quoteType`  
> 
> **Stock Symbol**  
> /`symbol`  
> 
> **Stock Underlying Symbol**  
> /`underlyingSymbol`  
> 
> **Stock Short Name**  
> /`shortName`  
> 
> **Stock Long Name**  
> /`longName`  
> 
> **Stock First Trade Date**  
> /`firstTradeDateEpochUtc`  
> 
> **Stock Time Zone (Full Name)**  
> /`timeZoneFullName`  
> 
> **Stock Time Zone (Short Name)**  
> /`timeZoneShortName`  
> 
> **Stock UUID**  
> /`uuid`  
> 
> **Stock MessageboardID**  
> /`messageBoardId`  
> 
> **Stock GMT Offset in Milliseconds**  
> /`gmtOffSetMilliseconds`  
> 
> **Max Age** *Maximum number of seconds in which results from the quoteType query can be cached*  
> /`maxAge`  


## Recommendation Trend
The **recommendationTrend** module displays recommendation trends data from the company's [Summary](https://finance.yahoo.com/quote/AAPL?p=AAPL) page. ("Recommendation Trends" Section)  

**Query:**  
`/quoteSummary/result/recommendationTrend` + **Nested Data** (*optional*)  

**Nested Data:**  
> **Recommendation Trend (All Data)**  
> /`trend`  
> 
> **Recommendation Trend Period (Current Month + 3 Months Prior)**  
> /`trend/period`  
> 
> **Recommendation Count contributing towards a "Strong Buy"**  
> /`trend/strongBuy`  
> 
> **Recommendation Count contributing towards a "Buy"**  
> /`trend/buy`  
> 
> **Recommendation Count contributing towards a "Hold"**  
> /`trend/hold`  
> 
> **Recommendation Count contributing towards a "Sell"**  
> /`trend/sell`  
> 
> **Recommendation Count contributing towards a "Strong Sell"**  
> /`trend/strongSell`  
> 
> **Max Age** *Maximum number of seconds in which results from the recommendationTrend query can be cached*  
> /`maxAge`  


## SEC Filings
The **secFilings** module displays SEC Filing data of the company.  

**Query:**  
`/quoteSummary/result/secFilings` + **Nested Data** (*optional*)  

**Nested Data:**  
> **SEC Filings (All Data)**  
> /`filings`  
> 
> **SEC Filings Date**  
> /`filings`/`date`  
> 
> **SEC Filings Epoch Date**  
> /`filings`/`epochDate`  
> 
> **SEC Filings Type**  
> /`filings`/`type`  
> 
> **SEC Filings Title**  
> /`filings`/`title`  
> 
> **SEC Filings Page URL**  
> /`filings`/`edgarUrl`  
> 
> **SEC Filings Max Age** *Maximum number of seconds in which results from the filings query can be cached*  
> /`filings`/`maxAge`  
> 
> **Max Age** *Maximum number of seconds in which results from the secFilings query can be cached*
> /`maxAge`  


## Sector Trend
The **sectorTrend** module does not display any pertinent information at this time.  

**Query:**  
`/quoteSummary/result/sectorTrend` + **Nested Data** (*optional*)  

**Nested Data:**  
> **Max Age** *Maximum number of seconds in which results from the sectorTrend query can be cached*
> /`maxAge`  
> 
> **Sector Trend Symbol**  
> /`symbol`  
> 
> **Sector Trend Estimates**  
> /`estimates`  


## Summary Detail
The **summaryDetail** module displays a detailed summary of stock data, mostly found on the company's [Summary](https://finance.yahoo.com/quote/AAPL?p=AAPL) page.  

**Query:**  
`/quoteSummary/result/summaryDetail` + **Nested Data** (*optional*)  

**Nested Data:**  
> **Max Age** *Maximum number of seconds in which results from the summaryDetail query can be cached*  
> /`maxAge`  
> 
> **Stock Price Hint**  
> /`priceHint`  
> /`priceHint`/`raw`  
> /`priceHint`/`fmt`  
> /`priceHint`/`longFmt`  
> 
> **Stock Previous Close Price**  
> /`previousClose`  
> /`previousClose`/`raw`  
> /`previousClose`/`fmt`  
> 
> **Stock Open Price**  
> /`open`  
> /`open`/`raw`  
> /`open`/`fmt`  
> 
> **Stock Day's Low Price**  
> /`dayLow`  
> /`dayLow`/`raw`  
> /`dayLow`/`fmt`  
> 
> **Stock Day's High Price**  
> /`dayHigh`  
> /`dayHigh`/`raw`  
> /`dayHigh`/`fmt`  
> 
> **Stock Regular Market Previous Close Price**  
> /`regularMarketPreviousClose`  
> /`regularMarketPreviousClose`/`raw`  
> /`regularMarketPreviousClose`/`fmt`  
> 
> **Stock Regular Market Open Price**  
> /`regularMarketOpen`  
> /`regularMarketOpen`/`raw`  
> /`regularMarketOpen`/`fmt`  
> 
> **Stock Regular Market Day's Low**  
> /`regularMarketDayLow`  
> /`regularMarketDayLow`/`raw`  
> /`regularMarketDayLow`/`fmt`  
> 
> **Stock Regular Market Day's High**  
> /`regularMarketDayHigh`  
> /`regularMarketDayHigh`/`raw`  
> /`regularMarketDayHigh`/`fmt`  
> 
> **Stock Dividend Rate**  
> /`dividendRate`  
> /`dividendRate`/`raw`  
> /`dividendRate`/`fmt`  
> 
> **Stock Dividend Yield**  
> /`dividendYield`  
> /`dividendYield`/`raw`  
> /`dividendYield`/`fmt`  
> 
> **Stock Ex-Dividend Date**  
> /`exDividendDate`  
> /`exDividendDate`/`raw`  
> /`exDividendDate`/`fmt`  
> 
> **Stock Payout Ratio**  
> /`payoutRatio`  
> /`payoutRatio`/`raw`  
> /`payoutRatio`/`fmt`  
> 
> **Stock 5 Year Average Dividend Yield**  
> /`fiveYearAvgDividendYield`  
> /`fiveYearAvgDividendYield`/`raw`  
> /`fiveYearAvgDividendYield`/`fmt`  
> 
> **Stock Beta**  
> /`beta`  
> /`beta`/`raw`  
> /`beta`/`fmt`  
> 
> **Stock Trailing PE**  
> /`trailingPE`  
> /`trailingPE`/`raw`  
> /`trailingPE`/`fmt`  
> 
> **Stock Forward PE**  
> /`forwardPE`  
> /`forwardPE`/`raw`  
> /`forwardPE`/`fmt`  
> 
> **Stock Volume**  
> /`volume`  
> /`volume`/`raw`  
> /`volume`/`fmt`  
> /`volume`/`longFmt`  
> 
> **Stock Regular Market Volume**  
> /`regularMarketVolume`  
> /`regularMarketVolume`/`raw`  
> /`regularMarketVolume`/`fmt`  
> /`regularMarketVolume`/`longFmt`  
> 
> **Stock Average Volume**  
> /`averageVolume`  
> /`averageVolume`/`raw`  
> /`averageVolume`/`fmt`  
> /`averageVolume`/`longFmt`  
> 
> **Stock Average Volume 10 Days**  
> /`averageVolume10days`  
> /`averageVolume10days`/`raw`  
> /`averageVolume10days`/`fmt`  
> /`averageVolume10days`/`longFmt`  
> 
> **Stock Average Daily Volume 10 Day**  
> /`averageDailyVolume10Day`  
> /`averageDailyVolume10Day`/`raw`  
> /`averageDailyVolume10Day`/`fmt`  
> /`averageDailyVolume10Day`/`longFmt`  
> 
> **Stock Bid Price**  
> /`bid`  
> /`bid`/`raw`  
> /`bid`/`fmt`  
> 
> **Stock Ask Price**  
> /`ask`  
> /`ask`/`raw`  
> /`ask`/`fmt`  
> 
> **Stock Bid Size**  
> /`bidSize`  
> /`bidSize`/`raw`  
> /`bidSize`/`fmt`  
> /`bidSize`/`longFmt`  
> 
> **Stock Ask Size**  
> /`askSize`  
> /`askSize`/`raw`  
> /`askSize`/`fmt`  
> /`askSize`/`longFmt`  
> 
> **Stock Market Cap**  
> /`marketCap`  
> /`marketCap`/`raw`  
> /`marketCap`/`fmt`  
> /`marketCap`/`longFmt`  
> 
> **Stock 52 Week Low**  
> /`fiftyTwoWeekLow`  
> /`fiftyTwoWeekLow`/`raw`  
> /`fiftyTwoWeekLow`/`fmt`  
> 
> **Stock 52 Week High**  
> /`fiftyTwoWeekHigh`  
> /`fiftyTwoWeekHigh`/`raw`  
> /`fiftyTwoWeekHigh`/`fmt`  
> 
> **Price-to-Sales Trailing 12 Months**  
> /`priceToSalesTrailing12Months`  
> /`priceToSalesTrailing12Months`/`raw`  
> /`priceToSalesTrailing12Months`/`fmt`  
> 
> **Stock 50 Day Average**  
> /`fiftyDayAverage`  
> /`fiftyDayAverage`/`raw`  
> /`fiftyDayAverage`/`fmt`  
> 
> **Stock 200 Day Average**  
> /`twoHundredDayAverage`  
> /`twoHundredDayAverage`/`raw`  
> /`twoHundredDayAverage`/`fmt`  
> 
> **Stock Trailing Annual Dividend Rate**  
> /`trailingAnnualDividendRate`  
> /`trailingAnnualDividendRate`/`raw`  
> /`trailingAnnualDividendRate`/`fmt`  
> 
> **Stock Trailing Annual Dividend Yield**  
> /`trailingAnnualDividendYield`  
> /`trailingAnnualDividendYield`/`raw`  
> /`trailingAnnualDividendYield`/`fmt`  
> 
> **Stock Exchange Currency Symbol**  
> /`currency`  
> 
> **Stock Exchange Currency (From)**  
> /`fromCurrency`  
> 
> **Stock Exchange Currency (To)**  
> /`toCurrency`  
> 
> **Last Market**  
> /`lastMarket`  
> 
> **Algorithm**  
> /`algorithm`  
> 
> **Stock Tradeable**  
> /`tradeable`  


## Summary Profile
The **summaryProfile** module displays general data from the company's [Profile](https://finance.yahoo.com/quote/AAPL/profile?p=AAPL) page.  

**Query:**  
`/quoteSummary/result/summaryProfile` + **Nested Data** (*optional*)  

**Nested Data:**  
> **Company Address: Street**  
> /`address1`  
> 
> **Company Address: City**  
> /`city`  
> 
> **Company Address: Zip Code**  
> /`zip`  
> 
> **Company Address: Country**  
> /`country`  
> 
> **Company Phone Number**  
> /`phone`  
> 
> **Company Fax**  
> /`fax`  
> 
> **Company Website**  
> /`website`  
> 
> **Company Market Industry**  
> /`industry`  
> 
> **Company Market Sector**  
> /`sector`  
> 
> **Company Business Summary**  
> /`longBusinessSummary`  
> 
> **Company Full-Time Employees**  
> /`fullTimeEmployees`  
> 
> **Company Officers**  
> /`companyOfficers`  
> 
> **Max Age** *Maximum number of seconds in which results from the summaryProfile query can be cached*  
> /`maxAge`  


## Upgrade Downgrade History
The **upgradeDowngradeHistory** module displays "Upgrade & Downgrades" data from the company's [Summary](https://finance.yahoo.com/quote/AAPL?p=AAPL) page.  

**Query:**  
`/quoteSummary/result/upgradeDowngradeHistory` + **Nested Data** (*optional*)  

**Nested Data:**  
> **Upgrade Downgrade History (All Data)**  
> /`history`  
> 
> **Upgrade Downgrade Epoch Date**  
> /`history`/`epochGradeDate`  
> 
> **Upgrade Downgrade Firm Name**  
> /`history`/`firm`  
> 
> **Upgrade Downgrade Value (To Grade)**  
> /`history`/`toGrade`  
> 
> **Upgrade Downgrade Value (From Grade)**  
> /`history`/`fromGrade`  
> 
> **Upgrade Downgrade Action**  
> /`history`/`action`  
> 
> **Max Age** *Maximum number of seconds in which results from the summaryProfile query can be cached*  
> /`maxAge`  
