# For-Ada-Analytics-Case-Dashboard
There are some thoughts about doing the Ada Analytics company's case:

## About the Project
This project was completed in collaboration with Ada Analytics, using the Riipen platform. Ada Analytics is a rapidly growing consulting firm facing challenges in scaling due to data being scattered across multiple spreadsheets. This resulted in information silos, with decisions relying on historical experience rather than empirical data.

The goal of this project was to help the company transition from manual tracking to an automated, evidence-based data strategy. We developed a comprehensive Power BI dashboard, providing a scalable decision support tool for account managers and executives around three core business pillars: “revenue, workload, and collection rate”.

## My Role
I was responsible for the dashboard design. My main contributions included:
Transforming raw, standardized datasets into meaningful business metrics;
Designing and developing core analytical models and DAX formulas;
Designing and optimizing the dashboard;
Identifying and analyzing issues in the charts, such as efficiency gaps and financial risks, and providing strategic and actionable recommendations to stakeholders, such as senior management at Ada Analytics.

## Key Skills and Tools
Power BI and Data Visualization: Built an interactive dashboard for daily use by account managers. Transform technological discoveries into customer-centric strategic objectives (e.g., transforming data anomalies into cash flow risk alerts).

DAX (Data Analysis Expressions):Designed custom business logic to translate raw data into actionable metrics. Below are key examples of the measures and calculated columns built for this project:
1. Payment Reliability (Measure) to evaluates the proportion of collected revenue against the total invoiced amount
Payment Reliability = 
DIVIDE(
    SUM('Cleaned_Data'[Total Revenue]), 
    SUM('Cleaned_Data'[Invoice Amount]), 
    0
)

2. Forecast Revenue (Measure & What-If Parameter) that allows users to dynamically model future revenue based on adjustable pricing scenarios.
Price Adj = GENERATESERIES(-0.2, 1, 0.01)

Price Adj Value = SELECTEDVALUE('Price Adj'[Price Adj], 0)

Forecast Revenue = 
VAR BaseRevenue = SUM('Cleaned_Data'[Total Revenue])
VAR SelectedPercent = [Price Adj Value]
RETURN
BaseRevenue * (1 + SelectedPercent)

3. Days Overdue (Calculated Column) that tracks aging invoices to identify cash flow risks.
Days Overdue = DATEDIFF('Cleaned_Data'[Invoice Date], TODAY(), DAY)

4. Attendance Status (Calculated Column) that flags potential hidden opportunity costs and disruptive client behavior.*
Attendance Status = 
IF(
    'Cleaned_Data'[Total Hours] <= 0.1, 
    "No-show / Cancelled", 
    "Showed up"
)

## Project Highlights
1. Automated Decision Support: Replaced fragmented spreadsheet tracking with a unified analytics dashboard that provides real-time visualization of revenue, workload, and collection rates.
2. Developed "Payment Reliability" Metric: Designed a custom visualization alert system to transform complex billing data into metrics that account managers can immediately identify financial anomalies.
3. Identified Efficiency Gap (Client A): Discovered significant hidden opportunity costs. Analysis showed that despite the client investing substantial resources (over 44 hours of consultation service), their hourly rates were below average, and their no-show rate was extremely high, severely impacting their business.
4. Reduce Cash Flow Risk (Client D): Discovered an unusual 210% payment delay. Although this client had the highest on-paper revenue ($9,000), our analysis revealed that over 80% of that revenue was tied up in bad debts (overdue by more than 30 days), requiring immediate strategic intervention.

## How to Navigate the Codebase
Dashboard: Contains `.pbix` files and partial screenshots of the final dashboard.
Scripts: Documentation of the core DAX formulas and data transformation steps used in the project.
Presentations: The final slide presentation highlighting our data story and actionable recommendations.
Documents: Data dictionary and business requirements documents mapping our metrics to organizational goals.

## Privacy and Client Notice
Confidentiality: *To comply with non-disclosure agreements (NDAs) and protect client privacy, all proprietary data in this repository has been rigorously anonymized and downsampled. Client names (e.g., Client A, Client D) and specific financial data have been replaced with synthetic data to preserve the statistical relationships and outliers used to demonstrate analytical concepts.
