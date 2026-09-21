# Mitron Bank – Credit Card Launch Analysis

![Power BI](https://img.shields.io/badge/Power%20BI-Data%20Visualization-yellow)
![DAX](https://img.shields.io/badge/DAX-Data%20Analysis-blue)
![Power Query](https://img.shields.io/badge/Power%20Query-Data%20Transformation-green)
![SQL](https://img.shields.io/badge/SQL-Data%20Analysis-orange)

## 📌 Project Overview

Mitron Bank, a legacy financial institution headquartered in Hyderabad, is planning to introduce a new line of credit cards.

To support this decision, a pilot dataset containing customer demographics and six months of spending behaviour was provided. This project analyses customer spending patterns, payment behaviour, income utilization, customer segments and city-level trends to identify opportunities for a successful credit card launch.

Built with **Power BI, Power Query, DAX and data modeling**, the project turns raw customer and transaction data into actionable business insights.

---

## 🎯 Business Problem

Mitron Bank needs data-driven insights before finalizing its credit card strategy:

- Which customer segments should the bank target?
- Which categories contribute the highest spending?
- Which payment methods do customers currently use, and how much spending is already on credit cards?
- Where is the opportunity to convert non-credit-card spending?
- Which age groups, cities, occupations and income bands represent the most valuable segments?
- How should the credit card rewards and acquisition strategy be designed?

The goal is not to report historical numbers, but to **translate customer behaviour into actionable recommendations for the credit card launch.**

---

## 💡 Approach

```text
Business Problem → Requirements → Data Understanding → Data Quality & Validation
→ Data Transformation → Data Modeling → KPI & DAX Development
→ Customer & Spending Analysis → Business Opportunities → Recommendations
→ Power BI Dashboard → Business Decision Support
```

---

## 📊 Dataset

| Table | Description | Records |
|---|---|---|
| `dim_customers` | Customer demographics and income (Customer_ID, Age_Group, City, Occupation, Gender, Marital_Status, Avg_Income) | 4,000 customers |
| `fact_spends` | Transaction-level spending (Customer_ID, Month, Category, Payment_Type, Spend) | 864,000 records |

**Analysis period:** May – October (6 months)

### Data Preparation (Power Query)

Column names and data types standardized, city names cleaned, income bands created, month sort order defined, and categorical fields prepared for visualization.

**Validation results:** no missing values, no duplicate transaction combinations, no negative or invalid spend values, and no orphan customer records.

---

## 🏗️ Data Model

A star-schema model with two dimensions filtering one fact table:

```text
dim_customers[Customer_ID]  1 : *  fact_spends[Customer_ID]
Month_Table[Month]          1 : *  fact_spends[Month]
```

This allows customer attributes and the month dimension to filter transaction-level spending efficiently.

---

## 📐 Key DAX Measures

```dax
Total Spend = SUM(fact_spends[Spend])

Total Customers = DISTINCTCOUNT(dim_customers[Customer_ID])

Avg Spend per Customer = DIVIDE([Total Spend], [Total Customers], 0)

Credit Card Share % =
DIVIDE(
    CALCULATE([Total Spend], fact_spends[Payment_Type] = "Credit Card"),
    [Total Spend],
    0
)

25-45 Spend Share % =
DIVIDE(
    CALCULATE([Total Spend], dim_customers[Age_Group] IN {"25-34", "35-45"}),
    [Total Spend],
    0
)
```

---

## 📈 Key KPIs

| KPI | Value |
|---|---|
| Total Customers | 4,000 |
| Spending Records | 864,000 |
| Total Spend | ₹530.90M |
| Avg 6-Month Spend / Customer | ₹132.72K |
| Avg Monthly Spend / Customer | ₹22.12K |
| Credit Card Spend Share | 40.74% |
| Non-Credit Spend Share | 59.26% |
| 25–45 Age Spend Share | 74.21% |
| Bills + Groceries + Electronics | 51.00% |
| Overall Income Utilization | 42.82% |

---

## 🔍 Key Findings

### 1. Age
Customers aged 25–45 contribute **74.21%** of total spending, making this the primary audience for the proposed card.

### 2. Payment Behaviour

| Payment Method | Spend Share |
|---|---|
| Credit Card | 40.74% |
| UPI | 26.53% |
| Debit Card | 22.52% |
| Net Banking | 10.21% |

**59.26%** of spending still runs through non-credit methods — the core conversion opportunity.

### 3. Spending Categories

| Category | Spend Share |
|---|---|
| Bills | 19.76% |
| Groceries | 16.26% |
| Electronics | 14.99% |
| Health & Wellness | 12.36% |
| Travel | 11.16% |

Bills, Groceries and Electronics together account for ~51% of total spend.

### 4. City Performance

| City | Total Spend | Income Utilization |
|---|---|---|
| Mumbai | ₹172.04M | 51.43% |
| Delhi-NCR | ₹111.45M | 48.03% |
| Bengaluru | ₹100.02M | 43.46% |
| Chennai | ₹79.87M | 31.10% |
| Hyderabad | ₹67.52M | 36.25% |

Mumbai leads on both total spend and income utilization.

### 5. Occupation

| Occupation | Total Spend | Avg Income |
|---|---|---|
| Salaried IT Employees | ₹243.72M | ₹61.50K |
| Business Owners | ₹88.00M | ₹70.09K |
| Salaried Other Employees | ₹87.51M | ₹38.79K |
| Freelancers | ₹75.54M | ₹35.06K |
| Government Employees | ₹36.12M | ₹52.03K |

Salaried IT employees drive the highest total spend; business owners hold the highest average income — two distinct dimensions of customer value.

### 6. Marital Status
Married customers make up 78.4% of the base and contribute **80.81%** of spending, pointing to household-oriented categories.

### 7. Monthly Trend

| Month | Total Spend |
|---|---|
| May | ₹68.14M |
| June | ₹79.32M |
| July | ₹80.62M |
| August | ₹100.86M |
| September | ₹115.93M |
| October | ₹86.03M |

September peaked at ₹115.93M.

### 8. Income Bands

| Income Band | Customers | Share |
|---|---|---|
| <40K | 1,250 | 31.25% |
| 40–80K | 2,701 | 67.53% |
| 80K–1.2L | 49 | 1.23% |
| 1.2L+ | 0 | 0% |

The opportunity sits in the mass-market ₹40K–₹80K band, not the premium segment.

---

## 🧠 Customer Segments

| Persona | Basis |
|---|---|
| **Digital-First Spender** | Strong UPI / net banking usage — prime conversion target |
| **Affluent Professional** | Salaried IT employees; high spend and solid income |
| **Business Owner** | Highest average income among occupation groups |
| **Value-Conscious Household** | Married, household-category-heavy spending |

---

## 💼 Business Recommendations

1. **Focus on the 25–45 segment** — 74.21% of total spend; build lifestyle and everyday-spend benefits around it.
2. **Build category-based rewards** — bills, groceries and electronics (51% of spend) form the foundation of the reward structure.
3. **Capture non-credit spending** — position the card as a better-value alternative to the UPI, debit and net banking spend that makes up 59.26% of volume.
4. **Segment by customer economics, not income alone** — pair spending behaviour with income (IT employees vs. business owners).
5. **Use regional insights** — pilot city-specific acquisition, merchant partnerships and offers in Mumbai, Delhi-NCR and Bengaluru.

---

## 📊 Power BI Dashboard

| Page | Contents |
|---|---|
| **Home** | Project overview, business problem, navigation |
| **Customer Overview** | Spend KPIs, age groups, payment mix, categories, city, occupation, monthly trend |
| **Customer Segmentation** | Personas, income and age segmentation, marital status, high-value customers |
| **Recommendations** | Findings translated into credit card launch strategy |

---

## 🛠️ Tools & Technologies

- **Power BI** – data modeling, interactive dashboards, KPI cards, business reporting
- **Power Query** – data cleaning, transformation, type handling, standardization
- **DAX** – measures, KPIs, share calculations, segmentation logic
- **Data Modeling** – star schema relationships across customer, spend and month tables

---

## 📁 Repository Structure

```text
mitron-bank-credit-card-analysis/
│
├── README.md
│
├── PowerBI/
│   └── Mitron_Bank_Credit_Card_Pilot.pbix
│
├── Dataset/
│   ├── dim_customers.csv
│   └── fact_spends.csv
│
├── Dashboard/
│   ├── Home.png
│   ├── Customer_Overview.png
│   ├── Customer_Segmentation.png
│   └── Recommendations.png
│
└── Documentation/
    └── Project_Insights.pdf
```

---

## 📌 Project Outcome

The analysis answers the questions that matter for the launch:

- **Who to target** — customers aged 25–45, salaried IT professionals and married households in the ₹40K–₹80K income band
- **Where the spend is** — bills, groceries and electronics (51% of total)
- **Where the conversion opportunity is** — the 59.26% of spend still on non-credit methods
- **Where to launch first** — Mumbai, Delhi-NCR and Bengaluru

The dashboard is built as a decision-support tool for credit card product strategy, not just a reporting layer.

---

## 📚 Skills Demonstrated

Business problem solving · Data cleaning & transformation · Data modeling · Power Query · DAX · KPI development · Customer segmentation · Financial and payment behaviour analysis · Data visualization · Insight generation · Data-driven recommendations
