# Chinook Database SQL
Chinook is a sample database available for SQL Server, Oracle, MySQL, etc. It can be created by running a single SQL script. Chinook database is an alternative to the Northwind database, being ideal for demos and testing ORM tools targeting single and multiple database servers.

Specifying SQL Queries:
-------
1. Provide a query showing Customers (just their full names, customer ID and country) who are not in the US.
```
SELECT "CustomerId", "FirstName", "LastName", "Country" FROM "Customer"
WHERE "Country" <> 'USA';
```

2. Provide a query only showing the Customers from Brazil.
```
SELECT "CustomerId", "FirstName", "LastName", "Country" FROM "Customer"
WHERE "Country" = 'Brazil';
```

3. Provide a query showing the Invoices of customers who are from Brazil. The resultant table should show the customer's full name, Invoice ID, Date of the invoice and billing country.
```
SELECT "Customer"."CustomerId", "FirstName", "LastName", "InvoiceId", "InvoiceDate", "BillingCountry"
FROM "Customer"
INNER JOIN "Invoice" ON "Customer"."CustomerId" = "Invoice"."CustomerId"
WHERE "BillingCountry" = 'USA';
```

4. Provide a query showing only the Employees who are Sales Agents.
```
SELECT * FROM "Employee";
```

5. Provide a query showing a unique list of billing countries from the Invoice table. 
```
SELECT DISTINCT "BillingCountry" FROM "Invoice";
```

6. Provide a query that shows the invoices associated with each sales agent. The resultant table should include the Sales Agent's full name.
```

```

7. Provide a query that shows the Invoice Total, Customer name, Country and Sale Agent name for all invoices and customers. 
```

```

8. How many Invoices were there in 2009 and 2011? What are the respective total sales for each of those years?
```

```

9. Looking at the InvoiceLine table, provide a query that COUNTs the number of line items for Invoice ID 37.
```

```

10. Looking at the InvoiceLine table, provide a query that COUNTs the number of line items for each Invoice. HINT: GROUP BY
```

```

11. Provide a query that includes the track name with each invoice line item. 
```

```

12. Provide a query that includes the purchased track name AND artist name with each invoice line item.
```

```

13. Provide a query that shows the # of invoices per country. HINT: GROUP BY 
```

```

14. Provide a query that shows the total number of tracks in each playlist. The Playlist name should be included on the resultant table. 
```

```

15. Provide a query that shows all the Tracks, but displays no IDs. The resultant table should include the Album name, Media type and Genre.
```

```

16. Provide a query that shows all Invoices but includes the # of invoice line items. 
```

```

17. Provide a query that shows total sales made by each sales agent.
```

```

18. Which sales agent made the most in sales in 2009?
```

```

19. Which sales agent made the most in sales in 2010?
```

```

20. Which sales agent made the most in sales over all?
```

```

21. Provide a query that shows the # of customers assigned to each sales agent. 
```

```

22. Provide a query that shows the total sales per country. Which country's customers spent the most?
```

```

23. Provide a query that shows the most purchased track of 2013.
```

```

24. Provide a query that shows the top 5 most purchased tracks over all. 
```

```

25. Provide a query that shows the top 3 best selling artists.
```

```

26. Provide a query that shows the most purchased Media Type. 
```

```

27. Provide a query that shows the number tracks purchased in all invoices that contain more than one genre. 
```

```


### EMD SCHEME:
![](https://user-images.githubusercontent.com/40778282/84611232-34ef3300-ae8b-11ea-8f43-b5a70a750e62.png)









