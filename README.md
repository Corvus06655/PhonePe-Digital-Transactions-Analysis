# PhonePe Digital Transactions Analysis

An interactive **Power BI** analysis of **300,000 transactions** and **107,658 users** for a UPI-style digital payments platform. The dashboard tracks transaction health, service mix, user demographics, and month-over-month growth.

> **Portfolio focus:** Power Query transformation, star-schema modeling, DAX measures, KPI design, time intelligence, and payment-reliability analysis.

## Business objective

Digital payment teams need visibility into transaction success, failure reasons, service mix, user activity, and growth. This dashboard is designed to help stakeholders monitor platform health and identify areas for operational follow-up.

## Data model and KPI design

The report uses a star-schema design with Date_table, All_Users, and All_Transactions. The transaction table contains 300,000 records, the user table contains 107,658 records, and the date table covers 365 days for time intelligence.

The KPI layer includes total transaction value, total transactions, successful transactions, success rate, total users, month-over-month transaction growth, and month-over-month value growth. The success rate is defined as successful transactions divided by total transactions.

## Dashboard coverage

The report includes KPI cards for transaction value, transaction count, users, and success rate; service and service-type comparisons; monthly and quarterly trends; payment-status analysis; age-group and top-user views; and slicers for time period and payment status.

## Observed findings

The supplied analysis reports an overall success rate of approximately **96%**. Money Transfer is the largest service by transaction volume. Failure categories include Wrong PIN, Server Error, and Insufficient Amount, which can be mapped to operational follow-up questions. Gen X and Millennials are described as the core user groups in the supplied analysis.

These are dashboard observations, not causal conclusions. Operational decisions should be validated against current production data and segmented by time, service, geography, and user cohort.

## Tools and methods

Power BI Desktop · Power Query (M) · DAX · Data modeling · Time intelligence · KPI reporting

## Repository contents

The repository contains Phone.pbix, the Power BI report file, and this documentation. Open the report in Power BI Desktop to review the model relationships, Power Query steps, DAX measures, report pages, slicers, and drill-through behavior.

## How to review locally

Clone the repository and open Phone.pbix in Power BI Desktop. Use the time and payment-status slicers to inspect changes in platform health and service performance.

## Limitations and next steps

A production-ready version would include a visible dashboard export, a data dictionary, refresh instructions, explicit date-coverage metadata, and a reconciliation check between transaction and user tables. A useful next extension would be a failure-rate cohort view by service and month.

---

*Part of Mayank Srivastava's Data Analyst and Business Intelligence portfolio.*
