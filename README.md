
# Database Pipeline: SQL Generation to Validation

This repository contains a 4-step pipeline for processing CSVs, generating SQL, loading data into a database, and applying constraints/indexes. Each step is implemented in a Jupyter Notebook. Run them in numerical order.

## 📂 Notebooks Overview

| Step | File Name                                      | Description |
|------|------------------------------------------------|-------------|
| 1    | `1__generate_sql.ipynb`                        | Generates SQL schema and table definitions based on input metadata or logic. |
| 2    | `2__preprocess_CSVs.ipynb`                     | Processes and cleans input CSV files for compatibility with the generated schema. |
| 3    | `3__run__create_load_validate__DB.ipynb`       | Executes schema creation, loads the preprocessed CSV data into the database, and validates successful insertion. |
| 4    | `4__constraints_and_indexes.ipynb`             | Adds constraints (e.g. PKs, FKs) and indexes to the loaded tables to enforce integrity and improve performance. |

## 🚀 Execution Steps

### Step 1: Generate SQL

This notebook:
- Generates SQL DDL statements to define the database schema.
- Can be driven by predefined metadata, inferred structure, or programmatic logic.

**Outputs:**
- `CREATE TABLE` statements saved to file or passed downstream
- Optionally includes column types, default values, and nullability constraints

**Key Tasks:**
- Define table names, column names, and datatypes
- Ensure compatibility with target DBMS (e.g., PostgreSQL)
- Save SQL files for later execution

**Customization Tips:**
- Adjust data types for performance or compatibility (e.g., `TEXT` vs `VARCHAR`)
- Include optional comments or docstrings in SQL for maintainability

---

### Step 2: Preprocess CSVs

This notebook:
- Loads raw CSV data files.
- Applies data cleaning, formatting, and normalization logic.
- Outputs sanitized CSVs that align with the schema generated in Step 1.

**Inputs:**
- Raw input CSVs (filenames and expected schema should match what Step 1 defines)

**Outputs:**
- Cleaned CSV files for loading in Step 3

**Key Tasks:**
- Handle missing or malformed values
- Standardize date/time and categorical formats
- Ensure consistency in column names and types

---

### Step 3: Create, Load, and Validate Database

This notebook:
- Connects to the database (ensure credentials are configured)
- Executes schema creation SQL from Step 1
- Loads preprocessed CSVs into corresponding tables
- Validates row counts and schema consistency

**Inputs:**
- SQL schema (from Step 1)
- Cleaned CSVs (from Step 2)

**Outputs:**
- Fully loaded database with all tables populated

**Validation Checks:**
- Row counts match CSVs
- No data type or constraint errors during load

---

### Step 4: Apply Constraints and Indexes

This notebook:
- Adds primary keys, foreign keys, and unique constraints after successful data load
- Creates indexes to improve query performance

**Inputs:**
- Loaded tables in the database (Step 3 must be completed successfully)

**Operations:**
- `ALTER TABLE ... ADD CONSTRAINT` for PKs, FKs, and UNIQUE
- `CREATE INDEX` on high-access or join columns

**Best Practices:**
- Apply constraints only after validating data to avoid load failures
- Create indexes based on expected query patterns (e.g. joins, filters)

---
