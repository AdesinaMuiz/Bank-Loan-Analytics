# DAX Measures & Date Table

This documents the DAX calculations used in the Bank Loan Analytics Dashboard. The measures support portfolio KPIs, loan performance analysis, default analysis, recovery analysis, and time-based reporting.

## 1. Date Dimension

A dedicated Date dimension was created to support consistent time-based analysis and filtering across the dashboard.

```DAX
dim_date =
    ADDCOLUMNS(
        CALENDAR(
            MIN(financial_loan[ISSUE_DATE]),
            MAX(financial_loan[ISSUE_DATE])
        ),
        "Year", YEAR([Date]),
        "Month", FORMAT([Date], "mmm"),
        "Monthnum", MONTH([Date]),
        "Weekday", FORMAT([Date], "ddd"),
        "Weeknum", WEEKDAY([Date]),
        "Qtr", "Q" & FORMAT([Date], "Q"),
        "Weektype",
            IF(
                WEEKDAY([Date]) IN {1, 7},
                "Weekend",
                "Weekday"
            )
    )
```
## 2. Portfolio KPIs

Total Loan Applications - Counts the loan records used in the portfolio.
```
Total Loan application =
COUNT(financial_loan[LOAN_ID])
```
## Total Funded

Calculates the total amount funded across the loan portfolio.
```
Total Funded =
SUM(financial_loan[LOAN_AMOUNT])
```
## Total Received
Calculates the total amount received across the loan portfolio.
```
Total Received =
SUM(financial_loan[TOTAL_PAYMENT])
```
## Average Interest Rate

Calculates the average interest rate across the portfolio.
```
Avg Interest =
AVERAGE(financial_loan[INT_RATE])
```
## Average DTI Ratio

Calculates the average debt-to-income ratio across the portfolio.
```
Avg DTI Ratio =
AVERAGE(financial_loan[DTI])
```
## Recovery Ratio
Compares the total amount received with the total amount funded.
```
Recovery Ratio =
DIVIDE(
    [Total Received],
    [Total Funded],
    0
)
```
## 3. Good vs. Bad Loan Analysis
### Good Loan Application
Calculates the number of loan applications classified as Good.
```
 Good Loan Application =
CALCULATE(
    [Total Loan application],
    financial_loan[Good vs Bad Loan] = "Good"
)
```
### Good Loan %
Calculates Good Loan Applications as a percentage of total loan applications.
```
Good Loan % =
DIVIDE(
    [Good Loan Application],
    [Total Loan application],
    0
)
```
### Bad Loan Application
Calculates the number of loan applications classified as Bad.
```
Bad Loan Application =
CALCULATE(
    [Total Loan application],
    financial_loan[Good vs Bad Loan] = "Bad"
)
```
### Bad Loan %
Calculates Bad Loan Applications as a percentage of total loan applications.
```
Bad Loan % =
DIVIDE(
    [Bad Loan Application],
    [Total Loan application],
    0
)
```
## 4. Default Analysis
### Defaulted Loans
Counts unique loan IDs for loans with a Charged Off status.
```
Defaulted Loans =
CALCULATE(
    DISTINCTCOUNT(financial_loan[LOAN_ID]),
    financial_loan[LOAN_STATUS] = "Charged Off"
)
```
### Default Rate

Calculates the proportion of defaulted (Charged Off) loans relative to total loan applications.
```
Default Rate =
DIVIDE(
    [Defaulted Loans],
    [Total Loan application],
    0
)
```
