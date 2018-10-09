---
layout: post
title:      "Database Normalization"
date:       2018-10-09 22:08:03 +0000
permalink:  database_normalization
---


When designing a SQL Database, there are general rules that should always be followed to minimize duplicate data, minimize or avoid modification issues, and to simplify queries. Firstly, each table should only serve one purpose and should store one type of data. For example, if you had a database for a business, the employees, offices, and customers should all have a separate table. Otherwise, a lot of data will be duplicated; for example, if two employees were working with the same customers, that customer name would appear twice. Duplicate data poses the problems of decreasing performance and also maintaining data changes. Insert, update, and delete anomalies can all result as an effect. 

Insert anomaly- In our example, suppose we had a customer but didn't yet know the employee he would be assigned to; this poses a problem as we would be unable to enter the customer in a row without entering the employee, as the ID column is the employee ID. 

Update anomaly- In our example, if a customer leaves the business, the customer's name would need to be removed from all the rows its mentioned it; otherwise, an inconsistency would occur.

Delete anomaly- In our example, if an employee quits and we need to remove his name, we could lose valuable information about some of our customers too since they're stored in the same row. 


