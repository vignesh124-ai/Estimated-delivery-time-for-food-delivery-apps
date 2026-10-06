# Food Delivery Time Prediction (Random Forest + Power BI)

Applied Predictive Analytics case study, Chaitanya Bharathi Institute of Technology.

**Team:** Vignesh (160124771030), Sri Vardhan (160124771031), Harshith (160124771033)

## Overview
Delivery times vary widely with distance, traffic, weather and rider factors. This project predicts delivery time (minutes) per order with a Random Forest Regressor, classifies each order into a Low / Medium / High delay-risk band, and visualises the results in a Power BI dashboard.

**Pipeline:** Dataset → Cleaning → Feature Engineering → Label Encoding → Random Forest → Predictions → Power BI

## Dataset
Public real-world food-delivery dataset (Kaggle, "Food Delivery Dataset" by Gaurav Malik), 45,584 orders, 20 columns. It is used here as a proxy for a Swiggy/Zomato-style delivery platform.
File: `data/zomato_delivery_dataset.csv`

## Features (17)
- **Distance:** Haversine distance between restaurant and drop point (km)
- **Time:** order day, month, weekday, order time, pickup time, pickup delay
- **Context:** weather, road traffic density, festival flag, city type
- **Rider & order:** rider age and rating, vehicle type and condition, order type, multiple deliveries

## Model
Random Forest Regressor (100 trees), 80/20 train-test split (`random_state=42`), categorical variables label-encoded.

## Results (20% hold-out set, 9,117 orders)
| Metric | Value |
|---|---|
| MAE | 3.18 min |
| RMSE | 4.02 min |
| R² | 0.816 |
| Avg. actual delivery time | 26.23 min |
| Avg. predicted delivery time | 26.33 min |
| Orders flagged High risk (predicted > 40 min) | 8.43% |

Delay-risk bands by predicted time: Low ≤ 30 min, Medium 30–40 min, High > 40 min.

## Repository structure
```
├── data/
│   ├── zomato_delivery_dataset.csv      # raw input data
│   └── Zomato_PowerBI_Predictions.csv   # model output used by Power BI
├── notebooks/
│   └── Delivery_Time_Random_Forest.ipynb
├── dashboard/
│   └── delivery_dashboard.pbix          # open with Power BI Desktop
├── docs/
│   ├── Case_Study.pptx
│   └── Swiggy_Case_Study_Redesigned.pdf
├── requirements.txt
└── README.md
```

## How to run
```bash
pip install -r requirements.txt
jupyter notebook notebooks/Delivery_Time_Random_Forest.ipynb
```
Run all cells; predictions are written to `data/`. Then open the `.pbix` in Power BI Desktop and refresh the data source to point at `data/Zomato_PowerBI_Predictions.csv`.

## Dashboard
KPI cards (total orders, avg. actual vs predicted time, high-risk %), predicted vs actual by traffic level, average delivery time by weather and city type, with filters for date, traffic and city.
