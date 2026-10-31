# RappiPlus | Business Analytics

**Profitability, conversion funnels, cohort retention and checkout experimentation with Python, SQL and Power BI.**

[View the analysis notebook](S12_Proyecto_RappiPlus_Portafolio.ipynb) · [Open the Power BI dashboard](https://app.powerbi.com/view?r=eyJrIjoiODg4OWRmMmQtNzhkMC00ZWQwLWJhMDUtMmViMmY0YzhjNzIzIiwidCI6ImM1ZDFlODIzLWUyYjgtNDZiZi05MmZmLTg0ZjU0MzEzZTBhNSIsImMiOjh9&pageName=da42d321a45002ef00c2)

## Overview

This portfolio case study combines order, product, marketing and user activity data to explore commercial performance and customer behavior. It uses educational datasets supplied through Practicum/TripleTen and does not represent an audit of Rappi's corporate results.

The README is in English; the notebook narrative is in Spanish. Saved notebook outputs are available for inspection without running the analysis.

## Business questions

- What do the recorded revenues, product costs and marketing expenses indicate about profitability?
- What proportion of first-visit users also records each purchase-funnel event?
- How does weekly activity compare across registration cohorts?
- Does a checkout interface change produce a statistically significant difference in conversion?

## Tools and workflow

| Stage | Approach |
| --- | --- |
| Data preparation | Pandas exploration, date conversion, duplicate removal and treatment of order quantities. |
| Financial analysis | Order/catalog joins, revenue, product costs, marketing spend and sales indicators. |
| Conversion funnel | PostgreSQL CTEs, distinct users and cumulative conversion relative to first visits. |
| Cohort retention | Registration-month cohorts and activity in days 7–13, 14–20 and 21–27. |
| A/B experiment | Two-sided Z-test for conversion proportions using statsmodels. |
| Communication | Power BI dashboard and notebook documentation. |

## Selected findings

These figures come from the notebook's saved execution; they were not recalculated for this publication.
- **Purchase-event reach: 77.83%.** Of 7,796 first-visit users, 6,068 also recorded a purchase event. This is cumulative event reach, not proof of an ordered journey.
- **Weekly cohort retention: 40.07%–43.98%.** The observed January–May 2025 cohorts show similar activity levels across the three weekly intervals.
- **Checkout experiment: p = 0.4161.** Control converted 779/4,965 users (15.69%), compared with 820/5,035 (16.29%) in treatment. At alpha = 0.05, the test does not establish a conversion difference; it does not establish equivalence either.
- **Financial calculations:** recorded revenue is 9,622,281.56, product cost is 3,828,869.01 and marketing spend is 2,871,843.53. The resulting profit calculation is 2,921,569.02, subject to the data-quality limitations below. Amounts are in source-data monetary units.

## Interpretation and limitations

The experiment alone does not justify claiming a conversion improvement from the checkout change. Cohort activity provides a baseline for further retention analysis.

Financial results need additional validation: missing product costs after the catalog join can understate costs; missing numeric values and order-amount consistency also require review. Marketing grouped by channel excludes null channels: its saved total is 177,179.10 below total marketing spend. These limitations are retained transparently rather than treating the original calculations as validated financial statements.

The funnel does not enforce event order or session continuity. Retention is limited to the stated weekly intervals. No currency harmonization across countries is assumed. Dashboard definitions should be reconciled with notebook calculations before using them together for financial decisions.

## Repository files

```text
README.md
S12_Proyecto_RappiPlus_Portafolio.ipynb
requirements.txt
.env.example
.gitignore
```

The notebook contains saved tables and outputs. The Power BI report is linked above; a `.pbix` file and a database export are not bundled.

## Data sources

The notebook reads the following CSV files directly from the educational dataset host:

- [Orders](https://practicum-content.s3.amazonaws.com/datasets/rappiplus_orders_raw.csv)
- [Product catalog](https://practicum-content.s3.amazonaws.com/datasets/rappiplus_catalog.csv)
- [Marketing spend](https://practicum-content.s3.amazonaws.com/datasets/rappiplus_marketing_spend.csv)
- [Checkout experiment](https://practicum-content.s3.amazonaws.com/datasets/experiment_checkout_ui.csv)

The SQL sections depend on an authorized PostgreSQL database containing `events`, `users` and `user_activity`. Those tables and access credentials are not distributed here. Remote data availability can change.

## Reading on GitHub

Open the `.ipynb` file to inspect its saved results. GitHub displays the notebook but does not execute its Python or SQL cells. No credentials are needed for reading.

## Running locally

Use Python 3.10 or later. From the repository directory, create and activate a virtual environment, then install the dependencies:

```bash
python -m venv .venv
```

On Windows PowerShell:

```powershell
.\.venv\Scripts\Activate.ps1
```

On macOS/Linux:

```bash
source .venv/bin/activate
```

Then run:

```bash
python -m pip install -r requirements.txt
python -m jupyter lab
```

Open the notebook from this directory.

### CSV analysis only

With internet access, run sections 1–2 for data preparation and financial calculations. For the A/B experiment, run the import cell in section 1 and then section 5. Skip sections 3–4 if you do not have database access. Do not use **Run All** without the SQL configuration.

The export cell writes `orders_clean.csv`, `catalog_clean.csv` and `marketing_clean.csv` into the working directory. These generated files are ignored by Git.

### Full analysis with authorized SQL access

1. Copy `.env.example` to `.env` in the repository directory.
2. Enter your own authorized PostgreSQL connection details.
3. Confirm the three required tables are available with the column names referenced by the notebook queries.
4. Run the notebook in order. The connection uses SSL and reads configuration from `.env` or existing environment variables.

Never commit `.env`. A missing configuration produces a clear message; SQL query cells require valid access to proceed. The credentials from the original training environment have been removed.

## Author

**Andres Martinez Sampayo** · Civil Engineer & Data Analyst

[GitHub](https://github.com/andres-martinez-sampayo) · [LinkedIn](https://www.linkedin.com/in/andres-martinez-sampayo-b4a4101a1/)
