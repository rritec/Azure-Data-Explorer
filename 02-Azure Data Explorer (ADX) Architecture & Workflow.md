## 📘 Chapter 2: Azure Data Explorer (ADX) Architecture & Workflow

### 🎯 Objective

Understand the architectural components of Azure Data Explorer and how data flows through the system.

### 📖 Key Concepts

* **Core Components:**

  * **Clusters:** The top-level container for ADX resources.
  * **Databases:** Logical containers within clusters to organize data.
  * **Tables:** Structured datasets organized in tabular form.
  * **Columns:** Each table has columns with specific data types.

* **ADX Workflow Overview:**

  1. **Ingestion:** Data is ingested in real-time or batch mode from multiple sources.
  2. **Indexing & Storage:** Ingested data is stored in columnar format and indexed for fast retrieval.
  3. **Querying:** Users query data using Kusto Query Language (KQL).
  4. **Visualization & Export:** Results can be visualized in dashboards or exported to other tools.

* **Supported Ingestion Sources:**

  * Azure Blob Storage
  * Event Hubs
  * IoT Hub
  * Azure Data Factory
  * Local files

* **ADX Engine Tiers:**

  * **Data Management Engine** – handles ingestion
  * **Query Engine** – handles queries and optimizations

### 🧪 Hands-On Exercise

> 🛠️ **Goal:** Understand how data flows through Azure Data Explorer.

**Steps:**

1. Visit the [ADX Architecture Documentation](https://learn.microsoft.com/en-us/azure/data-explorer/data-explorer-overview).
2. Study the diagram and note the stages: Ingestion → Storage → Query → Visualization.
3. Draw a simplified version of the architecture in your notebook or using a tool like Lucidchart or draw\.io.

### ✅ Outcomes

* Learned about the structure of ADX (clusters, databases, tables).
* Understood the flow of data and core components.
* Identified ingestion sources and engine roles in ADX.

---

## 📘 Chapter 3: Provision Azure Data Explorer (ADX) Cluster and Database

*Coming up next...*
