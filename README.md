# AdventureWorks Sales Analysis: SQL × Python

## Project Overview

This project demonstrates how SQL and Python can be combined in a practical data-analysis workflow.

Sales data was retrieved from the Microsoft AdventureWorks database using SQL Server and `pyodbc`. Python libraries such as pandas, NumPy, Matplotlib, and Seaborn were then used to validate, transform, analyze, and visualize the extracted data.

The project was completed as an open-ended course assignment focused on practicing Python–SQL integration.

## Objectives

The analysis explores:

1. Total order value over time
2. Product and category performance
3. Customer contribution and repeat purchasing
4. Order quantities and their relationship with order value

The project addresses questions such as:

- How does total order value change over time?
- Which products generate the greatest recorded value?
- How do product categories differ in catalogue size and value contribution?
- How concentrated is purchasing value across customers?
- What percentage of customers place multiple orders?
- How does the number of units in an order relate to its total value?

## Data Source

The analysis uses the Microsoft AdventureWorks sample database.

The following tables were queried:

- `Sales.SalesOrderHeader`
- `Sales.SalesOrderDetail`
- `Production.Product`
- `Production.ProductSubcategory`
- `Production.ProductCategory`

These tables contain information about orders, customers, order lines, products, subcategories, and categories.

## Workflow

### 1. Data extraction with SQL

Python was connected to Microsoft SQL Server using `pyodbc`.

SQL queries were used to:

- Retrieve order-header records
- Retrieve individual order lines
- Retrieve product information
- Join products with their corresponding subcategories and categories

### 2. Data validation

After loading the query results into pandas DataFrames, the data was inspected by:

- Previewing records
- Reviewing data types
- Checking missing values
- Calculating descriptive statistics
- Confirming the number of orders, products, and customers

### 3. Data preparation

Several analytical variables were created:

- Total quantity per order
- Total recorded value per product
- Monthly total order value
- Total order value per customer
- Repeat-purchase indicators

### 4. Exploratory analysis

The prepared data was analyzed and visualized at four levels:

- Time
- Product and category
- Customer
- Order

Log transformations and hexbin visualization were used where highly skewed distributions and overlapping observations made standard plots difficult to interpret.

## Key Results

- The data contains **31,465 orders**.
- The product catalogue contains **504 products**.
- Only **266 products**, or approximately **52.8% of the catalogue**, appeared in the recorded order details.
- The data contains **19,119 unique customers**.
- Approximately **39% of customers** placed at least two recorded orders.
- Product and customer value distributions are highly skewed.
- Product categories differ in both catalogue representation and total recorded value.
- Orders containing more units generally tend to have higher total values, although product-price differences also affect this relationship.

## Metric Clarification

The time and customer analyses use `TotalDue`.

In AdventureWorks:

```text
TotalDue = SubTotal + TaxAmt + Freight
```

Therefore, this metric is described as **total order value** or **total amount due**, rather than pure product sales.

Product-level and category-level value calculations use `LineTotal` from individual order lines.

## Technologies Used

- Python
- SQL
- Microsoft SQL Server
- AdventureWorks
- Jupyter Notebook
- pyodbc
- pandas
- NumPy
- Matplotlib
- Seaborn

## Requirements

To run the notebook, the following are required:

- Python 3
- Jupyter Notebook or JupyterLab
- Microsoft SQL Server
- An installed AdventureWorks database
- Microsoft ODBC Driver 17 for SQL Server
- The required Python packages

Install the Python dependencies with:

```bash
python -m pip install pandas numpy matplotlib seaborn pyodbc jupyter
```

## How to Run

1. Install Microsoft SQL Server and restore the AdventureWorks database.

2. Confirm that the database name and connection settings match those used in the notebook.

3. Update the connection string if necessary:

```python
conn = pyodbc.connect(
    "DRIVER={ODBC Driver 17 for SQL Server};"
    "SERVER=localhost;"
    "DATABASE=AdventureWorks2025;"
    "Trusted_Connection=yes;"
)
```

4. Install the required Python packages.

5. Open the notebook in Jupyter Notebook, JupyterLab, or Visual Studio Code.

6. Run the cells in order.

The SQL Server service must be running while the notebook retrieves data.

## Limitations

- This is an exploratory course assignment rather than a complete business audit.
- `TotalDue` includes tax and freight and should not be interpreted as product revenue alone.
- The analysis does not establish why certain products did not appear in orders.
- Apparent patterns in customer-value distributions do not establish distinct customer segments.
- Relationships shown in the analysis are observational and should not be interpreted as causal.
- Additional customer, product-availability, and business-context information would be required for more detailed conclusions.

## Conclusion

This project demonstrates the complementary roles of SQL and Python in data analysis.

SQL provided structured access to related business tables, while Python provided the flexibility needed to validate the extracted data, create analytical metrics, explore distributions, and communicate results through visualizations.