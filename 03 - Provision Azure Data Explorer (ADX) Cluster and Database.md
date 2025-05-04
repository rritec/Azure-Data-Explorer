## 📘 Chapter 3: Provision Azure Data Explorer (ADX) Cluster and Database

### 🎯 Objective

Provision a new Azure Data Explorer cluster and create a database within it using the Azure Portal.

### 📖 Key Concepts

* **Cluster:** The top-level resource in ADX, providing the compute and storage infrastructure.
* **Database:** A logical grouping of tables, functions, and data policies within a cluster.
* **Region:** The Azure region where the cluster will be created (e.g., East US, West Europe).
* **SKU:** Determines the performance tier and pricing.

### 🧪 Hands-On Exercise

> 🛠️ **Goal:** Create an ADX Cluster and Database in Azure Portal.

**Steps:**

1. Log in to [Azure Portal](https://portal.azure.com).
2. Search for **Azure Data Explorer Clusters** in the search bar and click **Create**.
3. Fill in the required fields:

   * **Subscription** and **Resource Group**
   * **Cluster Name** (e.g., `adx-demo-cluster`)
   * **Region** (choose closest to your location)
   * **Performance Tier** (Dev/Test or Production)
4. Click **Next: Scale**, accept defaults, and proceed.
5. Click **Review + Create**, then **Create**.
6. Once the cluster is provisioned (takes 2–3 minutes), go to the resource.
7. In the left menu, click **Databases** > **Add Database**.
8. Enter a name for the database (e.g., `demo-db`) and retention policy (e.g., 365 days).
9. Click **Create**.

### ✅ Outcomes

* Successfully provisioned an Azure Data Explorer cluster.
* Created a database within the cluster.
* Understood basic configuration options while provisioning ADX resources.

---
