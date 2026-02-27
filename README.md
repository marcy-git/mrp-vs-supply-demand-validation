# 🏭 MRP vs Supply & Demand — New Buys Validation

## 🔍 Overview
Excel model that cross-references MRP purchase recommendations against 
actual Supply & Demand data, identifying cases where multi-region inventory 
coverage makes a new buy unnecessary.

## ❗ Business Problem
MRP systems generate purchase recommendations per warehouse independently.
When a Part Number is set up across **multiple warehouses (multi-region)**, 
the system can suggest a new buy for WH-A even when WH-B already has 
enough stock to cover the need — leading to unnecessary purchases.

## 🛠️ Tools
- Microsoft Excel · Power Query

## 📊 Dataset (Anonymized)
- 198 MRP lines across 7 warehouse codes
- 48,000+ row Supply & Demand file (sample of multi-region PNs included)
- Fields: Part Number, Warehouse, Quantity, CRD, Lead Times, Monthly S&D

## ⚙️ How It Works
```
1. INPUT_MRP   → Raw MRP output with new buy recommendations
2. INPUT_S&D   → Supply & Demand snapshot filtered to multi-region PNs
3. BUY_LIST    → Delta calculation → BUY or NO BUY recommendation
```

## ✅ Key Logic
```
If S&D coverage across all warehouses >= MRP Qty → NO BUY
If a gap remains after netting multi-region supply → BUY (delta qty)
```

## 📈 Results
- 175 total recommendations: **116 BUY / 59 NO BUY**
- Prevented unnecessary POs by identifying cross-warehouse coverage
- Replaced manual review of 200+ MRP lines with a structured, repeatable process

## 📁 Files
- `MRP_vs_SD_ANONYMIZED.xlsx` — Full model with anonymized data
- `Project_Description_MRP_vs_SD.md` — Detailed project documentation
