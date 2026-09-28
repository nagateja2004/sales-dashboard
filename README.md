# Sales & Customer Dashboards

An interactive Tableau project for exploring sales performance and customer purchasing patterns. Use two dashboards to compare a selected year with the previous year, inspect trends, and filter results by product and location.

**Tools:** Tableau, calculated fields, FIXED level-of-detail (LOD) expressions, table calculations, and a packaged Hyper extract.

[Download the Tableau workbook](Sales%20%26%20Customer%20Dashboards.twbx)

## Dashboards

### Sales Dashboard

- Track total sales, profit, and quantity for the selected year alongside prior-year values.
- Compare monthly performance and identify the highest and lowest months.
- Compare sales by product subcategory and inspect profit performance.
- Explore weekly sales and profit trends with above- and below-average indicators.

### Customer Dashboard

- Track distinct customers, sales per customer, and distinct orders.
- Compare monthly customer metrics with the previous year.
- Explore customer distribution by number of orders.
- Review the top 10 customers ranked by selected-year profit, with sales and order counts.

Both dashboards include a year selector, category/subcategory and region/state/city filters, navigation controls, and chart selections that filter other views within the dashboard.

## Data

The supplied CSV files contain retail sales records from **2020 through 2023**. The Orders table has **9,994 line items across 5,009 distinct orders**; a row represents an order line, not an entire order.

| File | Rows | Contents |
| --- | ---: | --- |
| `Orders.csv` | 9,994 | Order and shipment dates, customer/product keys, sales, quantity, discount, and profit |
| `Customers.csv` | 793 | Customer IDs and names |
| `Products.csv` | 1,894 | Product IDs, names, categories, and subcategories |
| `Location.csv` | 632 | Postal codes, cities, states, regions, and country |

The workbook relates Orders to Customers on `Customer ID`, Products on `Product ID`, and Location on `Postal Code`.

The `eu` and `non-eu` folders provide locale-formatted versions of the data. Both use semicolon delimiters. The EU files use decimal commas; the non-EU files use decimal points. Dates use `DD/MM/YYYY`.

## Open and explore

1. Download this repository using **Code > Download ZIP**, then extract it.
2. Open `Sales & Customer Dashboards.twbx` in Tableau Desktop or Tableau Public desktop. The workbook metadata identifies Tableau 2023.2 as its authoring version.
3. Select **Sales Dashboard** or **Customer Dashboard**.
4. Open the filter panel and choose a year. Select 2021, 2022, or 2023 for comparisons with a prior year included in the dataset.
5. Filter by category, subcategory, region, state, or city. Select a chart mark to explore related views; clear the selection to reset the action filter.

The `.twbx` includes the workbook, a Hyper extract, and dashboard icons. To refresh from CSV files, replace the original local file paths in Tableau with one of the supplied dataset folders, check delimiter/date/number settings, and refresh the extract. The stored source connection uses EU-style number formatting.

## Calculations

- **Selected-year measures:** conditional calculations using the `Select Year` parameter and `YEAR([Order Date])`.
- **Previous-year measures:** the same conditions with `Select Year - 1`.
- **Year-over-year comparisons:** selected-year and previous-year aggregates for sales, quantity, customers, orders, and sales per customer.
- **Sales per customer:** selected-year sales divided by distinct selected-year customers.
- **Orders per customer:** a FIXED LOD calculation counting distinct selected-year orders for each selected-year customer.
- **Trend indicators:** `WINDOW_MIN`, `WINDOW_MAX`, and `WINDOW_AVG` calculations.

### Known calculation issue

The existing `% Diff Profit` field divides the profit difference by **current-year profit**. Standard year-over-year growth uses **previous-year profit** as the denominator. Correct that field before interpreting it as profit growth, and handle zero or missing prior-year values. This README documents the workbook as supplied; it does not change its calculations.

## Repository contents

```text
Sales & Customer Dashboards.twbx   Packaged Tableau workbook and extract
 datasets/
   eu/                            CSVs with decimal commas
   non-eu/                        CSVs with decimal points
 images/                          Dashboard navigation and filter icons
 mockup.pdf                       Reference dashboard/container layouts
 project_phases.pdf               Reference project planning material
```

## Project context

This repository includes reference PDFs labelled **Tableau Ultimate Course**. Treat the dashboard as a learning and portfolio project; the dataset metrics describe its scope and do not establish a business outcome.
