# Kusto Query Language (KQL) Examples using `emp` and `dept` Tables


## 📌 1. Kusto Query Language (KQL) Overview
KQL is a powerful query language for Azure Data Explorer (ADX) used to explore large volumes of structured and semi-structured data.

## 🖥️ 2. Kusto Explorer Installation and User Interface
- install Kusto Explorer is a desktop tool for running KQL queries https://learn.microsoft.com/en-us/kusto/tools/kusto-explorer?view=microsoft-fabric
- Alternatively, use https://dataexplorer.azure.com/freecluster.

## Create Free Cluster
1. Click on https://dataexplorer.azure.com/freecluster > my clusters > create free cluster
## Create table
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

## Add help cluster

[06 - Add help cluster](https://github.com/rritec/Azure-Data-Explorer/blob/main/06%20-%20Add%20help%20cluster.md)
## 💬 3. Add a Comment in KQL
```kql
// This is a single-line comment
```

## 📛 4. Alias Statement in KQL
```kql
emp 
| take 10
| as employee 

```

## 📥 5. Query Parameters Declaration Statement in KQL
```kql
let min_salary = 2000;
emp
| where sal > min_salary
```

## 📦 6. Batches in KQL
Run multiple queries together:
```kql
emp | count;
dept | count
```

## 🧱 7. `datatable()` Operator in KQL
```kql
let demo = datatable(id:int, name:string)[1, "Alice", 2, "Bob"];
demo
```

## 🔢 8. `count()` & `distinct()` Operators
```kql
emp | count;
emp | distinct job
```

## 🔍 9. `project` Operator
```kql
emp | project empno, ename, sal;
```

## ✂️ 10. `project-away` & `project-keep`
```kql
emp | project-away comm, mgr;
emp | project-keep empno, job
```

## 🔄 11. `project-rename` & `project-reorder`
```kql
emp | project-rename EmployeeName = ename;
emp | project-reorder empno, deptno, ename;
```

## 🧬 12. `getschema` Operator
```kql
emp | getschema;
```

## 🖨️ 13. `print` Operator
```kql
print now = now(), version = "KQL";
```

## ➗ 14. `range` Operator
```kql
range x from 1 to 10 step 2;
```

## 🔍 15. `where` & `filter` Operators
```kql
emp | where job == "CLERK";
```

## 🎯 16. `take` & `limit` Operators
```kql
emp | take 5;
emp | limit 5
```

## 🏆 17. `top` Operator
```kql
emp | top 3 by sal desc
```

## ➕ 18. `extend` Operator
```kql
emp | extend annual_salary = sal * 12
```

## 📊 19. `union` Operator
```kql
let by_dept = emp
| summarize count() by deptno;


let by_job = emp
| summarize count() by job;

union 
(by_dept | project Category="ByDept", Label=deptno, Count=count_),
(by_job | project Category="ByJob", Label=job, Count=count_)
```


## 🎲 20. `sample` Operator
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

```kql
explain
select dname,sum(sal) as total_sal from emp inner join dept on emp.deptno=dept.deptno group by dname
```
## Reference:

1. https://learn.microsoft.com/en-in/kusto/query/sql-cheat-sheet?view=azure-data-explorer&preserve-view=true
2. 
