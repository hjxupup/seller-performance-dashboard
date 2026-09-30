# Seller Performance Dashboard

An interactive analytics dashboard that brings seller revenue, delivery performance, and account health into one operational workspace.

**[Open the Live Demo →](https://jiaxin-sellerops.hjxupup.chatgpt.site/)**

**Original application:** Python · Dash · Pandas · NumPy · Plotly · SQL/JDBC  
**Public portfolio demo:** HTML · CSS · JavaScript · Synthetic data

## Project Overview

Seller performance is more than a revenue number. A seller can generate strong sales while experiencing delivery delays, missing tracking events, or increasing item-not-received cases. Understanding those signals together requires consistent metrics and the ability to move between account, seller, entity, and group views.

This project connects account information, transaction performance, and assessment results through an interactive dashboard. Users can filter the reporting scope, compare time periods, investigate delivery metrics, and identify individual accounts that explain a broader trend.

The original application uses a Python data pipeline and Dash interface. The public demo reconstructs the main interactions with fictional data, so visitors can explore the product directly in their browser.

## The Problem

The dashboard addresses three practical challenges in seller operations:

- **Fragmented reporting:** Account attributes, business metrics, and assessment results come from different datasets. Reviewing them together requires a shared reporting context.
- **Different levels of analysis:** Teams need both portfolio-level summaries and account-level detail. The same seller may be associated with multiple accounts, making consistent aggregation important.
- **Recurring data processing:** Large exports, repeated filtering, and daily updates create engineering work beyond drawing charts. The application needs a repeatable path from source data to usable reports.

The goal is to make these questions easier to investigate: Which accounts contribute to a revenue change? Which delivery corridor needs attention? Does a seller-level summary hide a problem in one account?

## Key Features

### Account Hierarchy and Drill-Down

Explore four reporting levels: **Group, Entity/UID, Seller, and Account**. Scope filters connect high-level summaries with the underlying accounts. In the public demo, searchable account tables and clickable account names provide a direct path into an individual account's performance.

### Monthly and Year-to-Date Reporting

Switch between a selected month and cumulative year-to-date results. The public demo aligns prior-year comparisons to the same month or month range, and keeps the selected scope consistent across metrics, charts, and tables.

### Business and Delivery Metrics

Explore fourteen core chart metrics, including:

- Gross merchandise value and transaction volume.
- Item-not-received counts and rates.
- Acceptance and delivery scan on-time rates.
- Acceptance and delivery scan filling rates.
- Average handling time and average delivery days.
- ILM counts, ILM rates, implied ILM rates, and CWH transaction share.

The interface combines commercial performance with delivery signals, allowing users to investigate growth and service quality in the same view.

### Assessment and Reporting Views

The original application includes seller/account assessment results alongside performance reporting. The demo uses clearly labeled illustrative thresholds to show how an assessment view can highlight signals for further review. It also adds CSV export for the selected reporting window and scope.

## Technology Stack

| Technology | Role in the project |
| --- | --- |
| Python | Data-processing orchestration, application logic, and refresh workflow in the original application. |
| SQL and JDBC | Retrieving source datasets through a database export workflow. |
| Pandas and NumPy | Data cleaning, type normalization, grouping, numerical operations, and metric calculation. |
| Dash | Building the original interactive interface and connecting filters to tables and charts through callbacks. |
| Dash Bootstrap Components | Organizing the original interface into filter panels, cards, and reporting sections. |
| Plotly Express | Rendering interactive metric trends in the original application. |
| HTML, CSS, and JavaScript | Implementing the responsive public demo, browser-based aggregation, SVG charts, and CSV downloads. |

## Engineering Design

### Aggregate Counts Before Calculating Rates

Percentage metrics are calculated from summed numerators and denominators, rather than averaging account-level percentages.

For example, if one account has 2 item-not-received cases across 100 transactions and another has 9 cases across 900 transactions, the combined rate is:

`INR rate = (2 + 9) / (100 + 900) = 1.1%`

This gives each account the appropriate weight and preserves the metric's meaning as users move between reporting levels.

### Reuse Account Filtering

The original Dash application uses a lock-protected, process-local account-filter cache. Table and chart callbacks can reuse the filtered DataFrame for the same scope, avoiding a second scan of the full dataset for that selection.

### Load Large Files in Chunks

The original application selects the required performance columns and reads CSV data in chunks of 400,000 rows. This limits individual read allocations. The resulting chunks are concatenated into a DataFrame, so the complete dataset still needs to fit in memory.

### Coordinate Snapshots and Refreshes

The dashboard selects a dataset suffix for which all three required CSV snapshots are available. The export script includes partition checkpoints, retry paths, and temporary-file replacement. A scheduled daily workflow refreshes the CSV data and restarts the original application.

Together, these components connect data acquisition, metric processing, and interactive reporting into a repeatable workflow.

## Why This Project Matters

**For operational users**, the dashboard provides a common view of revenue and delivery quality. A trend can be investigated by corridor and account, helping users identify where further analysis is needed.

**For reporting quality**, shared aggregation rules make results easier to interpret across different account levels and reporting windows. Weighted rates address a concrete source of misleading summaries.

**For software engineering**, the project demonstrates how business requirements translate into data schemas, callback behavior, metric definitions, and refresh workflows. It combines data engineering and interactive application development within one system.

## Explore the Demo

1. Open **Overview** to see revenue, transactions, and delivery signals.
2. Change **View by** to Seller and select a seller scope.
3. Filter a corridor and switch between Monthly and Year to date.
4. Open **Performance** to explore a metric and its calculation.
5. Open **Accounts** and select an account to drill down.
6. Export the current report or open **Project story** to read about the original architecture.

## Original Application and Public Demo

| Aspect | Original application | Public demo |
| --- | --- | --- |
| Implementation | Python, Dash, Pandas, and Plotly. | HTML, CSS, and JavaScript. |
| Data | SQL/JDBC exports and coordinated CSV snapshots. | Deterministic synthetic records. |
| Refresh | Scheduled export and application restart. | Fixed demonstration dataset. |
| Assessment | Source assessment results. | Illustrative thresholds created for the demo. |
| Access | Requires its configured data environment. | Public browser-based demonstration. |

All demo names, IDs, transaction values, and assessment targets are fictional. The demo contains 18 accounts, 9 sellers, 6 entities, 3 groups, and four delivery corridors. Internal database connections, credentials, company data, and original assessment policies are excluded from the public materials.

**Built by Jiaxin Hu**
