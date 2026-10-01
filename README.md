# Predictive-Retail-Inventory-Optimization
# Predictive Retail Inventory & Supply Chain Optimization

An end-to-end retail analytics project that combines **machine learning demand forecasting** with **inventory optimization** to support data-driven replenishment decisions.

The project uses historical Walmart retail sales data to forecast weekly demand, calculate inventory parameters such as **EOQ, Safety Stock, and Reorder Point**, simulate different inventory policies, and visualize key forecasting and inventory KPIs using **Power BI**.

---

## 📌 Project Overview

Retailers need to maintain enough inventory to satisfy customer demand while avoiding excessive inventory and associated holding costs.

This project addresses the problem in two stages:

1. **Demand Forecasting** – Predict future weekly sales for each Store-Department combination.
2. **Inventory Optimization** – Use demand forecasts to determine reorder points, safety stock, and order quantities, and compare different inventory policies.

The final results are presented through an interactive **Power BI dashboard**.

---

## 🎯 Objectives

- Forecast weekly retail demand using machine learning.
- Compare multiple regression and machine learning models.
- Use historical demand patterns such as lag and rolling-average features.
- Calculate **Economic Order Quantity (EOQ)** and **Safety Stock**.
- Determine inventory reorder points.
- Simulate inventory policies under a 2-week lead-time assumption.
- Compare ordering, holding, and stockout costs.
- Build a Power BI dashboard for monitoring forecasting and inventory KPIs.

---

## 🗂️ Dataset

The project uses the **Walmart Store Sales Forecasting dataset**, consisting of:

- `train.csv` – Historical weekly sales
- `features.csv` – Additional store-level and economic features
- `stores.csv` – Store information

The datasets are merged using:

- Store
- Date
- IsHoliday

### Key Variables

| Variable | Description |
|---|---|
| Store | Store identifier |
| Dept | Department identifier |
| Date | Week/date of observation |
| Weekly_Sales | Weekly sales |
| IsHoliday | Holiday indicator |
| Temperature | Temperature |
| Fuel_Price | Fuel price |
| CPI | Consumer Price Index |
| Unemployment | Unemployment rate |
| MarkDown1–5 | Promotional markdown information |
| Type | Store type |
| Size | Store size |

---

## 🔧 Data Preprocessing

The following preprocessing steps were performed:

- Merged sales, feature, and store datasets.
- Sorted observations by Store, Department, and Date.
- Filled missing markdown values with `0`.
- Forward-filled and backward-filled CPI and unemployment values within stores.
- Converted categorical variables into numerical representations.
- Extracted:
  - Year
  - Month
  - Week
- Clipped negative sales values to zero for demand modeling.

---

## 📈 Feature Engineering

Historical demand features were created for each **Store-Department** combination.

### Lag Features

- `Lag_1` – Previous week's sales
- `Lag_4` – Sales approximately 4 weeks earlier
- `Lag_13` – Sales approximately 13 weeks earlier
- `Lag_52` – Sales approximately one year earlier

### Rolling Features

- `Rolling_4` – Previous 4-week average demand
- `Rolling_12` – Previous 12-week average demand

The rolling features were calculated using shifted values to avoid directly including the current week's sales.

---

## 🤖 Demand Forecasting

Multiple models were trained and evaluated:

- Linear Regression
- Decision Tree
- K-Nearest Neighbors (KNN)
- Random Forest
- HistGradientBoosting
- XGBoost

A **last-year sales baseline** was also included using sales from approximately 364 days earlier.

### Evaluation Metrics

The models were evaluated using:

- MAE
- RMSE
- WAPE
- R²

### Best Result

The Random Forest model achieved approximately:

**8.2% WAPE**

compared with approximately:

**11.2% WAPE for the last-year naive baseline.**

This indicates that the machine-learning model provided lower forecast error than the historical baseline on the evaluated holdout period.

---

## 📦 Inventory Optimization

The forecasting model was connected to an inventory simulation framework.

The project calculates:

### Economic Order Quantity (EOQ)

EOQ determines an order quantity that balances ordering and holding costs.

### Safety Stock

Safety stock is calculated using forecast error, service-level assumptions, and the assumed lead time.

### Reorder Point

For the forecast-driven policy, the reorder point is based on:

**Expected lead-time demand + Safety Stock**

---

## 🚚 Inventory Simulation

A **2-week lead time** was assumed for replenishment.

The simulation tracks:

- On-hand inventory
- Incoming orders
- Inventory position
- Customer demand
- Lost sales
- Number of orders
- Ordering cost
- Holding cost
- Stockout cost
- Total inventory cost

Three policies were compared:

### Policy A – Historical Average

Uses historical average weekly demand as the ordering reference.

### Policy B – Static Reorder Point

Uses historical demand and a static reorder-point approach.

### Policy C – Forecast-Driven

Uses predicted demand over the lead-time period plus safety stock to determine the reorder point.

---

## 💰 Cost Model

The inventory simulation uses the following assumptions:

| Parameter | Assumption |
|---|---:|
| Unit Price | $25 |
| Annual Holding Rate | 25% |
| Ordering Cost | $100/order |
| Stockout Cost | 40% of unit price |
| Lead Time | 2 weeks |

> **Note:** Inventory costs and policy comparisons are simulated results based on these assumptions. They do not represent Walmart's actual inventory costs or savings.

---

## 📊 Power BI Dashboard

The final analysis is visualized in Power BI.

The dashboard includes:

- Model WAPE
- Naive baseline WAPE
- Forecast performance
- Inventory cost
- Fill rate
- Low-cover inventory count
- Cost comparison between inventory policies
- Forecast vs. actual demand
- Inventory-related KPIs

The dashboard allows the forecasting and inventory results to be viewed from a business and supply-chain perspective.

---

## 🛠️ Tech Stack

### Programming & Analytics
- Python
- Pandas
- NumPy
- Scikit-learn

### Machine Learning
- Linear Regression
- Decision Tree
- KNN
- Random Forest
- HistGradientBoosting
- XGBoost

### Visualization & BI
- Power BI
- Matplotlib

### Development
- Jupyter Notebook
- Git
- GitHub

---

## 🔄 Project Workflow

```text
Raw Walmart Data
       ↓
Data Cleaning & Merging
       ↓
Feature Engineering
       ↓
Lag & Rolling Demand Features
       ↓
Train ML Models
       ↓
Evaluate Forecast Accuracy
       ↓
Select Forecast Model
       ↓
Calculate Safety Stock & EOQ
       ↓
Determine Reorder Points
       ↓
Simulate Inventory Policies
       ↓
Compare Costs & Service Levels
       ↓
Power BI Dashboard
