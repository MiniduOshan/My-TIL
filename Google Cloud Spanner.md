# TIL: Google Cloud Spanner

**Date:** August 10, 2026

## What I Learned

Today I learned how to create and manage a **Google Cloud Spanner** database using the Google Cloud Console and `gcloud` CLI.

Cloud Spanner is a fully managed, globally scalable relational database service provided by Google Cloud. In the challenge lab, I worked with Spanner from the command line and practiced common database administration tasks.

---

## 1. Creating a Cloud Spanner Instance

I learned how to create a Spanner instance using the `gcloud` CLI.

```bash
gcloud spanner instances create banking-ops-instance \
  --config=regional-us-west1 \
  --description="Banking Operations Instance" \
  --nodes=1
```

The instance was configured with:

* **Instance:** `banking-ops-instance`
* **Region:** `us-west1`
* **Nodes:** 1

---

## 2. Creating a Spanner Database

After creating the instance, I created a database inside it:

```bash
gcloud spanner databases create banking-ops-db \
  --instance=banking-ops-instance
```

The database was named:

```text
banking-ops-db
```

A Spanner database exists inside a Spanner instance and contains the application's tables and data.

---

## 3. Creating Tables with DDL

I learned how to create tables using **DDL (Data Definition Language)**.

The database contained four tables:

* `Portfolio`
* `Category`
* `Product`
* `Customer`

For example:

```sql
CREATE TABLE Customer (
  CustomerId STRING(36) NOT NULL,
  Name STRING(MAX) NOT NULL,
  Location STRING(MAX) NOT NULL
) PRIMARY KEY (CustomerId);
```

The primary key uniquely identifies each customer.

---

## 4. Loading Data with SQL

I learned how to insert multiple records into Spanner using SQL.

For example:

```sql
INSERT INTO Portfolio
(PortfolioId, Name, ShortName, PortfolioInfo)
VALUES
(1, "Banking", "Bnkg", "All Banking Business"),
(2, "Asset Growth", "AsstGrwth", "All Asset Focused Products"),
(3, "Insurance", "Insurance", "All Insurance Focused Products");
```

I also loaded data into the `Category` and `Product` tables.

---

## 5. Loading a Large Dataset

One of the more interesting parts was loading the `Customer` table with a larger dataset.

The CSV file was provided through Google Cloud Storage:

```text
gs://spls/gsp381/Customer_List_500.csv
```

I downloaded it using:

```bash
gsutil cp gs://spls/gsp381/Customer_List_500.csv .
```

The file contained **500 customer records**.

I learned that CSV files without headers should be processed using `csv.reader()` instead of `csv.DictReader()`.

---

## 6. Verifying Data

I learned that database operations should be verified after execution.

For example, I could check the number of customers using:

```sql
SELECT COUNT(*) AS CustomerCount
FROM Customer;
```

The expected result was:

```text
CustomerCount: 500
```

This is useful for confirming that the complete dataset was successfully loaded.

---

## 7. Altering an Existing Table

I also learned how to modify an existing Spanner table using DDL.

The task required adding a `MarketingBudget` column to the `Category` table.

```bash
gcloud spanner databases ddl update banking-ops-db \
  --instance=banking-ops-instance \
  --ddl='ALTER TABLE Category ADD COLUMN MarketingBudget INT64;'
```

This demonstrated how an existing database schema can be changed without recreating the table.

---

## 8. Useful Spanner CLI Commands

Some commands I practiced today:

### List instances

```bash
gcloud spanner instances list
```

### List databases

```bash
gcloud spanner databases list \
  --instance=banking-ops-instance
```

### View database schema

```bash
gcloud spanner databases ddl describe banking-ops-db \
  --instance=banking-ops-instance
```

### Execute SQL

```bash
gcloud spanner databases execute-sql banking-ops-db \
  --instance=banking-ops-instance \
  --sql='SELECT * FROM Customer;'
```

---

## Key Takeaways

Today I learned that Google Cloud Spanner can be managed efficiently using the `gcloud` CLI. I practiced the complete basic database workflow:

```text
Create Instance
      ↓
Create Database
      ↓
Create Tables
      ↓
Insert Data
      ↓
Load Large Dataset
      ↓
Verify Data
      ↓
Modify Schema
```

The main concepts I learned were **Spanner instances, databases, tables, primary keys, DDL, DML, bulk data loading, SQL queries, and schema modification**.

### What I want to learn next

* Spanner indexes
* Interleaved tables
* Foreign keys
* Query performance
* Spanner backups and restores
* Spanner replication
* Multi-region configurations
* Spanner monitoring
* Dataflow-based bulk loading
