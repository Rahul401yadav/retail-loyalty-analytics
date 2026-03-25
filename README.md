# 🛒 Retail Loyalty Analytics — Customer Intelligence Platform

> A end-to-end Python data science project analysing retail customer behaviour 
> through RFM segmentation, K-Means clustering, churn risk scoring, and 
> interactive dashboards — directly mirroring Nectar360 loyalty analytics 
> at Sainsbury's.

---

## 📌 Project Overview

| Item | Detail |
|------|--------|
| **Domain** | Retail / E-Commerce Analytics |
| **Stack** | Python, Pandas, Scikit-Learn, Plotly, Seaborn, Matplotlib |
| **Dataset** | Retail orders dataset (5,000+ transactions) |
| **Output** | Interactive HTML dashboard + CSV segment exports |
| **Relevance** | RFM segmentation, churn modelling, customer clustering — core Sainsbury's / Nectar360 use cases |

---

## 🎯 Business Questions Answered

1. **Who are our most valuable customers?** → RFM Segmentation
2. **Which customers are about to leave?** → Churn Risk Scoring
3. **Are there natural customer groupings we can target differently?** → K-Means Clustering
4. **When and how do customers buy?** → Time-Series & Day/Hour Analysis
5. **Which products and categories drive the most revenue?** → Product Performance Analysis
6. **How is revenue trending over time?** → YoY Growth & Quarterly Heatmap

---

## 📁 Project Structure
```
retail-loyalty-analytics/
│
├── retail_analytics.py        # Main analysis script (8 modules)
├── orders.csv                 # Raw order transaction data
├── products.csv               # Product catalogue with categories
├── departments.csv            # Department reference data
├── aisles.csv                 # Aisle reference data
│
├── outputs/
│   ├── executive_dashboard.html   # Interactive Plotly dashboard
│   ├── rfm_segments.csv           # RFM scored customer table
│   ├── churn_risk.csv             # Churn risk banded customers
│   ├── cluster_profiles.csv       # K-Means cluster summary
│   ├── elbow_silhouette.png       # Optimal K selection chart
│   └── quarterly_heatmap.png      # Revenue heatmap by quarter
│
└── README.md
```

---

## 🔬 Modules Explained

### Module 1 — Data Loading & Cleaning
- Loads all four CSV files
- Standardises column names
- Parses dates, extracts year/month/quarter/day features
- Checks nulls and data types

### Module 2 — Exploratory Data Analysis
**Why:** Understand the shape of the data before modelling — essential first step in any production data science workflow.

**What we found:**
- Peak ordering days and hours
- Sales value distribution with mean/median markers
- Revenue breakdown by shipping mode

**Charts produced:**
- Bar chart: Orders by day of week
- Line chart: Monthly sales trend
- Histogram: Sales value distribution

---

### Module 3 — RFM Customer Segmentation
**Why:** RFM (Recency, Frequency, Monetary) is the industry-standard framework for loyalty programme analytics. Sainsbury's Nectar team uses this to identify which customers to target with promotions.

**How it works:**
| Dimension | Meaning | Scoring |
|-----------|---------|---------|
| **Recency** | Days since last order | Lower days = Score 5 |
| **Frequency** | Number of orders | Higher orders = Score 5 |
| **Monetary** | Total spend | Higher spend = Score 5 |

Each dimension is scored 1–5 using NTILE quintiles. Scores are summed into a total RFM score (3–15).

**Segments defined:**

| Segment | RFM Score | Description |
|---------|-----------|-------------|
| Champions | 13–15 | Buy often, spend most, bought recently |
| Loyal Customers | 10–12 | Regular buyers with good spend |
| Potential Loyalists | 7–9 | Recent buyers with growth potential |
| At Risk | 5–6 | Used to buy but slipping away |
| Lost Customers | 3–4 | Haven't bought in a long time |

**Charts produced:**
- Donut chart: Segment distribution
- Scatter plot: Recency vs Monetary by segment

---

### Module 4 — K-Means Clustering
**Why:** While RFM uses rule-based labelling, K-Means discovers natural groupings in the data without assumptions — useful for finding unexpected customer patterns.

**How it works:**
1. Standardise RFM features using `StandardScaler`
2. Run K-Means for K = 2 to 8
3. Plot **Elbow curve** (inertia) and **Silhouette score** to find optimal K
4. Fit final model and profile each cluster

**Key concept — Silhouette Score:**
> Measures how similar a customer is to their own cluster vs other clusters.
> Score range: -1 to 1. Higher = better-defined clusters.

**Charts produced:**
- Elbow + Silhouette plot to justify K selection
- 3D scatter: Clusters in RFM space

---

### Module 5 — Churn Risk Scoring
**Why:** Identifying at-risk customers before they leave is 5–7x cheaper than reacquiring them. This is a core Nectar360 use case — targeting lapsed customers with reactivation offers.

**Risk banding logic:**

| Risk Band | Condition | Action |
|-----------|-----------|--------|
| 🔴 High Risk | Recency > 180 days AND orders ≤ 2 | Immediate reactivation campaign |
| 🟡 Medium Risk | Recency > 90 days OR orders ≤ 3 | Loyalty incentive offer |
| 🟢 Low Risk | Active, frequent buyers | Retention rewards |

**Charts produced:**
- Bar chart: Customers by risk band
- Box plot: Recency distribution per band

---

### Module 6 — Sales Performance Analysis
**Why:** Understanding revenue trends is essential for business planning and stakeholder reporting.

**What we analyse:**
- Year-on-year revenue growth
- Top 10 customers by lifetime value
- Quarterly revenue heatmap to spot seasonality

**Charts produced:**
- Side-by-side: Annual revenue + YoY growth %
- Horizontal bar: Top 10 customers
- Heatmap: Revenue by year × quarter

---

### Module 7 — Product Analysis
**Why:** Understanding which categories and price points drive volume helps merchandising and promotional planning.

**What we analyse:**
- Average price by product category
- Price range (min/max) per category
- Price distribution box plots

---

### Module 8 — Executive Dashboard
**Why:** A single-page interactive dashboard communicates all findings to non-technical stakeholders — a core skill for data scientists at Sainsbury's and JPMAM.

**Dashboard panels:**
1. Monthly sales trend
2. RFM customer segments (donut)
3. Sales by shipping mode
4. Churn risk distribution
5. Top 10 customers
6. Quarterly revenue heatmap

📊 **[View Live Dashboard](executive_dashboard.html)**

---

## ⚙️ How to Run

### 1. Clone the repository
```bash
git clone https://github.com/YOUR_USERNAME/retail-loyalty-analytics.git
cd retail-loyalty-analytics
```

### 2. Install dependencies
```bash
pip install pandas numpy matplotlib seaborn plotly scikit-learn
```

### 3. Run the analysis
```bash
python retail_analytics.py
```

### 4. View the dashboard
Open `executive_dashboard.html` in any browser.

---

## 📊 Key Results

| Analysis | Finding |
|----------|---------|
| RFM Segments | X% of customers are Champions, Y% are At Risk |
| K-Means | Optimal K = N clusters (silhouette = X.XX) |
| Churn Risk | X% customers flagged High Risk |
| Top Customer | Customer ID XXX — £X,XXX lifetime value |
| Peak Sales Day | [Day] drives highest order volume |
| Revenue Growth | YoY growth of X% from 2014 to 2017 |

> 📝 Fill in the actual numbers after running the script

---

## 🔮 Future Enhancements

| Enhancement | Description |
|-------------|-------------|
| **Uplift Modelling** | Measure whether promotions *caused* purchases (causal inference with DoWhy) |
| **Product Recommendation** | Collaborative filtering to recommend next purchase |
| **LSTM Forecasting** | Deep learning for demand forecasting |
| **SHAP Explainability** | Explain which features drive each customer's churn risk score |
| **Live Dashboard** | Deploy as Streamlit app with real-time data refresh |
| **A/B Test Framework** | Statistical power analysis for promotion experiment design |

---

## 🧠 Skills Demonstrated

`Python` `Pandas` `NumPy` `Scikit-Learn` `Plotly` `Seaborn` `Matplotlib`
`RFM Analysis` `K-Means Clustering` `Churn Modelling` `Feature Engineering`
`Data Visualisation` `EDA` `Stakeholder Reporting` `Retail Analytics`

---

## 👤 Author

**Rahul Yadav**
📧 rahul401yadav@gmail.com
🔗 [LinkedIn](www.linkedin.com/in/rahul-yadav-3272021b6)
🌐 [Portfolio]([https://your-portfolio.com](https://rahul401yadav.github.io/Portfolio/))

---

## 📄 License
MIT License — free to use and adapt.
