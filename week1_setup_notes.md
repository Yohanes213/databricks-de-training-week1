# Week 1 Setup Notes

## Databricks Workspace
I created a cluster named `my-first-cluster` in the East US region with the following configuration:

### Cluster Configuration
- **Worker Type:** Standard_D4pds_v6 (16 GB Memory, 4 Cores)
- **Autoscaling:** Enabled (Min Workers: 1, Max Workers: 1)
- **Driver Type:** Same as Worker (Standard_D4pds_v6)
- **Photon Acceleration:** Enabled
- **Auto Termination:** 10 minutes of inactivity
- **Databricks Runtime Version:** 16.4 LTS (includes Apache Spark 3.5.2, Scala 2.13)

Below is a screenshot of the configuration for `my-first-cluster`:


## Data Exploration Findings

I created a `mock_sales_data.csv` file with 30 rows and 9 columns:

| Column Name      | Data Type  |
|------------------|------------|
| TransactionID    | String     |
| TransactionDate  | Timestamp  |
| CustomerID       | String     |
| Product          | String     |
| ProductCategory  | String     |
| Quantity         | Integer    |
| SaleAmount       | Double     |        
| PaymentMethod    | String     |
| StoreLocation    | String     |

### Key Insights

- The product **Monitor** generated the highest total sales ($2,837.46).
- **PayPal** was the most frequently used payment method.
- **Electronics** was the top product category by sales.
- Most customers made purchases online.
- The `PaymentMethod` column contained 6 null values.

### Data Transformation & Cleansing

- Added a new column, `TransactionTimestamp`, by converting `TransactionDate` to a timestamp data type.
- Created a `TotalItemCost` column by multiplying `SaleAmount` and `Quantity`.
- Replaced missing values in the `PaymentMethod` column with "Unknown".
- Saved the preprocessed data to DBFS in Parquet format.

## Challenges Faced

- **Cluster Creation Authorization:**  
  Initially, I encountered authorization issues when attempting to create a cluster.

- **Data Upload and Access:**  
  At first, I uploaded the data file directly to Databricks, but was unable to access it from my notebook. I later learned that files should be uploaded to DBFS (Databricks File System) for seamless access within notebooks. After re-uploading the file to DBFS, I was able to proceed without issues.

## Self-Reflection

The most challenging part of this week was resolving the initial cluster authorization issue, as it required troubleshooting permissions and understanding how access controls work within Azure Databricks. Additionally, learning the correct way to upload and access data in Databricks (using DBFS) was a valuable lesson after some initial confusion.

The most interesting discovery was seeing how powerful and flexible PySpark and Databricks notebooks are for data exploration and transformation. I enjoyed using both Python and SQL within the same environment, and appreciated how easy it was to perform data cleansing, create new columns, and save processed data in efficient formats like Parquet.

Throughout this week, I gained several important skills and knowledge:
- Learned the fundamentals of Spark, including basic DataFrame operations such as `filter`, `count`, and column selection.
- Developed an understanding of key Databricks and Spark concepts and terminology, such as driver, worker, Photon, DBU (Databricks Unit), and DBFS (Databricks File System).
- Built a basic understanding of cloud computing concepts within Azure, specifically as they relate to Databricks and resource management.
- Gained some experience with the Azure CLI for resource setup and management.
- Became comfortable navigating and utilizing the Databricks workspace, including clusters, notebooks, and data management features.

I am still curious about best practices for managing larger datasets, optimizing cluster costs, and how to automate more of the data pipeline process within Databricks. I look forward to exploring these topics in future weeks.