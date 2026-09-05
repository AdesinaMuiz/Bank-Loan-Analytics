# Bank-Loan-Analytics-Dashboard
An end-to-end loan portfolio analytics project using Excel and Power BI to analyze loan applications, funding, repayment, borrower risk, and default patterns across 38K+ loans.

## Business Problem
A lending institution needs visibility into the health of its loan book: how much has been funded, how much has been recovered, loan status and where default risk is concentrated across grade, term, and geography.
This dashboard answers questions for stakeholders who wants to monitor, need a fast and accurate read on portfolio performance without digging through raw records.

## Tools & Technologies
| Tool                | Purpose                                           |
| ------------------- | ------------------------------------------------- |
| **Microsoft Excel** | Data cleaning, validation and preparation         |
| **Power BI**        | Data modeling, analysis and dashboard development |
| **DAX**             | KPI calculations and portfolio metrics            |

## Dataset
The dataset contains 38,576 loan records and includes fields covering:
- **Loan information:** Loan ID, issue date, loan amount, purpose, term, and loan status
- **Borrower information:** Annual income, employment length, employment title, home ownership, and state
- **Credit risk:** Grade, sub-grade, verification status, interest rate, and debt-to-income (DTI) ratio
- **Payment information:** Installment, total amount received, last payment date, and next payment date
- **Account information:** Member ID and total accounts

## Data Preparation & Approach
The dataset was first reviewed and prepared in **Microsoft Excel**.The column names and field definitions to understand the structure of the dataset, Date fields were verified, missing or blank values as well as duplicate records across relevant fields were checked. It was cleaned and KPI formulas (SUM, AVERAGE,SUMIF,COUNTIF) alongside PivotTables, Power Query were used to transform and validate the dataset for reporting
After validation, the cleaned dataset was imported into **Power BI** for modeling and analysis.

## Data Model

The flat source file was normalized using the simple **star-schema approach**, with the loan dataset serving as the central fact table and supporting dimension tables to support clean filtering and scalable analysis.

### Model Structure

- **Fact Table – Financial Loan:** Contains the individual loan-level records and the core measures used for portfolio analysis, including loan amount, total amount received, interest rate, DTI ratio, and loan status.
- **Grade Dimension:** Contains the unique loan grade and sub-grade combinations used to analyze portfolio risk.
- **Date Dimension:** A dedicated calendar table was created to support time-based analysis of loan applications, including year and month-level reporting.

## Key Performance Indicators

The dashboard uses a set of core KPIs to provide a high-level view of loan portfolio size, funding, repayment, pricing, borrower leverage, and credit risk.

### Portfolio KPIs

- **Total Loan Applications:** Measures the number of unique loan applications in the portfolio.
- **Total Funded Amount:** Measures the total value of loans issued to borrowers.
- **Total Amount Received:** Measures the cumulative amount received from borrowers against the loans.
- **Average Interest Rate:** Shows the average interest rate across the loan portfolio.
- **Average DTI Ratio:** Shows the average debt-to-income ratio of borrowers, providing an indication of overall borrower leverage.
- **Default Rate:** Measures the proportion of loan applications classified as charged off relative to total loan applications.

## Dashboard

The Power BI dashboard was designed to provide both a high-level overview of the loan portfolio and a deeper analysis of portfolio risk and performance.

### Page 1 – Overview

The Overview page provides a summary of the overall loan portfolio through key performance indicators and interactive visuals.

It includes:

- Total loan applications
- Total funded amount
- Total amount received
- Average interest rate
- Average DTI ratio
- Default rate
- Good versus bad loan distribution
- Funded amount versus amount received by loan status
- Loan applications by loan status
- Average interest rate by loan status
- Average DTI ratio by loan status

Users can interact with the dashboard using filters such as **Risk Grade** and **Loan Purpose** to examine different segments of the portfolio.

### Page 2 – Risk Analysis

The Risk Analysis page focuses on identifying patterns in loan performance and borrower risk.

It includes analysis of:

- Loan application trends over time
- Loan applications by state
- Loan applications by loan purpose
- Default rate by loan term
- Default rate across risk grades
- Funding and portfolio performance across risk grades

The interactive design allows users to move from overall portfolio performance into specific risk segments and identify areas requiring closer attention.

## Key Insights
38,576 loan applications, 435.8M funded, 473.1M received — the portfolio has taken in more than it lent out, giving a Recovery Ratio of 108.6%. That's expected and healthy: interest payments on performing loans push total collections above principal, even after accounting for defaults.
**Avg Interest Rate**: 12.0%, Avg DTI: 13.3% — a moderate-risk retail lending book overall, not subprime-heavy.
**Default Rate**: 13.8% — roughly 1 in 7 loans issued ends in charge-off, which becomes the throughline for the rest of the risk analysis.
