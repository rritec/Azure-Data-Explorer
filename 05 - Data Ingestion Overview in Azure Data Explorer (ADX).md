## 🔹 What is Data Ingestion?

**Data Ingestion** is the process of **loading data into ADX** tables so it can be queried using **KQL (Kusto Query Language)**.

---

## ✅ Supported Data Formats

ADX supports ingestion from various formats:

| Format             | Description                                |
|--------------------|--------------------------------------------|
| CSV                | Comma-separated values                     |
| JSON               | Semi-structured data                       |
| Parquet            | Columnar data format                       |
| Avro               | Row-based format for Hadoop systems        |
| ORC                | Optimized Row Columnar format              |
| TSV, PSV           | Tab/pipe-separated values                  |
| Single JSON object | For small payloads                         |

---

## Load data from blob

1. Click on Mycluster > Click on Ingest
2. Click on Azure Storage
3. Click on New Table
4. Name it as StromEvents
5. Click on add ARL > paster this url https://kustosamples.blob.core.windows.net/samplefiles/StormEvents.csv
6. Click on +
7. Click on Next

![image](https://github.com/user-attachments/assets/7ee2f0b3-d828-49cd-a302-ec53a8e8ee30)

8. Click on Finish > Click on Close

## Load data from Local System file emp.csv

1. Click on Mycluster > Click on Ingest
2. Click on Local File
3. Click on New Table
4. Name it as emp
5. browse and select emp.csv
6. Click on Next
7. Click on Finish > Click on Close
