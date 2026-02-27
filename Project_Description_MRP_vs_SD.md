# 🏭 MRP vs Supply & Demand — New Buys Validation

## Project Overview

Developed a validation model to cross-reference MRP-generated purchase recommendations 
against actual Supply & Demand data, identifying cases where the system overlooks 
multi-region inventory coverage and flagging whether a new buy is truly needed.

## Business Problem

MRP (Material Requirements Planning) systems generate purchase recommendations based 
on demand signals, but they often lack visibility into **multi-region inventory**. 
A Part Number (PN) may be set up across multiple Warehouses (WH), and the MRP 
treats each WH independently — meaning it can suggest a new buy for WH-A even when 
WH-B already has sufficient stock to cover the need.

Manually reviewing 200+ MRP lines against a 48,000-row S&D file every planning cycle 
was time-consuming and prone to error.

## Solution

Built a 3-tab Excel model that:

1. **INPUT_MRP** — Loads the raw MRP output with new buy recommendations (PN, WH, QTY, CRD)
2. **INPUT_S&D** — Loads the Supply & Demand snapshot, filtered to multi-region PNs 
   (those set up in more than one warehouse)
3. **BUY_LIST** — Cross-references both sources to calculate the delta between MRP quantity 
   and actual S&D coverage, producing a final recommendation: **BUY** or **NO BUY**

## Tools & Techniques

| Tool | Usage |
|---|---|
| **Microsoft Excel** | Model structure, BUY_LIST logic, final output |
| **Power Query** | Data ingestion and transformation from ERP exports |
| **Composite key logic** | PN + WH matching across sources |
| **Delta calculation** | MRP_Qty vs S&D coverage to determine final buy qty |

## Dataset (Anonymized)

- **198 MRP lines** across 7 warehouse codes
- **48,000+ S&D rows** (sample of 460 multi-region rows included)
- **175 final recommendations**: 116 BUY / 59 NO BUY

## Key Logic

```
If S&D coverage across all WH for a PN >= MRP Qty → NO BUY
If gap exists after netting multi-region supply → BUY (delta qty)
```

## Impact

- Prevented unnecessary purchase orders by identifying cross-WH coverage
- Reduced manual review time per planning cycle significantly
- Provided buyers with a clear, auditable action list instead of raw MRP output

## Skills Demonstrated

`Excel` · `Power Query` · `Supply Chain Analytics` · `MRP` · `Inventory Planning` · 
`Multi-region Analysis` · `Data Validation` · `Procurement Operations`

---

*Data has been fully anonymized. Part Numbers, Warehouse Codes, and Manufacturer names 
have been replaced with generic identifiers. S&D data reduced to a representative 
sample of multi-region PNs for illustration purposes.*
