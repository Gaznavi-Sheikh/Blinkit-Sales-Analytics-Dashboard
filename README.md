# Blinkit Sales Analytics Dashboard

An interactive sales dashboard built entirely in **Microsoft Excel** from a 8,523-row Blinkit grocery sales dataset. The workbook uses PivotTables, PivotCharts and slicers to summarise sales by item type, fat content, outlet size, outlet location, outlet type and outlet establishment year.

> Beginner-friendly Data Analytics portfolio project.

## Table of Contents

- [Objectives](#objectives)
- [Business Questions](#business-questions)
- [Dataset](#dataset)
- [Tools and Excel Techniques](#tools-and-excel-techniques)
- [Dashboard Preview](#dashboard-preview)
- [KPIs](#kpis)
- [Key Findings](#key-findings)
- [Project Structure](#project-structure)
- [How to Use the Workbook](#how-to-use-the-workbook)
- [Limitations](#limitations)
- [Future Enhancements](#future-enhancements)
- [Suggested GitHub Topics](#suggested-github-topics)

## Objectives

- Summarise overall sales performance with a small set of KPIs.
- Compare sales across product categories and outlet characteristics.
- Let a viewer filter every chart interactively with slicers.

## Business Questions

- How much did Blinkit sell in total, and what is the average sale per item?
- Which item types contribute the most sales?
- How do sales differ by outlet size, location tier and outlet type?
- Do Low Fat and Regular items sell differently?
- How do sales vary by outlet establishment year?

## Dataset

| Property | Value |
|---|---|
| File | [data/blinkit_sales_dataset.xlsx](data/blinkit_sales_dataset.xlsx) |
| Sheet / table | `BlinkIT Grocery Data` (Excel table) |
| Rows | 8,523 records |
| Columns | 12 |
| Outlets / items | 10 distinct outlets, 1,559 distinct item identifiers |
| Source | Not documented in this repository (see [Limitations](#limitations)) |

**Columns:** Item Fat Content, Item Identifier, Item Type, Outlet Establishment Year, Outlet Identifier, Outlet Location Type, Outlet Size, Outlet Type, Item Visibility, Item Weight, Sales, Rating.

The original dataset file is kept unchanged. The dashboard workbook holds its own copy of the data with two differences (verified by comparing both files):

- An added **`Sr No`** column (1 to 8,523), used for counting items.
- **Item Fat Content** labels standardised: `LF` was changed to `Low Fat` and `reg` to `Regular`. The raw data contains `Low Fat` (5,089), `Regular` (2,889), `LF` (316), `reg` (117) and `low fat` (112); the workbook sheet contains `Low Fat` (5,405), `Regular` (3,006) and `low fat` (112). The 112 lowercase `low fat` cells were left as they are, but PivotTables ignore letter case, so the dashboard still shows only two categories.

Item Weight has 1,463 blank values in both files.

## Tools and Excel Techniques

All of the following were verified by inspecting the workbook:

- **Excel table** (`Table1`) as the data source for the PivotTables
- **10 PivotTables** on `Dashboard Analysis` (sums, averages and counts)
- **PivotCharts**: doughnut, bar, area and funnel charts
- **3 slicers**: Outlet Size, Item Type, Outlet Location Type, connected to the PivotTables
- **Dashboard layout** built from shapes, text boxes, icons and hyperlinks to `Dashboard Analysis` and the data sheet

No macros, external data connections or worksheet formulas beyond simple cell references (`=A5`, `=A85`, etc.) were found.

## Dashboard Preview

<!-- TODO: Open the workbook in Excel, take a screenshot of the Dashboard sheet, save it as images/dashboard-preview.png, then uncomment the line below. -->
<!-- ![Blinkit Sales Dashboard](images/dashboard-preview.png) -->

*Screenshot pending: the repository does not yet contain a full dashboard screenshot. The files in `images/` are the 512 x 512 icons used on the dashboard.*

## KPIs

Verified from the `Dashboard Analysis` PivotTable ("KPI's Requirements") and recomputed independently from the dataset.

| KPI | Definition | Value |
|---|---|---|
| Total Sales | Sum of `Sales` | 1,201,681.49 (shown as **$1.20M** on the dashboard) |
| Average Sales | Average of `Sales` per item record | 140.99 (shown as **$141**) |
| Number of Items | Count of records (`Sr No`) | 8,523 |
| Average Rating | Average of `Rating` | 3.97 (shown as **4.0**) |

The dataset has no currency field; the `$` symbol is only a label on the dashboard.

## Key Findings

All figures are PivotTable totals from `Dashboard Analysis`; percentages are of total sales (rounded).

| Dimension | Result |
|---|---|
| Fat content | Low Fat 776,320 (64.6%) vs Regular 425,362 (35.4%) |
| Top item types | Fruits and Vegetables 178,124 (14.8%), Snack Foods 175,434 (14.6%), Household 135,977 (11.3%) |
| Lowest item type | Seafood 9,078 (0.8%) |
| Outlet size | Medium 507,896 (42.3%), Small 444,794 (37.0%), High 248,992 (20.7%) |
| Outlet location | Tier 3 472,133 (39.3%), Tier 2 393,151 (32.7%), Tier 1 336,398 (28.0%) |
| Outlet type | Supermarket Type1 787,550 (65.5%); Grocery Store 151,939 (12.6%); Supermarket Type2 131,478 (10.9%); Supermarket Type3 130,715 (10.9%) |
| Outlet establishment year | Highest: 2018 (204,522, 17.0%); lowest: 2011 (78,132, 6.5%) |

Observations that follow directly from the numbers:

- Low Fat items account for almost two thirds of sales, but they also have more records (5,517 vs 3,006), and average sales per record are similar (about 140.7 vs 141.5).
- Average sales per record are nearly identical across outlet types (139.8 to 141.7), so Supermarket Type1's lead in total sales comes from having many more records (5,577 of 8,523), not from higher sales per item.
- The data contains no outlets established in 2013, 2019 or 2021.

These are descriptive observations. The dataset does not show *why* the differences occur.

## Project Structure

```
Blinkit-Sales-Analytics-Dashboard/
├── dashboard/
│   └── blinkit_sales_analysis_dashboard.xlsx   # Working dashboard (Dashboard, Dashboard Analysis, BlinkIT Grocery Data)
├── data/
│   └── blinkit_sales_dataset.xlsx              # Original dataset (unchanged)
├── images/                                     # Icons used on the dashboard (512 x 512 PNG)
└── README.md
```

**Workbook sheets**

| Sheet | Purpose (verified) |
|---|---|
| `Dashboard` | Final dashboard: KPI cards, charts and a filter panel with slicers |
| `Dashboard Analysis` | Working sheet holding the 10 PivotTables that feed the charts, plus the KPI table. Cells `D84:E87` hold a small linked table used by the funnel chart |
| `BlinkIT Grocery Data` | The data table (A1:M8524) |

## How to Use the Workbook

1. Download [dashboard/blinkit_sales_analysis_dashboard.xlsx](dashboard/blinkit_sales_analysis_dashboard.xlsx) (use **Download raw file** on GitHub, or clone the repository).
2. Open it in **Microsoft Excel 2016 or later** (desktop). The funnel chart and slicers are not supported in older versions, and LibreOffice or Excel Online may not display them correctly.
3. Go to the `Dashboard` sheet and use the **Filter Panel** slicers (Outlet Size, Item Type, Outlet Location) to filter the charts.
4. Open `Dashboard Analysis` to inspect the PivotTables, or `BlinkIT Grocery Data` to view the records.

```bash
git clone https://github.com/Gaznavi-Sheikh/Blinkit-Sales-Analytics-Dashboard.git
```

## Limitations

- The data source and licence of the dataset are not documented in the repository, and the data's time period is not stated.
- The only time dimension is Outlet Establishment Year; there are no transaction dates, so trends over time cannot be analysed.
- The dataset contains no currency, quantity or profit fields; `Sales` is analysed as given.
- Item Weight has 1,463 blank values (not used in the dashboard).
- The KPI table and some labels in `Dashboard Analysis`/`Dashboard` are PivotTable output and static text, so they update only when the PivotTables are refreshed.
- No screenshot of the full dashboard is included yet.

## Future Enhancements

Planned only; none of these are implemented:

- Add a dashboard screenshot to `images/`.
- Document the dataset's source and licence.
- Add a short data-cleaning log (fat content standardisation, blank weights).
- Add an insights or recommendations section for business stakeholders.

## Suggested GitHub Topics

`excel` `data-analytics` `dashboard` `pivot-table` `pivot-chart` `slicers` `sales-analysis` `data-visualization` `blinkit` `portfolio-project`
