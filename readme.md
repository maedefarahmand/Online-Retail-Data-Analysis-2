# This is my personal project.

## Objective
This project is to analyze sales data of an online store. The source data is from [Link to data](https://cdn.theforage.com/vinternships/companyassets/ifobHAoMjQs9s6bKS/5XsFFJu2oCLdmYJW2/1654128941410/Online%20Retail.xlsx)

I used PowerBI to gain insight about this dataset.
Questions which were answered could be found in questions.docx file.

I used DAX formula to create some new columns.

In order to calculate month over month ratio of data I used following DAX formula:
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