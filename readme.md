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
				SUM('Online Retail'[TotalPrice]),
				DATEADD('Online Retail'[InvoiceDate].[Date], -1, MONTH)
			)
		RETURN
			DIVIDE(SUM('Online Retail'[TotalPrice]) - __PREV_MONTH, __PREV_MONTH)

	```
* Which months generated the most revenue? Is there a seasonality in sales?

	On the third page of the report, I used a line chart to track seasonality in sales.

* Who are the top customers and how much do they contribute to the total revenue? Is the business dependent on these customers or is the customer base diversified?

	For answering this question, I created a table and filled it with columns CustomerID, Sum of Total price and count of distinct invoice no by that customer so now by sorting the table based on sum of unit price we could track if the highest customer in revenue had ordered most frequently.

* What is the percentage of customers who are repeating their orders? Are they ordering the same products or different?

	I created a new column called timesrepeating and filtered the data on timesrepeating greater than one so that I could identify customers who purchased repeatedly more than once and view the products they bought 
```md-dax
isRepeating = CALCULATE(DISTINCTCOUNT('Online Retail'[InvoiceNo]),ALLEXCEPT('Online Retail','Online Retail'[CustomerID]))
```
