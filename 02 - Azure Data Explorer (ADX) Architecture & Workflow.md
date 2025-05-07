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

1. Visit the [ADX Architecture Documentation](https://learn.microsoft.com/en-us/azure/data-explorer/data-explorer-overview).
