# Alteryx Data Analytics Projects

Two end-to-end data preparation and analysis projects built in **Alteryx**, covering ETL, data cleansing, joins, aggregation, and reporting. Built while completing an Alteryx course on Udemy, using both the cloud and desktop versions of the platform.

**Author:** Pratik Deshmukh
**Tools:** Alteryx Designer (Desktop), Alteryx Designer Cloud (formerly Trifacta)

---

## Projects

### 1. MovieLens Genre Analysis — *Alteryx Designer Cloud*
An ETL pipeline on the MovieLens dataset (~100K ratings, 9.7K movies) that parses pipe-delimited genres, reshapes them to genre level, joins ratings to movies, and computes **average rating and rating volume per genre**.

→ [View project](./01-movielens-designer-cloud)

**Key skills:** ETL, text splitting, unpivot (transpose), conditional logic, filtering, joins, group-by aggregation, CSV output.

### 2. Customer Orders Analysis — *Alteryx Designer Desktop*
A multi-source data project for a fictitious retail company. Reads five related tables across three file formats (.yxdb, tab-delimited CSV, multi-sheet Excel), performs the required transformations, joins them together, and produces sales reporting.

→ [View project](./02-customer-orders-designer-desktop)

**Key skills:** multi-format ingestion, RegEx parsing, date conversion, field concatenation, type casting, multi-table joins, calculated fields, aggregation & ranking, charting and rendering output (PNG).

---

## What These Projects Demonstrate

| Capability | Project 1 | Project 2 |
|---|---|---|
| Reading multiple file formats | | ✓ |
| String parsing / RegEx | ✓ | ✓ |
| Date handling | | ✓ |
| Joins across tables | ✓ | ✓ |
| Aggregation & grouping | ✓ | ✓ |
| Conditional / calculated columns | ✓ | ✓ |
| Reporting output (charts/files) | ✓ | ✓ |

Each step maps directly onto equivalent SQL operations (joins, `GROUP BY`, `CASE WHEN`, aggregate functions), which is documented in the individual project READMEs.

---

## Certifications

- Alteryx course completion — see [`certifications/`](./certifications)

---

## A Note on Process

These projects were built independently as hands-on practice. I used AI assistance for guidance and troubleshooting along the way, but designed, built, and verified every workflow myself.

---

## Contact

- **GitHub:** [github.com/pratik1055](https://github.com/YOUR_USERNAME)
- **LinkedIn:** [www.linkedin.com/in/pratikdeshmukhuk](https://linkedin.com/in/YOUR_PROFILE)
