# Challenge Set 9
## Part I: W3Schools SQL Lab 

*Introductory level SQL*

--

This challenge uses the [W3Schools SQL playground](http://www.w3schools.com/sql/trysql.asp?filename=trysql_select_all). Please add solutions to this markdown file and submit.

1. Which customers are from the UK?
SELECT CustomerName 
FROM Customers WHERE Country = 'UK';

    Around the Horn
    B's Beverages
    Consolidated Holdings
    Eastern Connection
    Island Trading
    North/South
    Seven Seas Imports

2. What is the name of the customer who has the most orders?
SELECT CustomerName, Count(OrderID) 
FROM Orders 
INNER JOIN Customers ON Orders.CustomerID = Customers.CustomerID 
GROUP BY CustomerName 
ORDER BY COUNT(OrderID) DESC;
        
    Ernst Handel

3. Which supplier has the highest average product price?
SELECT SupplierName, MAX(AveragePrice)
FROM (SELECT SupplierName, AVG(Price) AS AveragePRICE 
	FROM Suppliers 
	INNER JOIN Products ON Suppliers.SupplierID = Products.SupplierID
    GROUP BY SupplierName);

    Aux joyeux ecclésiastiques

4. How many different countries are all the customers from? (*Hint:* consider [DISTINCT](http://www.w3schools.com/sql/sql_distinct.asp).)
SELECT DISTINCT(Country) FROM Customers; 
       
    21

5. What category appears in the most orders?
SELECT CategoryName, Categories.CategoryID, COUNT(OrderID) 
FROM OrderDetails 
INNER JOIN Products ON OrderDetails.ProductID = Products.ProductID 
INNER JOIN Categories ON Products.CategoryID = Categories.CategoryID 
GROUP BY CategoryName 
ORDER BY COUNT(OrderID) DESC;
    
    Dairy Products
    

6. What was the total cost for each order?
SELECT OrderID, Sum(Quantity*Price) 
FROM Products 
INNER JOIN OrderDetails ON Products.ProductID = OrderDetails.ProductID 
GROUP BY OrderID 
ORDER BY OrderID DESC;          
    
    Each order:
        OrderID	Sum(Quantity*Price)
10443	673.2
10442	2246
10441	2195
10440	7246.01
10439	1348.7
10438	710.5
10437	491.99999999999994
10436	2763.5
10435	790
10434	450
10433	1064
10432	610.3
10431	3155
10430	7245
10429	2186.5
10428	240
10427	813.75
10426	422.75
10425	600
10424	14366.5
10423	1275
10422	62.46
10421	1595.6999999999998
10420	2372
10419	2760
10418	2268.5
10417	14104
10416	902
10415	128
10414	290.6
10413	2656
10412	465
10411	1514.25
10410	1002.5
10409	399
10408	2030.2
10407	1492.5
10406	2527
10405	500
10404	2096.9
10403	1258.95
10402	3393.5
10401	4837.02
10400	3829.59
10399	2207
10398	3420
10397	1054
10396	2380.8
10395	2920
10394	553
10393	4135.6
10392	1800
10391	108
10390	2845.2
10389	2292
10388	1594.5
10387	1323.6
10386	207.5
10385	1080
10384	2778
10383	1123.75
10382	3628.76
10381	140
10380	1776.02
10379	1200.6
10378	129
10377	1272
10376	525
10375	423.25
10374	573.75
10373	2135
10372	15353.6
10371	114
10370	1467.5
10369	3159.8
10368	2294.05
10367	1044.85
10366	170.25
10365	504
10364	1187.5
10363	559
10362	1938.8
10361	2842
10360	9244.250000000002
10359	4572.2
10358	565
10357	1701.68
10356	1383
10355	600
10354	711.1600000000001
10353	13427
10352	194
10351	7103.599999999999
10350	891.75
10349	178.8
10348	495
10347	1160.1
10346	2164
10345	3662
10344	3570
10343	1982.5
10342	2876
10341	515
10340	3205.8
10339	4330.4
10338	1168.35
10337	3087.52
10336	396
10335	3181.5
10334	181
10333	1192.5
10332	2792
10331	111.75
10330	2431.5
10329	6025.12
10328	1462
10327	2828.65
10326	1227.5
10325	1873.25
10324	7698.45
10323	205.5
10322	140
10321	180
10320	645
10319	1490.4
10318	301
10317	360
10316	3547.5
10315	646
10314	2910
10313	228
10312	2019.9
10311	336
10310	421
10309	2202.5
10308	111
10307	530.5
10306	624.15
10305	5197.25
10304	1193
10303	1555
10302	3388.8
10301	944
10300	760
10299	438
10298	3909.5
10297	1776
10296	1315.5
10295	152
10294	2359.5
10293	1061
10292	1620
10291	692.8
10290	2713.8500000000004
10289	599.25
10288	112
10287	1158
10286	3772
10285	2726.8
10284	1816.95
10283	1770
10282	194.34
10281	108.2
10280	766.5
10279	585
10278	1862.4
10277	1503.6
10276	525
10275	384
10274	673.5999999999999
10273	2679.5
10272	1821.1999999999998
10271	60
10270	1720
10269	846
10268	1377.1000000000001
10267	5040
10266	456
10265	1470
10264	906.25
10263	3086.4
10262	782.2
10261	560
10260	2183.9
10259	126
10258	2529.75
10257	1400.5
10256	648
10255	3115.75
10254	781.5
10253	1806
10252	4662.5
10251	839.5
10250	2267.25
10249	2329.25
10248	566

    Total = $386,424.23

7. Which employee made the most sales (by total price)?
SELECT (FirstName || ' ' || LastName) AS EmployeeName, Employees.EmployeeID, COUNT(DISTINCT Orders.OrderID), SUM(Quantity*Price) 
FROM Products 
INNER JOIN OrderDetails ON Products.ProductID = OrderDetails.ProductID 
INNER JOIN Orders ON OrderDetails.OrderID = Orders.OrderID
INNER JOIN Employees ON Orders.EmployeeID = Employees.EmployeeID
GROUP BY Employees.EmployeeID
ORDER BY SUM(Quantity*Price) DESC;

    Margaret Peacock

8. Which employees have BS degrees? (*Hint:* look at the [LIKE](http://www.w3schools.com/sql/sql_like.asp) operator.)
SELECT (FirstName || ' ' || LastName) AS EmployeeName 
FROM Employees
WHERE Notes LIKE '%BS%';

    Janet Leverling
    Steven Buchanan

9. Which supplier of three or more products has the highest average product price? (*Hint:* look at the [HAVING](http://www.w3schools.com/sql/sql_having.asp) operator.)
SELECT SupplierName, Max(AveragePrice)
FROM (SELECT SupplierName, Suppliers.SupplierID, AVG(Price) AS AveragePrice, COUNT(ProductID)
    FROM Suppliers 
    INNER JOIN Products ON Suppliers.SupplierID = Products.SupplierID 
    GROUP BY SupplierName 
    HAVING COUNT(ProductID) >= 3);
    
    Tokyo Traders
