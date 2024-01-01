# Online Sales Analysis with Power BI

## Objective
This project is to analyze sales data of an online store. The source data is from [Link to data](https://cdn.theforage.com/vinternships/companyassets/ifobHAoMjQs9s6bKS/5XsFFJu2oCLdmYJW2/1654128941410/Online%20Retail.xlsx)

Some of the key insights about the data include:
* Which region is generating the highest revenue and which region is generating the lowest?

	On the first page of the report, I used a clustered bar chart to identify top 5 countries in revenue and bottom 5 countries in revenue.

* What is the monthly trend of revenue, which months have faced the biggest increase/decrease?

	On the second page of the report, I used the following DAX formula to calculate month over month ratio. 
```md-dax
UnitPrice MoM% = 
IF(
	ISFILTERED('Online Retail'[InvoiceDate]),
	ERROR("Time intelligence quick measures can only be grouped or filtered by the Power BI-provided date hierarchy or primary date column."),
	VAR __PREV_MONTH =
		CALCULATE(
			SUM('Online Retail'[UnitPrice]),
			DATEADD('Online Retail'[InvoiceDate].[Date], -1, MONTH)
		)
	RETURN
		DIVIDE(SUM('Online Retail'[UnitPrice]) - __PREV_MONTH, __PREV_MONTH)

```
* Which months generated the most revenue? Is there a seasonality in sales?

	On the third page of the report, I used a line chart to track seasonality in sales.

