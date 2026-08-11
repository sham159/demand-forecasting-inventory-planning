# Demand Forecasting & Inventory Planning Analytics

End-to-end supply chain planning project built with **SQL + Excel** - cleaning, demand analysis, ABC-XYZ segmentation, forecast validation, and live-formula inventory planning (Safety Stock, ROP, EOQ, stockout/overstock risk).

## Data
- Source: [Retail Store Inventory & Demand Forecasting](https://www.kaggle.com/datasets/atomicd/retail-store-inventory-and-demand-forecasting) (Kaggle)
- 73,100 daily records — 5 stores × 20 products × 2 years (2022–2024)
- Fields: Date, Store, Product, Category, Inventory Level, Units Sold, Price, Discount, etc.

## What I did
1. **SQL cleaning (SQLite):** duplicate, null, negative-value, and referential-integrity checks on 73,100 rows.
2. **Data-integrity finding:** `Product ID` alone is not a stable SKU key — it's inconsistently tagged across all 5 categories. Redefined the SKU grain as `Store ID + Product ID` (100 SKUs, verified clean via SQL).
3. **SQL analysis:** SKU-level demand stats (avg daily demand, std dev, CV) and monthly time series, aggregated from the raw table.
4. **ABC-XYZ classification:** value-based Pareto split + a rank-based alternative (documented why the value-based method underperforms on this dataset's flat demand distribution).
5. **Forecast validation:** backtested Naive vs 3-month vs 6-month moving average on a real holdout period (Oct–Dec 2023, unseen in training). **6-month MA won**, cutting MAPE ~33% vs naive.
6. **Inventory planning:** Safety Stock, Reorder Point, EOQ, and stockout/overstock flags — all built as **live Excel formulas**, driven by an editable Assumptions tab (service level, lead time, cost inputs).

## File
- `Demand_Forecasting_Inventory_Planning.xlsx` — full workbook (ReadMe → Cleaning Log → SKU Master → ABC-XYZ → Forecast Accuracy → Assumptions → Inventory Planning → Dashboard)

## Tools
SQL (SQLite) · Excel (formulas, no hardcoded outputs) · ABC/XYZ analysis · Safety stock / ROP / EOQ · Forecast accuracy (MAE, RMSE, MAPE, Bias)
