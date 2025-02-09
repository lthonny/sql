# Chinook Database SQL
Chinook is a sample database available for SQL Server, Oracle, MySQL, etc. It can be created by running a single SQL script. Chinook database is an alternative to the Northwind database, being ideal for demos and testing ORM tools targeting single and multiple database servers.

Specifying SQL Queries:
-------
1. Provide a query showing Customers (just their full names, customer ID and country) who are not in the US.
```sql
SELECT
  "CustomerId",
  "FirstName",
  "LastName",
  "Country"
FROM
  "Customer"
WHERE
  "Country" <> 'USA';
```

2. Provide a query only showing the Customers from Brazil.
```sql
SELECT
  "CustomerId",
  "FirstName",
  "LastName",
  "Country"
FROM
  "Customer"
WHERE
  "Country" = 'Brazil';
```

3. Provide a query showing the Invoices of customers who are from Brazil. The resultant table should show the customer's full name, Invoice ID, Date of the invoice and billing country.
```sql
SELECT
  "Customer"."CustomerId",
  "Customer"."FirstName" || ' ' || "Customer"."LastName" AS "Customer",
  "Invoice"."InvoiceId",
  "Invoice"."InvoiceDate",
  "Invoice"."BillingCountry"
FROM
  "Customer"
  JOIN "Invoice" USING("CustomerId")
WHERE
  "Invoice"."BillingCountry" = 'USA';
```

4. Provide a query showing only the Employees who are Sales Agents.
```sql
SELECT
  *
FROM
  "Employee";
```

5. Provide a query showing a unique list of billing countries from the Invoice table. 
```sql
SELECT 
	DISTINCT "Invoice"."BillingCountry"
FROM
  "Invoice";
```

6. Provide a query that shows the invoices associated with each sales agent. The resultant table should include the Sales Agent's full name.
```sql
SELECT 
	"Employee"."LastName" || ' ' || "Employee"."FirstName" AS "Employee",
	"Invoice".*
FROM 
	"Invoice"
  	JOIN "Customer" USING("CustomerId")
	JOIN "Employee" ON "Customer"."SupportRepId" = "Employee"."EmployeeId";
```

7. Provide a query that shows the Invoice Total, Customer name, Country and Sale Agent name for all invoices and customers. 
```sql
SELECT
  	"Customer"."FirstName" || ' ' || "Customer"."LastName" AS "Customer",
  	"Invoice"."BillingCountry",
  	"Invoice"."Total",
  	"Employee"."LastName"
FROM
  	"Customer"
  	JOIN "Invoice" USING("CustomerId")
 	JOIN "Employee" ON "Customer"."SupportRepId" = "Employee"."EmployeeId";
```

8. How many Invoices were there in 2009 and 2011? What are the respective total sales for each of those years?
```sql
SELECT 
	COUNT("Invoice"."InvoiceId"),
	SUM("Invoice"."Total") AS "Total"
FROM
	"Invoice"
WHERE
	"Invoice"."InvoiceDate" BETWEEN '2009-01-01' AND '2009-12-31' OR 
	"Invoice"."InvoiceDate" BETWEEN '2011-01-01' AND '2011-12-31'
```

9. Looking at the InvoiceLine table, provide a query that COUNTs the number of line items for Invoice ID 37.
```sql
SELECT 
	COUNT("InvoiceLine"."InvoiceLineId") AS "NumberOfLineItems"
FROM 
	"InvoiceLine"
WHERE 
	"InvoiceLine"."InvoiceLineId" = 37;
```

10. Looking at the InvoiceLine table, provide a query that COUNTs the number of line items for each Invoice. HINT: GROUP BY
```sql
SELECT
	"InvoiceLine"."InvoiceId" AS "InvoiceId",
	COUNT("InvoiceLine"."InvoiceId")
FROM
	"InvoiceLine"
	GROUP BY("InvoiceId");
```

11. Provide a query that includes the track name with each invoice line item. 
```sql
SELECT 
	"Track"."Name" AS "trackName",
	"InvoiceLine".*
FROM
	"Track"
	JOIN "InvoiceLine" USING("TrackId");
```

12. Provide a query that includes the purchased track name AND artist name with each invoice line item.
```sql
SELECT 
	"Artist"."Name" AS "NameArtist",
	"Track"."Composer",
	"Track"."Name" AS "NameTrack",
	"InvoiceLine"."InvoiceId"
FROM 
	"Artist"
	JOIN "Album" USING("ArtistId")
	JOIN "Track" USING("AlbumId")
	JOIN "InvoiceLine" USING("TrackId");
```

13. Provide a query that shows the # of invoices per country. HINT: GROUP BY 
```sql
SELECT 
	"Invoice"."BillingCountry", 
	COUNT(*) AS "Number_of_Invoices"
FROM 
	"Invoice"
GROUP BY ("Invoice"."BillingCountry")
ORDER BY ("Number_of_Invoices") ASC;
```

14. Provide a query that shows the total number of tracks in each playlist. The Playlist name should be included on the resultant table. 
```sql
SELECT 
	"Playlist"."Name" AS "Name_Playlist", 
	COUNT(*) AS "Number_of_Tracks"
FROM 
	"PlaylistTrack"
	JOIN "Playlist" USING("PlaylistId")
	JOIN "Track" USING("TrackId")
	JOIN "InvoiceLine" USING("TrackId")
	JOIN "Invoice" USING("InvoiceId")
GROUP BY ("Playlist"."Name")
ORDER BY ("Number_of_Tracks") ASC;
```

15. Provide a query that shows all the Tracks, but displays no IDs. The resultant table should include the Album name, Media type and Genre.
```sql
SELECT 
	"Track"."Name" AS "TrackName",
	"Album"."Title" AS "AlbumTitle",
	"Genre"."Name" AS "Genre",
	"MediaTypeId" AS "MediaType"
FROM 
	"Track"
	JOIN "Album" USING("AlbumId")
	JOIN "Genre" USING("GenreId")
	JOIN "MediaType" USING("MediaTypeId");
```

16. Provide a query that shows all Invoices but includes the # of invoice line items. 
```sql
SELECT 
	"Invoice".*, 
	COUNT("InvoiceLine"."InvoiceId") AS "ofLineItems"
FROM 
	"InvoiceLine"
	JOIN "Invoice" USING("InvoiceId")
GROUP BY ("Invoice"."InvoiceId");
```

17. Provide a query that shows total sales made by each sales agent.
```sql
SELECT 
	DISTINCT "Employee"."LastName" || ' ' || "Employee"."FirstName" AS "SalesAgent",
	SUM("Invoice"."Total") AS "Total"
FROM
	"Customer"
	JOIN "Employee" ON "Customer"."SupportRepId" = "Employee"."EmployeeId"
	JOIN "Invoice" USING("CustomerId")
GROUP BY ("SalesAgent")
ORDER BY ("Total") DESC;
```

18. Which sales agent made the most in sales in 2009?
```sql
SELECT 
	DISTINCT "Employee"."LastName" || ' ' || "Employee"."FirstName" AS "SalesAgent",
	SUM("Invoice"."Total") AS "Total"
FROM
	"Customer"
	JOIN "Employee" ON "Customer"."SupportRepId" = "Employee"."EmployeeId"
	JOIN "Invoice" USING("CustomerId")
WHERE 
	"Invoice"."InvoiceDate" BETWEEN '2009-01-01' AND '2009-12-31'
GROUP BY ("SalesAgent")
ORDER BY ("Total") DESC
LIMIT 1;
```

19. Which sales agent made the most in sales in 2010?
```sql
SELECT 
	DISTINCT "Employee"."LastName" || ' ' || "Employee"."FirstName" AS "SalesAgent",
	SUM("Invoice"."Total") AS "Total"
FROM
	"Customer"
	JOIN "Employee" ON "Customer"."SupportRepId" = "Employee"."EmployeeId"
	JOIN "Invoice" USING("CustomerId")
WHERE 
	"Invoice"."InvoiceDate" BETWEEN '2010-01-01' AND '2010-12-31'
GROUP BY ("SalesAgent")
ORDER BY ("Total") DESC
LIMIT 1;
```

20. Which sales agent made the most in sales over all?
```sql
SELECT 
	DISTINCT "Employee"."LastName" || ' ' || "Employee"."FirstName" AS "SalesAgent",
	SUM("Invoice"."Total") AS "Total"
FROM
	"Customer"
	JOIN "Employee" ON "Customer"."SupportRepId" = "Employee"."EmployeeId"
	JOIN "Invoice" USING("CustomerId")
GROUP BY ("SalesAgent")
ORDER BY ("Total") DESC
LIMIT 1;
```

21. Provide a query that shows the # of customers assigned to each sales agent. 
```sql
SELECT 
	"Employee"."LastName" || ' ' || "Employee"."FirstName" AS "SalesAgent",
	COUNT("Customer"."SupportRepId") AS "TopSalesAgent"
FROM
	"Customer"
	JOIN "Employee" ON "Customer"."SupportRepId" = "Employee"."EmployeeId"
	JOIN "Invoice" USING("CustomerId")
GROUP BY ("SalesAgent")
ORDER BY ("TopSalesAgent") DESC
LIMIT 1;
```

22. Provide a query that shows the total sales per country. Which country's customers spent the most?
```sql
SELECT
	DISTINCT "Invoice"."BillingCountry" AS "Country",
	SUM("Invoice"."Total") AS "Total"
FROM 
	"Invoice"
GROUP BY ("Country")
ORDER BY ("Total") DESC
LIMIT 1;
```

23. Provide a query that shows the most purchased track of 2013.
```sql
SELECT
	"Track"."Composer" AS "ComposerName",
	COUNT("InvoiceLine"."InvoiceLineId") AS "topComposer"
FROM 
	"Track"
	JOIN "InvoiceLine" USING("TrackId")
	JOIN "Invoice" USING("InvoiceId")
WHERE 
	"Invoice"."InvoiceDate" BETWEEN  '2013-01-01' AND '2013-12-31'
GROUP BY ("ComposerName")
ORDER BY ("topComposer") DESC
LIMIT 1;
```

24. Provide a query that shows the top 5 most purchased tracks over all. 
```sql
SELECT 
	"Track"."Name",
	COUNT("InvoiceLine"."InvoiceLineId") AS "topTrack"
FROM 
	"Track"
	JOIN "InvoiceLine" USING("TrackId")
GROUP BY ("Track"."Name")
ORDER BY ("topTrack") DESC
LIMIT 5;
```

25. Provide a query that shows the top 3 best selling artists.
```sql
SELECT 
	"Artist"."Name" AS "Artist",
	COUNT("InvoiceLine"."InvoiceLineId") AS "topArtist"
FROM 
	"Album"
	JOIN "Artist" USING("ArtistId")
	JOIN "Track" USING("AlbumId")
	JOIN "InvoiceLine" USING("TrackId")
GROUP BY ("Artist")
ORDER BY ("topArtist") DESC
LIMIT 3;
```

26. Provide a query that shows the most purchased Media Type. 
```sql
SELECT 
	"MediaType"."Name" AS "MediaType",
	COUNT("InvoiceLine"."InvoiceLineId") AS "topMediaType"
FROM 
	"Track"
	JOIN "MediaType" USING("MediaTypeId")
	JOIN "InvoiceLine" USING("TrackId")
GROUP BY ("MediaType")
ORDER BY ("topMediaType") DESC
LIMIT 1;
```

27. Provide a query that shows the number tracks purchased in all invoices that contain more than one genre. 
```sql
SELECT
	DISTINCT "MediaType"."Name",
	COUNT("Track"."TrackId") AS "PurchasedСompositions"
FROM 
	"Track"
	JOIN "MediaType" USING("MediaTypeId")
	JOIN "Genre" USING("GenreId")
	JOIN "InvoiceLine" USING("TrackId")
	JOIN "Invoice" USING("InvoiceId")
WHERE
	"Track"."GenreId" > 1
GROUP BY ("MediaType"."Name")
ORDER BY ("PurchasedСompositions") DESC;
```


### EMD SCHEME:
![](https://user-images.githubusercontent.com/40778282/84611232-34ef3300-ae8b-11ea-8f43-b5a70a750e62.png)









