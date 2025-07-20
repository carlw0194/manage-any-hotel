# Manage Any Hotel | Power BI Dashboard

A two‑page interactive report (Overview & Analysis) that helps **any** hotel manager track revenue, bookings, cancellations, ADR, and more—using the open‑source **[Hotel](https://www.kaggle.com/datasets/mojtaba142/hotel-booking) Booking** dataset.

## 📊 Key Features
| Page | Highlights |
|------|------------|
| **Overview** | KPI strip with YoY arrows, monthly trend, cancellation gauge,
| **Analysis** | Metric selector, distribution by channel & room, Top 15 country insight, Reserved v Assigned comparison |

## 🗄️ Dataset
* **Source:** [Hotel Booking](https://www.kaggle.com/datasets/mojtaba142/hotel-booking)
* **Strengths:** 119k rows, multi‑year, rich categorical fields (market, channel, room).
* **Weaknesses:** Imbalanced years (2014 sparse), missing ADR for cancelled stays.
* **Cleaning:** Removed 3% null ADR, unified country ISO3, generated Flag URLs.

## 🔄 Slicer Logic
* **Metric Selector** (field parameter) → drives all charts & dynamic titles.
* **Page Tabs** built with Power BI’s Page Navigator; hover underline + selected pill.

## 🚀 How to Use
1. Select **Hotel Type** & **Year** in the header pills.
2. Hover any chart for rich tooltips.
3. Click **Reset** or **Clear all slicers** to return to defaults.

## 🤖 Tech
* Power BI Desktop Apr 2025
* Flag images via `https://flagcdn.com/w40/{iso2}.png`
* Custom visual. chiclet , tornado charts and paypal donut kpi charts

## 📑 Insights & Recommendations
1. **Portugal** delivers highest revenue ($11M) with avg ADR$140—double down on promotions.
2. **Resort Hotel** faces 37% cancellation—revisit deposit policy.
3. **GDS channel** drives highest ADR but only 8% bookings—expand negotiated rates.

## 📹 Video Walk‑through
_Link coming soon_

## 🌐 Live Report
* Power BI Service (app link)
* GitHub Pages demo ➜ https://<username>.github.io/hotel-dashboard

