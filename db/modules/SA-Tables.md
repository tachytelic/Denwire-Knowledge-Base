# Denwire Sales Analysis Tables (SA)

Tables prefixed `sa` belong to the Sales Analysis module of the Strategix ERP system.
These tables are populated from invoiced sales order lines and provide pre-aggregated
period statistics for reporting. The primary transaction table is **saday**.

---

## saday — Sales Analysis Daily Ledger

The core transaction-level sales analysis table. One row per invoiced line item.
This is the best source for ad-hoc sales reporting — contains everything needed
without joining SO tables.

| Column | Type | Nulls |
|--------|------|-------|
| sad_seq | serial | no |
| sad_account | char(10) | yes |
| sad_deladd | char(4) | yes |
| sad_product | char(40) | yes |
| sad_qty | float | yes |
| sad_value | float | yes |
| sad_cosval | float | yes |
| sad_dscval | float | yes |
| sad_unitprice | float | yes |
| sad_unitcost | float | yes |
| sad_docdat | date | yes |
| sad_ordref | char(8) | yes |
| sad_ref | char(8) | yes |
| sad_rep | char(4) | yes |
| sad_area | char(4) | yes |
| sad_van | char(4) | yes |
| sad_prdgrp | char(4) | yes |
| sad_stloc | char(5) | yes |
| sad_year | smallint | yes |
| sad_period | smallint | yes |
| sad_icflag | char(1) | yes |
| sad_psource | char(1) | yes |
| sad_currency | char(4) | yes |
| sad_ccwt | char(2) | yes |
| sad_job | char(5) | yes |
| sad_ledpst | char(1) | yes |
| sad_usage | char(4) | yes |
| sad_category | char(4) | yes |
| sad_class | char(4) | yes |

---

## sacustat — Customer/Product Period Statistics

Pre-aggregated sales statistics by customer + product + year, summed into 13 accounting
periods. Faster than querying saday for period comparisons. Also holds week-to-date
accumulators.

| Column | Type | Nulls |
|--------|------|-------|
| sacus_cust | char(10) | yes |
| sacus_deladd | char(4) | yes |
| sacus_pcode | char(40) | yes |
| sacus_loc | char(5) | yes |
| sacus_year | smallint | yes |
| sacus_lastpur | date | yes |
| sacus_pgroup | char(4) | yes |
| sacus_category | char(4) | yes |
| sacus_usage | char(4) | yes |
| sacus_class | char(4) | yes |
| sacus_rep | char(4) | yes |
| sacus_area | char(4) | yes |
| sacus_van | char(4) | yes |
| sacus_icflag | char(1) | yes |
| sacus_keyfields | char(52) | yes |
| sacus_qty1 | float | yes |
| sacus_qty2 | float | yes |
| sacus_qty3 | float | yes |
| sacus_qty4 | float | yes |
| sacus_qty5 | float | yes |
| sacus_qty6 | float | yes |
| sacus_qty7 | float | yes |
| sacus_qty8 | float | yes |
| sacus_qty9 | float | yes |
| sacus_qty10 | float | yes |
| sacus_qty11 | float | yes |
| sacus_qty12 | float | yes |
| sacus_qty13 | float | yes |
| sacus_val1 | float | yes |
| sacus_val2 | float | yes |
| sacus_val3 | float | yes |
| sacus_val4 | float | yes |
| sacus_val5 | float | yes |
| sacus_val6 | float | yes |
| sacus_val7 | float | yes |
| sacus_val8 | float | yes |
| sacus_val9 | float | yes |
| sacus_val10 | float | yes |
| sacus_val11 | float | yes |
| sacus_val12 | float | yes |
| sacus_val13 | float | yes |
| sacus_cos1 | float | yes |
| sacus_cos2 | float | yes |
| sacus_cos3 | float | yes |
| sacus_cos4 | float | yes |
| sacus_cos5 | float | yes |
| sacus_cos6 | float | yes |
| sacus_cos7 | float | yes |
| sacus_cos8 | float | yes |
| sacus_cos9 | float | yes |
| sacus_cos10 | float | yes |
| sacus_cos11 | float | yes |
| sacus_cos12 | float | yes |
| sacus_cos13 | float | yes |
| sacus_dsc1 | float | yes |
| sacus_dsc2 | float | yes |
| sacus_dsc3 | float | yes |
| sacus_dsc4 | float | yes |
| sacus_dsc5 | float | yes |
| sacus_dsc6 | float | yes |
| sacus_dsc7 | float | yes |
| sacus_dsc8 | float | yes |
| sacus_dsc9 | float | yes |
| sacus_dsc10 | float | yes |
| sacus_dsc11 | float | yes |
| sacus_dsc12 | float | yes |
| sacus_dsc13 | float | yes |
| sacus_qtyweek | float | yes |
| sacus_valweek | float | yes |
| sacus_cosweek | float | yes |
| sacus_dscweek | float | yes |
| sacus_postweek | smallint | yes |

---

## sarepstat — Rep/Area Period Statistics

Same aggregation pattern as sacustat but keyed by rep/area rather than customer.
Additionally stores 13-period **budget** figures alongside actuals — used for
budget vs actual by rep reporting.

| Column | Type | Nulls |
|--------|------|-------|
| sarep_type | char(1) | yes |
| sarep_code1 | char(4) | yes |
| sarep_code2 | char(4) | yes |
| sarep_stloc | char(5) | yes |
| sarep_yearst | smallint | yes |
| sarep_prodmngr | char(4) | yes |
| sarep_budg1 | float | yes |
| sarep_budg2 | float | yes |
| sarep_budg3 | float | yes |
| sarep_budg4 | float | yes |
| sarep_budg5 | float | yes |
| sarep_budg6 | float | yes |
| sarep_budg7 | float | yes |
| sarep_budg8 | float | yes |
| sarep_budg9 | float | yes |
| sarep_budg10 | float | yes |
| sarep_budg11 | float | yes |
| sarep_budg12 | float | yes |
| sarep_budg13 | float | yes |
| sarep_qty1 | float | yes |
| sarep_qty2 | float | yes |
| sarep_qty3 | float | yes |
| sarep_qty4 | float | yes |
| sarep_qty5 | float | yes |
| sarep_qty6 | float | yes |
| sarep_qty7 | float | yes |
| sarep_qty8 | float | yes |
| sarep_qty9 | float | yes |
| sarep_qty10 | float | yes |
| sarep_qty11 | float | yes |
| sarep_qty12 | float | yes |
| sarep_qty13 | float | yes |
| sarep_value1 | float | yes |
| sarep_value2 | float | yes |
| sarep_value3 | float | yes |
| sarep_value4 | float | yes |
| sarep_value5 | float | yes |
| sarep_value6 | float | yes |
| sarep_value7 | float | yes |
| sarep_value8 | float | yes |
| sarep_value9 | float | yes |
| sarep_val10 | float | yes |
| sarep_val11 | float | yes |
| sarep_val12 | float | yes |
| sarep_val13 | float | yes |
| sarep_cos01 | float | yes |
| sarep_cos02 | float | yes |
| sarep_cos03 | float | yes |
| sarep_cos04 | float | yes |
| sarep_cos05 | float | yes |
| sarep_cos06 | float | yes |
| sarep_cos07 | float | yes |
| sarep_cos08 | float | yes |
| sarep_cos09 | float | yes |
| sarep_cos10 | float | yes |
| sarep_cos11 | float | yes |
| sarep_cos12 | float | yes |
| sarep_cos13 | float | yes |
| sarep_dsc1 | float | yes |
| sarep_dsc2 | float | yes |
| sarep_dsc3 | float | yes |
| sarep_dsc4 | float | yes |
| sarep_dsc5 | float | yes |
| sarep_dsc6 | float | yes |
| sarep_dsc7 | float | yes |
| sarep_dsc8 | float | yes |
| sarep_dsc9 | float | yes |
| sarep_dsc10 | float | yes |
| sarep_dsc11 | float | yes |
| sarep_dsc12 | float | yes |
| sarep_dsc13 | float | yes |

---

## sacuprod — Customer/Product Transaction History

A lighter transaction table similar to saday but scoped to customer + product history.
Useful for "what has this customer bought" style queries.

| Column | Type | Nulls |
|--------|------|-------|
| sac_customer | char(10) | yes |
| sac_deladd | char(4) | yes |
| sac_stloc | char(5) | yes |
| sac_product | char(40) | yes |
| sac_seq | smallint | yes |
| sac_qty | float | yes |
| sac_price | float | yes |
| sac_cost | float | yes |
| sac_dsc | float | yes |
| sac_unitprice | float | yes |
| sac_idate | date | yes |
| sac_ordref | char(8) | yes |

---

## sacomrat — Commission Rates

Commission rate lookup table by code pair and type.

| Column | Type | Nulls |
|--------|------|-------|
| sacom_code1 | char(4) | yes |
| sacom_code2 | char(4) | yes |
| sacom_rate | float | yes |
| sacom_type | char(1) | yes |

---

## sapara — Sales Analysis Parameters

Single-row system configuration table. Controls which financial years the SA module
treats as current and prior year. Check `sapar_cusyear` and `sapar_db1year` /
`sapar_db2year` before writing year-based queries — these define the active years,
not the calendar year.

| Column | Type | Nulls |
|--------|------|-------|
| sapar_cusyear | smallint | yes |
| sapar_db1year | smallint | yes |
| sapar_db2year | smallint | yes |
| sapar_dbstloc | char(2) | yes |
| sapar_proofno | integer | yes |
| sapar_dbkeys | char(4) | yes |
| sapar_analloc | char(1) | yes |
| sapar_analteam | char(1) | yes |
| sapar_dummy | char(1) | yes |

---

## satemp — Temporary Reporting Work Table

Populated during SA report generation and cleared afterwards. Holds both current-year
and prior-year (prefixed `y`) period columns plus week-to-date and grand totals.
**Do not query this for live data** — contents depend on whether a report is currently
being generated.

| Column | Type | Nulls |
|--------|------|-------|
| sat_loc | char(5) | yes |
| sat_cust | char(10) | yes |
| sat_deladd | char(4) | yes |
| sat_pcode | char(40) | yes |
| sat_pgroup | char(4) | yes |
| sat_category | char(4) | yes |
| sat_usage | char(4) | yes |
| sat_class | char(4) | yes |
| sat_rep | char(4) | yes |
| sat_area | char(4) | yes |
| sat_van | char(4) | yes |
| sat_icflag | char(1) | yes |
| sat_agroup | char(10) | yes |
| sat_pid | integer | yes |
| sat_conc | char(55) | yes |
| sat_conc2 | char(40) | yes |
| sat_sortval | float | yes |
| sat_qty1–13 | float | yes |
| sat_val1–13 | float | yes |
| sat_cos1–13 | float | yes |
| sat_dsc1–13 | float | yes |
| sat_yqty1–13 | float | yes |
| sat_yval1–13 | float | yes |
| sat_ycos1–13 | float | yes |
| sat_ydsc1–13 | float | yes |
| sat_qtyweek | float | yes |
| sat_valweek | float | yes |
| sat_cosweek | float | yes |
| sat_dscweek | float | yes |
| sat_qtytot | float | yes |
| sat_valtot | float | yes |
| sat_costot | float | yes |
| sat_ptstot | float | yes |
| sat_wttot | float | yes |

---

## Key notes for report writing

- **Use `saday` for transaction-level queries** (date ranges, by rep, by customer, by product).
  It has `sad_rep`, `sad_area`, `sad_ordref`, `sad_period`, `sad_year` — everything in one table.
- **Use `sacustat` for period summaries** when you need qty/value/cost across all 13 periods
  for a customer or product without summing thousands of saday rows.
- **Use `sarepstat` for budget vs actual** — it's the only table with budget figures.
- The period columns (1–13) correspond to the company's accounting periods, not calendar months.
  Period 1 start date depends on the financial year configured in `sapara`.
- `sad_icflag` distinguishes invoice (`I`) from credit note (`C`) lines — always filter
  or account for this in value totals.
