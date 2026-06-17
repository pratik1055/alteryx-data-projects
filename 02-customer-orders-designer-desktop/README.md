# Customer Orders Analysis — Alteryx Designer Desktop

A multi-source data preparation and reporting project for a fictitious retail company. Reads five related tables from three different file formats, transforms each to spec, joins them, and produces sales reporting.

Built in Alteryx Designer (Desktop).

---

## The Data

| Table | Source File | Format | Key Columns |
|---|---|---|---|
| Orders | `orders.yxdb` | Alteryx native | ORDER_ID, ORDER_DATE, CUSTOMER_ID, ORDER_STATUS, STORE_ID |
| Order Items | `order_items.yxdb` | Alteryx native | ORDER_ID, PRODUCT_ID, UNIT_PRICE, QUANTITY |
| Products | `products.csv` | Tab-delimited | PRODUCT_ID, PRODUCT_NAME, UNIT_PRICE |
| Stores | `stores_and_customer_data.xlsx` ("stores" sheet) | Excel | STORE_ID, STORE_NAME |
| Customers | `stores_and_customer_data.xlsx` ("customers" sheet) | Excel | CUSTOMER_ID, FIRST_NAME, LAST_NAME |

---

## Part 1 — Transformations

Each table was read in and shaped to match the required target layout, with all ID columns cast to **integer**:

- **Customers** — combined FIRST_NAME + LAST_NAME into a single `FULL_NAME` (with `Trim()` to remove a trailing-space data-quality issue in the source).
- **Products** — product names contained the colour in parentheses (e.g. `Women's Socks (Grey)`). Used a single **RegEx Parse** to simultaneously split the malformed delimiter and extract the colour into `PRODUCT_DESCRIPTION`, leaving a clean `PRODUCT_NAME`.
- **Orders** — converted `ORDER_DATE` from `DD-MON-YY` text (e.g. `06-JAN-22`) to proper ISO date format `yyyy-MM-dd` using the DateTime tool.
- **Order Items** — added a `Line_Total` calculated field (`UNIT_PRICE * QUANTITY`).
- **Stores** — trimmed to the required columns only.

---

## Part 2 — Analysis & Reporting

Joined the branches (order_items → orders → products) and filtered to **March 2022, completed orders only**.

- **Total Revenue by Store (March 2022)** — grouped revenue by store and rendered a bar chart to **PNG** (see `outputs/`).

*(Further reporting — top-selling products and sales-by-colour PDF — is part of the same workflow.)*

---

## SQL Equivalent (Part 2 — top orders)

```sql
SELECT order_id, SUM(unit_price * quantity) AS total_order_amount
FROM order_items
GROUP BY order_id
ORDER BY total_order_amount DESC
FETCH FIRST 10 ROWS ONLY;
```

The store-revenue chart is equivalent to:

```sql
SELECT store_id, SUM(unit_price * quantity) AS revenue
FROM order_items
  JOIN orders USING (order_id)
WHERE order_status = 'COMPLETE'
  AND order_date BETWEEN '2022-03-01' AND '2022-03-31'
GROUP BY store_id;
```

---

## Files

- `data/` — the five raw source files
- `workflow/customer_orders.yxmd` — the Alteryx workflow (open in Designer)
- `outputs/` — generated chart (PNG)
- `screenshots/` — the workflow canvas

---

## Skills Demonstrated

Multi-format ingestion · RegEx parsing · date conversion · string concatenation · type casting · multi-table joins · calculated fields · filtering · aggregation · charting & rendering to file.
