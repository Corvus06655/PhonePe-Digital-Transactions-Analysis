# PhonePe Digital Transactions Analysis — Power BI Dashboard

An interactive **Power BI** analysis of **300,000 transactions** and **107,658 users** for a UPI-style digital payments platform. The dashboard tracks transaction health, service mix, user demographics, and month-over-month growth.

> **Portfolio focus:** Power Query transformation, star-schema modeling, DAX measures, KPI design, time intelligence, and payment-reliability analysis.

## Business objective

Digital payment teams need visibility into transaction success, failure reasons, service mix, user activity, and growth. This dashboard is designed to help stakeholders monitor platform health and identify areas for operational follow-up.

## Questions answered

The report addresses the platform’s transaction success rate, the payment outcomes contributing most to failures, the services driving transaction volume and value, month-over-month changes in activity and value, and the user age groups most active on the platform.

## Dashboard preview

![PhonePe dashboard overview](images/dashboard-overview.png)

The image above is a **complete Power BI Desktop screenshot** with populated KPI cards, transaction trend, age-segment contribution, service-value analysis, top-user ranking, weekday-versus-weekend usage, slicers, and the report’s Insights panel. Open `Phone.pbix` in Power BI Desktop to interact with the live DAX values, filters, tooltips, and report pages.

## Data model

The report uses a simple star-schema design:

```text
Date_table 1 ---- * All_Transactions * ---- 1 All_Users
```

| Table | Records | Role |
|---|---:|---|
| `All_Transactions` | 300,000 | Transaction facts, amount, service, status, and date. |
| `All_Users` | 107,658 | User and age-group attributes. |
| `Date_table` | 365 days | Calendar and time-intelligence dimension. |

The model covers Money Transfer, Recharge & Bills, Loans, and Insurance, with 16 service types. Payment outcomes include Successful, Failed, Wrong PIN, Server Error, and Insufficient Amount.

## Tools and techniques

Power BI Desktop · Power Query (M) · DAX · Star-schema modeling · Date-table time intelligence · KPI cards · Slicers · Tooltips · Drill-through analysis

## KPI definitions

| KPI | Definition |
|---|---|
| Total transaction value | Sum of transaction amount. |
| Total transactions | Count of transaction IDs. |
| Successful transactions | Count of transactions with `Payment_Status = Successful`. |
| Success rate | Successful transactions divided by total transactions. |
| Total users | Distinct count of user IDs. |
| MoM transaction growth | Current-month transaction count compared with the prior month. |
| MoM value growth | Current-month transaction value compared with the prior month. |

## DAX examples

```dax
Total Transaction Value = SUM(All_Transactions[Amount])

Total Transactions = COUNT(All_Transactions[Transaction_ID])

Successful Transactions =
    CALCULATE(
        [Total Transactions],
        All_Transactions[Payment_Status] = "Successful"
    )

Success Rate = DIVIDE([Successful Transactions], [Total Transactions])

Total Users = DISTINCTCOUNT(All_Users[User_ID])

Trans Value PM =
    CALCULATE([Total Transaction Value], DATEADD(Date_table[Date], -1, MONTH))

Total Value MoM % =
    DIVIDE([Total Transaction Value] - [Trans Value PM], [Trans Value PM], 0)
```

The PBIX may retain legacy measure names from the original implementation. The conceptual definitions above describe the intended KPI logic shown to reviewers.

## Dashboard coverage

The report includes KPI cards for transaction value, transaction count, users, and success rate; service and service-type comparisons for volume and value; monthly and quarterly transaction trends; payment-status analysis for failure follow-up; age-group and top-user views; weekday-versus-weekend usage; and slicers for time period and payment status. The published screenshot shows the populated report canvas in Power BI Desktop, including the 300K transaction card, 3.47bn total-value card, 108K unique-users card, and 96.00% success-rate card.

Use the Month slicer to compare reporting periods and the Payment Status slicer to isolate successful or failed outcomes. Hover over visuals to inspect tooltips, and use any available drill-through behavior to move from summary metrics to supporting detail.

## Observed findings

The supplied analysis reports an overall success rate of approximately **96%**. Money Transfer is the largest service by transaction volume, with approximately 150,000 transactions or half of the reported activity. Wrong PIN, Server Error, and Insufficient Amount are identified as failure categories for operational follow-up. Gen X and Millennials are described as the core user groups in the supplied analysis.

These findings are dashboard observations, not causal conclusions. Operational decisions should be validated against current production data and segmented by time, service, geography, and user cohort.

## How to review the dashboard

1. Clone the repository and open `Phone.pbix` in **Power BI Desktop**.
2. If Power BI prompts for an external refresh, review the source settings before refreshing; the repository includes the PBIX report but not a separate refresh automation script.
3. Review the model relationships, Power Query steps, DAX measures, and report page layout.
4. Start with the four KPI cards, then use the Month and Payment Status slicers to inspect changes in platform health.
5. Hover over the time, service, age-group, top-user, and weekday/weekend visuals to inspect tooltips.
6. Compare the Insights panel with the filtered KPI values before drawing conclusions.

## Reproducibility and review checklist

A reviewer can reproduce the report review by opening the PBIX, confirming that the Date table is used for time intelligence, checking the relationships between Transactions, Users, and Date, and validating the success-rate and month-over-month measures against the KPI cards.

For a production-ready implementation, add documented source-file locations, a refresh timestamp, a data dictionary, and automated checks for duplicate transaction IDs, missing user IDs, invalid payment statuses, and date-table coverage.

## Repository contents

- `Phone.pbix` — Power BI report file containing the live model, report pages, DAX measures, slicers, and interactions.
- `README.md` — model, KPI, dashboard, and review documentation.
- `images/dashboard-overview.png` — complete Power BI Desktop dashboard screenshot for recruiter review.

## Limitations and next steps

This is a dashboard case study rather than a production monitoring system. A stronger next version would add a visible refresh-status indicator, failure-rate breakdowns by service and geography, confidence intervals for reliability comparisons, an exported dashboard PDF, and a documented data-refresh pipeline. It would also separate descriptive monitoring from root-cause analysis by incorporating event logs or operational incident data.

## Author

**Mayank Srivastava**  
[LinkedIn](https://linkedin.com/in/mayank-srivastava-076020215) · [GitHub](https://github.com/Corvus06655)
