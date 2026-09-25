# Impact of COVID-19 on India's Digital Payments

## 📊 Tableau Dashboard

An interactive Tableau dashboard exploring the impact of the COVID-19 pandemic on India's digital payment ecosystem, with a focus on **UPI transactions, aggregate digital payments, and currency in circulation**.

The dashboard visualizes trends before and after the COVID-19 shock and highlights changes in transaction volumes and transaction sizes over time.

---

## 🎯 Dashboard Objective

The dashboard aims to provide a visual understanding of how India's digital payment system evolved around the COVID-19 period.

It compares:

- UPI transaction activity
- Aggregate digital payment activity
- Average transaction sizes
- Currency in circulation
- Pre-COVID and post-COVID trends

A vertical reference line is used to identify the **COVID-19 structural break**, allowing the trends before and after the pandemic period to be compared visually.

---
## 🛠️ Tools & Data

**Visualization:** Tableau

**Data Sources:**
- National Payments Corporation of India (NPCI)
- Reserve Bank of India (RBI)

**Data Frequency:** Monthly

**Key Measures:**
- UPI transaction volume
- UPI transaction value
- Average UPI transaction size
- Digital payment transaction volume
- Digital payment transaction value
- Average digital payment transaction size
- Currency in circulation

---

## Methodology 

Raw fields (as imported from Excel):

- Month — Monthly time period (primary date dimension)
- UPI Volume (In Mn.) — UPI transaction volume, in millions
- UPI Value (In Cr.) — UPI transaction value, in crores
- UPI Average Transactions — Average UPI transactions
- Currency in circulation — Value of physical currency in circulation
- digital payment volume — Total digital payment transaction volume
- digital payment value — Total digital payment transaction value
- Digital_avg_transaction_size — Average size of a digital transaction
- Growth_rate_upi — Pre-computed period-over-period UPI growth rate
- Growth_rate_currency — Pre-computed period-over-period currency growth rate
- Growth_rate_digital — Pre-computed period-over-period digital payment growth rate
- ln UPI Volume, ln UPI value, ln UPI Average Transactions, ln Currency in Circulation, ln_digital_payment_volume, ln_digital_payment_value — Log-transformed versions of the above, used to compare growth rates on the same scale

CALCULATED FIELDS

- Pre-Post COVID dummy: IF [Month] < 2020-03-01 THEN "Pre-COVID" ELSE "Post-COVID" END — Categorical split point for all comparisons
- Post Dummy: IF [Month] >= 2020-03-01 THEN 1 ELSE 0 END — Numeric (0/1) version of the same split, used inside AVG()/IF logic
- Time Index: DATEDIFF('month', 2016-01-01, [Month]) — Converts date into a linear month-count index (useful for regression/trend analysis)
- Interaction Term: Time Index × Post Dummy — Captures change in trend slope after COVID (classic interrupted time-series / DiD term)
- UPI % Change: AVG(Growth_rate_upi | Post=1) − AVG(Growth_rate_upi | Post=0) — Difference in average UPI growth rate, post vs. pre COVID
- Digital % Change: Same logic, using Growth_rate_digital — Difference in average digital payment growth rate
- % Change in Currency: Same logic, using Growth_rate_currency — Difference in average currency growth rate
- precovid_avg_upi / postcovid_avg_upi: AVG(UPI Volume) filtered by Post Dummy = 0 / 1 — Average UPI volume in each period
- Relative_upi: postcovid_avg_upi / precovid_avg_upi — Scale-up factor: how many times larger UPI volume is post-COVID
- Relative_Dig: Same logic, using digital payment volume — Digital payment scale-up factor
- Relative_curr: Same logic, using currency in circulation — Cash/currency scale-up factor
- Growth_rate_digital_payment: (SUM(digital payment volume) − LOOKUP(prior period)) / LOOKUP(prior period) — Table-calculation growth rate for digital payment volume

- Note: Relative_upi, Relative_Dig, and Relative_curr are the fields driving the three KPI cards.

WORKSHEETS (SHEETS)

- UPI_volume — Line/bar (Automatic) — X: Month — Y: SUM(UPI Volume in Mn.) — Color: Pre-Post COVID dummy — UPI transaction volume trend over time
- Currency Trend — Line/bar (Automatic) — X: Month — Y: SUM(Currency in circulation) — Color: Pre-Post COVID dummy — Physical currency in circulation over time
- digiyal_payment_vol — Line/bar (Automatic) — X: Month — Y: SUM(digital payment volume) — Color: Pre-Post COVID dummy — Digital payment volume trend over time
- Avg UPI transactions — Line/bar (Automatic) — X: Month — Y: SUM(UPI Average Transactions) — Color: none — Average transaction size trend for UPI
- Sheet 14 — Line/bar (Automatic) — X: Month — Y: SUM(Digital_avg_transaction_size) — Color: Pre-Post COVID dummy — Average digital transaction size trend (with - - Month filter + a dropdown filter)
- Comparison — Dual-axis line chart — X: Month — Y: SUM(ln UPI Volume) + SUM(ln Currency in Circulation) — Color: Measure Names — Log-scale comparison of UPI growth vs. currency growth
- dig_comparison — Dual-axis line chart — X: Month — Y: SUM(ln Digital Payment Volume) + SUM(ln Currency in Circulation) — Color: Measure Names — Log-scale comparison of digital payments growth vs. currency growth
- KPI_card1 — Text/scorecard — "Cash Circulation Scale-Up Factor" — shows Relative_curr ("Cash grew 1.8x Post-COVID")
- KPI_card2 — Text/scorecard — "Digital Payment Scale-Up Factor" — shows Relative_Dig ("Digital Payments grew 30x Post-COVID")
- KPI_card3 — Text/scorecard — "UPI Scale-Up Factor" — shows Relative_upi ("UPI grew 22x Post-COVID")

---

## 📈 Dashboard Features

### 1. Currency in Circulation vs. Digital Payments

Visualizes the relationship between currency in circulation and the volume of digital payment transactions using a logarithmic scale.

### 2. Currency in Circulation vs. UPI Transactions

Shows the relationship between cash circulation and UPI transaction volume over time.

### 3. Average UPI Transaction Size

Tracks changes in the average value of UPI transactions from the early years of UPI adoption through the post-COVID period.

### 4. Average Digital Payment Transaction Size

Shows how the average transaction size of digital payments changed over time, including the sharp movement around the COVID-19 period.

### 5. UPI Volume Over Time

Displays UPI transaction volume with separate pre-COVID and post-COVID trend lines.

### 6. Digital Payment Volume Over Time

Shows the evolution of aggregate digital payment transaction volume and highlights the change around the COVID-19 period.

### 7. Currency in Circulation Over Time

Tracks the movement of currency in circulation, including the effects visible around major economic events such as demonetization and COVID-19.

---

## 🔎 Key Visual Insights

The dashboard highlights several important patterns:

- Cash in circulation grew ~1.8x post-COVID
- Digital payments grew ~30x post-COVID
- UPI transactions grew ~22x post-COVID
- UPI transaction volume shows strong growth over the study period.
- Aggregate digital payment volume shows a pronounced increase around the COVID-19 period.
- Average transaction sizes display different patterns for UPI and aggregate digital payments.
- Currency in circulation continues to increase alongside digital payment adoption.
- The trends suggest that increasing digital payment usage did not simply correspond to the disappearance of cash.
- The dashboard allows pre-COVID and post-COVID trajectories to be compared through trend lines and the COVID-19 reference point.
  
**Refer to doc file for detailed results**
