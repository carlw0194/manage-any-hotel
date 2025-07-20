# Manage Any Hotel | Power BI Dashboard

A two‑page interactive report (Overview & Analysis) that helps **any** hotel manager
**maximise revenue** while **minimising cancellations & revenue loss**—the core
challenge of hospitality revenue management—using the open‑source
[Hotel Booking Demand](https://www.kaggle.com/datasets/jessemostipak/hotel-booking-demand) dataset.

---

## 🧩 Business Problem

> **Goal:** Give a general manager (GM) a single dashboard that answers  
> “*Where can we earn more and lose less?*”

1. **Increase revenue:** spot high‑ADR, high‑volume markets & channels.  
2. **Reduce revenue leakage:** surface excessive cancellations & revenue loss.  
3. **Optimize room allocation:** compare reserved vs assigned room mix to cut free upgrades.

---

## 📊 Key Features

| Page | Highlights |
|------|------------|
| **Overview** | KPI strip with YoY arrows • monthly booking trend • cancellation gauge • global map |
| **Analysis** | Metric selector • breakdown by channel, room & segment • Top‑15 country table • Reserved v Assigned tornado |
### 📸 Dashboard Preview

| Overview | Analysis |
|----------|----------|
| ![Overview dashboard](screenshots/overview%20final%20version.PNG) | ![Analysis dashboard](screenshots/analysis%20final%20version.PNG) |
---

## 🗄️ Dataset & Assumptions

| Item | Detail |
|------|--------|
| **Source** | Kaggle – *Hotel Booking Demand* (Mojtaba, 119 k rows) |
| **Time span** | 2014–2017 |
| **Assumptions** | • ADR of cancelled bookings isn’t realised revenue  <br>• Lead‑time = days between booking and arrival <br>• Room upgrade “Cost” not in dataset, so focus on mix, not dollar impact |
| **Known gaps** | • No room occupancy tax/fees  <br>• No channel commission cost  |

---

## 🧹 Data‑Cleaning Summary

| Step | Rows / Cols | Rationale |
|------|-------------|-----------|
| delete non useful columns | –12 cols | 
| Drop bookings with **null ADR** | –3% rows | Cannot price revenue/ADR |
| Standardise **country codes** | 7 typos fixed | Ensures map joins & flag lookup |
| Add `Booking Date`, `Weekday`, `Lead‑Time Bucket`, `Nights` columns | +4 cols | Drives time intelligence & slicers |
| Build **Flag URL** PNG | +1 col | Render country flags via FlagCDN |

*(Full M‑code  in `/M_code_adding_flags.md`)*

---

## 🗄️ Data‑Modelling Folder

The report follows a classic **star schema**:

| Table | Role | Key Columns | Why Needed |
|-------|------|-------------|------------|
| `hotel_booking` | Fact | Booking-level fields | Central fact table feeding all visuals |
| `Date` | Calendar | Date, Year, Month, Weekday | Enables YTD / YoY via SAMEPERIODLASTYEAR, TOTALYTD, etc. |
| `CountryFlags` | Lookup | ISO3, ISO2, Country, FlagURL | Clean country names & render PNG flags |

<details>
<summary>Schema preview</summary>
🔄 Slicer Logic
Slicer	Type	Purpose
Metric Selector	Field parameter	Swaps KPIs (Bookings, ADR, Revenue, etc.)
Hotel Type	Tile	City vs Resort segmentation
Year	Tile	2015–2017 focus
Reset / Clear	Buttons	Quick reset of state


🚀 How to Use

    Choose Hotel Type & Year.

    Hover charts for tool‑tips; click bars or bubbles to cross‑filter.

    Hit Reset or Clear all slicers at any time.

---

🤖 Tech Stack

    Power BI Desktop Jul 2025

    Flag images via https://flagcdn.com/w40/{iso2}.png

    Custom visuals: Chiclet Slicer (metric pills), Nova Silva Tornado, PayPal Donut KPI

📑 Insights & Recommendations
#	Insight	Recommendation
1	Portugal tops revenue: $11 M, ADR $140.	Increase paid‑search budget & launch “remote‑work” package.
2	Resort Hotel cancellations 37 %.	Tighten deposit terms; 5 % discount for non‑refundable 14‑day bookings.
3	GDS channel ADR $156 but 8 % share.	Negotiate rate‑parity; add loyalty perks for GDS.

Full table with impact estimates in /insights/insights.md.
📹 Video Walk‑through

Link coming soon

🌐 Live Report
Platform
Power BI Service [Link](https://app.powerbi.com/view?r=eyJrIjoiMjY1MWRjNzItMDQyNy00NGI0LTg5NTktODQyZjU4NmI4Njg2IiwidCI6ImY1ZGYwMGE1LTc4NzQtNGViZi05MTkzLTIxOTI2ZTVmYmUyMiIsImMiOjl9)
GitHub Pages [Link](https://carlw0194.github.io/manage-any-hotel/)