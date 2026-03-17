# Kusto Query Language (KQL) Examples using `emp` and `dept` Tables


## 📌 1. Kusto Query Language (KQL) Overview
KQL is a powerful query language for Azure Data Explorer (ADX) used to explore large volumes of structured and semi-structured data.

## 🖥️ 2. Kusto Explorer Installation and User Interface
- install Kusto Explorer is a desktop tool for running KQL queries https://learn.microsoft.com/en-us/kusto/tools/kusto-explorer?view=microsoft-fabric
- Alternatively, use https://dataexplorer.azure.com/freecluster.

## 3. Create Free Cluster
1. Click on https://dataexplorer.azure.com/freecluster > my clusters > create free cluster
## 4. Create table
```kql
.create table Logs(Level:string ,Text:string);

.show tables ;

.ingest inline into table Logs <|
"INFO", "System initialized successfully"
"WARN", "Disk usage is reaching 85%"
"ERROR", "Failed to connect to database"
"INFO", "User logged in"
"DEBUG", "Fetching user preferences"
"INFO", "Cache refresh completed"
"WARN", "Low memory warning triggered"
"INFO", "Scheduled task executed"
"ERROR", "Timeout occurred while fetching data"
"INFO", "Health check passed"
"DEBUG", "Session token generated"
"WARN", "Unusual network latency detected"
"INFO", "Service restarted after crash"
"ERROR", "Authentication failed for user"
"INFO", "New configuration deployed"
"DEBUG", "Retry logic engaged on API call"
"WARN", "Unexpected payload format"
"INFO", "Backup completed successfully"
"ERROR", "Disk write operation failed"
"INFO", "User logged out";

Logs
| take 6;

```

## 5. Add help cluster

[06 - Add help cluster](https://github.com/rritec/Azure-Data-Explorer/blob/main/06%20-%20Add%20help%20cluster.md)


## 💬 6. Add a Comment in KQL
```kql
// This is a single-line comment
```

## 📛 7. Count rows
```kql
StormEvents 
| count

```

## 📥 8. See a sample of data
```kql
StormEvents 
| take 5
```

## 📦 9. Select a subset of columns

```kql
StormEvents
| take 5
| project State, EventType, DamageProperty
```

## 📦 10. List unique values

```kql
StormEvents 
| distinct EventType
```

## 📦 11. Sort results

```kql
StormEvents
| where State == 'TEXAS' and EventType == 'Flood'
| sort by DamageProperty
| project StartTime, EndTime, State, EventType, DamageProperty
```
## 📦 12. Filter by condition

```kql
StormEvents
| where State == 'TEXAS' and EventType == 'Flood'
| project StartTime, EndTime, State, EventType, DamageProperty
```
## 📦 13.Filter by date and time range

```kql
StormEvents
| where StartTime between (datetime(2007-08-01 00:00:00) .. datetime(2007-08-30 23:59:59))
| project State, EventType, StartTime, EndTime
| sort by StartTime asc
```
## 📦 14. Get the top n rows

```kql
StormEvents
| where State == 'TEXAS' and EventType == 'Flood'
| top 5 by DamageProperty
| project StartTime, EndTime, State, EventType, DamageProperty
```
## 📦 15. Create calculated columns

```kql
StormEvents
| where State == 'TEXAS' and EventType == 'Flood'
| top 5 by DamageProperty desc
| project StartTime, EndTime, Duration = EndTime - StartTime, DamageProperty
```
```kql
StormEvents
| where State == 'TEXAS' and EventType == 'Flood'
| top 5 by DamageProperty desc
| extend Duration = EndTime - StartTime
```
## 📦 16. Map values from one set to another

```kql
let sourceMapping = dynamic(
  {
    "Emergency Manager" : "Public",
    "Utility Company" : "Private"
  });
StormEvents
| where Source == "Emergency Manager" or Source == "Utility Company"
| project EventId, Source, FriendlyName = sourceMapping[Source]
```


## 🧱 17. `datatable()` Operator in KQL
```kql
let demo = datatable(id:int, name:string)[1, "Alice", 2, "Bob"];
demo
```

## 🔢 18. `count()` & `distinct()` Operators
```kql
emp | count;
emp | distinct job
```

## 🔍 19. `project` Operator
```kql
emp | project empno, ename, sal;
```

## ✂️ 20. `project-away` & `project-keep`
```kql
emp | project-away comm, mgr;
emp | project-keep empno, job
```

## 🔄 21. `project-rename` & `project-reorder`
```kql
emp | project-rename EmployeeName = ename;
emp | project-reorder empno, deptno, ename;
```

## 🧬 22. `getschema` Operator
```kql
emp | getschema;
```

## 🖨️ 23. `print` Operator
```kql
print now = now(), version = "KQL";
```

## ➗ 24. `range` Operator
```kql
range x from 1 to 10 step 2;
```

## 🔍 25. `where` & `filter` Operators
```kql
emp | where job == "CLERK";
```

## 🎯 26. `take` & `limit` Operators
```kql
emp | take 5;
emp | limit 5
```

## 🏆 27. `top` Operator
```kql
emp | top 3 by sal desc
```
```kql
Emp | sort by sal asc | take 3
```

## ➕ 28. `extend` Operator
```kql
emp | extend annual_salary = sal * 12
```

## 📊 29. `union` Operator
```kql
let by_dept = emp
| summarize count() by deptno;


let by_job = emp
| summarize count() by job;

union 
(by_dept | project Category="ByDept", Label=deptno, Count=count_),
(by_job | project Category="ByJob", Label=job, Count=count_)
```


## 🎲 30. `sample` Operator
```kql
emp | sample 3
```
## Joins

```kql
emp
| join kind=inner (
    dept
    | project deptno, dname
) on $left.deptno == $right.deptno
| summarize total_sal = sum(sal) by dname
```

```kql
emp
| join kind=leftouter (
    dept
    | project deptno, dname
) on $left.deptno == $right.deptno
| summarize total_sal = sum(sal) by dname
```

```kql
emp
| join kind=rightouter (
    dept
    | project deptno, dname
) on $left.deptno == $right.deptno
| summarize total_sal = sum(sal) by dname
```

```kql
emp
| join kind=fullouter (
    dept
    | project deptno, dname
) on $left.deptno == $right.deptno
| summarize total_sal = sum(sal) by dname
```
## Explain

1. If you're familiar with SQL and want to learn KQL, translate SQL queries into KQL by prefacing the SQL query with a comment line, --, and the keyword explain. The output shows the KQL version of the query, which can help you understand the KQL syntax and concepts.

```kql
explain
select dname,sum(sal) as total_sal from emp inner join dept on emp.deptno=dept.deptno group by dname
```
## Reference:

1. https://learn.microsoft.com/en-in/kusto/query/sql-cheat-sheet?view=azure-data-explorer&preserve-view=true
2. 
