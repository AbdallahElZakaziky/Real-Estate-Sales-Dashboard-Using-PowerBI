# Real Estate Sales Dashboard Using Power BI

**Primary Tool: Microsoft Power BI**

---

## Dashboard Preview

![Dashboard](Dashboard.png)

---

## Project Purpose

This project analyzes real estate sales performance across the MENA region — covering 3,000 transactions worth EGP 3.09B across 40 agents, 500 properties, and 8 cities (Cairo, Giza, Alexandria, Dubai, Sharjah, Riyadh, Jeddah, Amman) between 2022 and 2024. The dashboard is structured around a sales overview view that tracks revenue, commissions, units sold, and client volume — segmented by agent, property condition, city, transaction type, and time period to support brokerage management decisions on agent performance, market prioritization, and product mix.

---

## Data Model

The project follows a **Star Schema** with one central fact table and five dimension tables.

```
FACT_Transactions (3,000 rows — 2022 to 2024)
├── DIM_Date              (1,096 rows — daily granularity, full 3-year calendar)
├── DIM_Agent             (40 rows  — name, branch, specialization, experience, rating)
├── DIM_Property          (500 rows — type, city, district, area, condition, amenities)
├── DIM_Client            (800 rows — type, nationality, age group, lead source)
└── DIM_TransactionType   (4 rows  — Sale, Re-Sale, Rental, Lease)
```

### Fact Table — Key Columns

| Column            | Description                                          |
| ----------------- | ---------------------------------------------------- |
| TransactionKey    | Unique transaction identifier                        |
| ListingPriceEGP   | Original listing price in Egyptian Pounds            |
| FinalPriceEGP     | Final sale price in Egyptian Pounds                  |
| CommissionRate    | Commission percentage applied                        |
| CommissionEGP     | Commission earned on the transaction                 |
| DaysOnMarket      | Number of days from listing to deal closure          |
| Status            | Completed, Pending, Cancelled, Under Review          |
| PaymentMethod     | Cash, Mortgage, Bank Transfer, Installment           |
| NegotiationDisc   | Negotiated discount from listing price               |

### Dimension Breakdowns

**Properties (500):** Eight types — Townhouse (416), Warehouse (410), Apartment (407), Penthouse (401), Studio (359), Villa (350), Retail Space (331), Office (326). Four conditions — Excellent, New, Good, Needs Renovation.

**Agents (40):** Five specializations — Residential, Rental, Industrial, Luxury, Commercial. Experience and rating tracked per agent.

**Clients (800):** Five types — Individual (largest segment), Investor, Corporate, Expat, Government. Lead sources span Social Media, Walk-in, Property Portal, Website, Exhibition, Phone, and Referral.

**Geography (8 cities):** Cairo, Giza, Alexandria (Egypt), Dubai, Sharjah (UAE), Riyadh, Jeddah (KSA), Amman (Jordan).

---

## Key Performance Indicators

| Metric                | Value           |
| --------------------- | --------------- |
| Total Revenue         | EGP 3.09B       |
| Total Commissions     | EGP 113M        |
| Total Transactions    | 3,000           |
| Completed Deals       | 2,074 (69.1%)   |
| Average Deal Size     | EGP 1.03M       |
| Average Days on Market| 65.6            |
| Active Agents         | 40              |
| Active Clients        | 800             |
| Date Range            | 2022 – 2024     |

---

## Dashboard Page — Sales Overview

**Visuals:**

- KPI Cards — Total Units Sold, Total Revenue, Total Commissions Paid, Number of Clients
- Clustered Column Chart — Revenue and transaction count by Agent Name
- Clustered Bar Chart — Performance breakdown by Property Condition
- Pie Chart — Revenue distribution by City
- Line Chart — Revenue and transaction volume by Month and Year (trend view)

**Filters available:** Year, Month, City, Agent Name, Property Condition

---

## Analytical Findings

### Sale Transactions Drive Nearly Two-Thirds of Revenue Despite Being Below 40% of Volume

Sale and Re-Sale transactions together generate 93.6% of total revenue (67.8% and 25.8% respectively) from only 54.3% of transaction volume. Rental and Lease transactions account for 45.6% of activity but contribute just 6.4% of revenue combined.

**Implication:** While rental volume keeps the agent network active and feeds the client pipeline, the commercial weight of the business sits in ownership transactions. Commission structure design and agent KPIs should reflect this asymmetry — rewarding sale closures more heavily than rental throughput. For Rental-specialized agents, the dashboard should track lead-to-sale conversion as a secondary metric to surface agents who use rentals as a funnel into higher-value sales.

### Revenue is Distributed Nearly Evenly Across All Eight Cities

The eight cities each contribute between 11% and 14% of total revenue, with Alexandria (14.0%) and Dubai (14.0%) at the top and Giza, Amman, and Riyadh (each 11%) at the bottom. The spread between the highest and lowest city is under 3 percentage points.

**Implication:** The near-uniform distribution indicates either a well-balanced regional network or that no specific city has been deliberately prioritized for growth. Uniform revenue does not imply uniform profitability — the next analytical layer should examine commission yield per city (CommissionEGP / FinalPriceEGP) and operating cost density to identify whether certain cities are generating revenue at lower margin or higher acquisition cost. Alexandria's leadership at the highest average deal size (EGP 1.23M) suggests it may be the natural candidate for premium-property focus.

### Property Quality is a Stronger Revenue Lever than Property Type

Excellent and New condition properties together account for 66% of revenue (38% and 28% respectively), while Needs Renovation properties contribute only 9% despite representing nearly 10% of transactions. Within property types, Penthouses lead at 29% of revenue from 13.4% of transactions — clear evidence that premium-format properties drive disproportionate value.

**Implication:** Listing acquisition strategy should prioritize Excellent-condition and New properties, particularly in the Penthouse and Villa categories, which together generate 47% of revenue from 25% of transactions. For Needs Renovation inventory, the brokerage should consider whether the time investment per agent is justified by the lower deal value — or whether these properties should be channelled through a dedicated specialist rather than the general agent pool.

### Agent Revenue Distribution is Healthy, Not Pareto-Concentrated

The top 5 agents (12.5% of the agent base) generate 16.3% of revenue, and the top 10 (25%) generate 31.1%. This is notably flatter than the typical 80/20 concentration seen in real estate sales organizations, where top-decile agents often capture 40–60% of revenue.

**Implication:** A well-distributed performance curve is a positive signal — it reduces key-person risk and indicates training and onboarding are producing consistent output across the agent base. However, the lack of clear standouts also raises the question of whether the top performers are being recognized and retained appropriately, or whether the commission structure unintentionally flattens incentives. The dashboard's agent-level drill-down should be paired with a tenure overlay to confirm that top performers are not concentrated in a specific experience cohort that may eventually churn.

### Cancellation Rates Cluster Geographically

Dubai (12.9%), Riyadh (11.9%), and Cairo (11.7%) carry the highest cancellation rates, while Giza (8.0%) and Jeddah (8.0%) carry the lowest — a 5-percentage-point spread between best and worst markets.

**Implication:** Cancellation differentials of this size warrant investigation rather than acceptance as random variation. Possible drivers include inspection or documentation friction specific to certain regulatory environments, agent experience mix differing by city, or pricing/negotiation discipline. A targeted root-cause analysis on Dubai and Riyadh cancellations could recover meaningful revenue — at the current average deal size of EGP 1.03M, every prevented cancellation in those two markets is worth approximately EGP 1M in topline impact.

### Year-Over-Year Growth is Steady but Moderate

Transaction volume grew from 969 (2022) to 1,006 (2023) to 1,025 (2024), and revenue grew from EGP 934M to EGP 1.05B to EGP 1.11B — roughly 8.5% annual revenue growth with much flatter volume growth (under 6% over the two-year span).

**Implication:** Revenue is growing faster than volume, meaning average deal size is rising — a positive signal for either market appreciation or successful upmarket movement. However, the modest volume growth suggests the brokerage is capturing more value per transaction rather than expanding its market footprint. If growth strategy is volume-led, this trend indicates the current acquisition channels (which are distributed nearly evenly across seven lead sources, none above 16% of revenue) may need consolidation around the highest-converting channel rather than continued even spread.

---

## Tools & Technologies

| Tool             | Application                                                               |
| ---------------- | ------------------------------------------------------------------------- |
| Microsoft Excel  | Data source and star schema design                                        |
| Power BI Desktop | Data modeling, DAX measures, report authoring                             |
| Power Query (M)  | Data loading and transformation                                           |
| DAX              | KPI measures — Total Revenue, Commissions, Units Sold, Client Count       |

---

## Repository Structure

```
real-estate-sales-dashboard/
│
├── Real_Estate_Practice_Dataset.xlsx   # Source data (star schema, 6 sheets)
├── Real_Estate_Sales_Dashboard.pbix    # Power BI report file
├── Dashboard.png
└── README.md
```

---

## Setup Instructions

1. Clone this repository.
2. Open `Real_Estate_Practice_Dataset.xlsx` — no modifications are required; it is the static data source.
3. Open `Real_Estate_Sales_Dashboard.pbix` in Power BI Desktop.
4. If prompted, update the data source path to the local location of the Excel file.
5. Click Refresh — all visuals and KPIs will populate automatically.

---

## Author

**Abdallah ElZakaziky** — [LinkedIn](https://www.linkedin.com/in/abdallahelzakaziky/)