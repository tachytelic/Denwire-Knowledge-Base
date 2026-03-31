# Informix SQL Syntax Notes — Denwire

Reference for writing SQL against Informix 7.23.UC13 SE via the SCO Vision ODBC driver.

---

## The Golden Rule: Always Use sql_syntax=1

The SCO Vision ODBC driver has a `SQLSyntax` connection parameter that controls how SQL
is translated before being sent to Informix. **Always use mode 1.**

| Mode | Behaviour |
|------|-----------|
| 0 | Translate to native SQL (strict — errors on non-ODBC syntax) |
| **1** | **No translation — SQL passed directly to Informix** ← use this |
| 2 | Translate to native SQL (lenient — passes non-ODBC syntax through) |
| 3 | Try native first, translate on error ← was the old default, do NOT use |

**Why mode 3 is broken**: SQLSyntax=3 makes two round-trips per query (try → fail → translate
→ retry). Its translation layer corrupts `ORDER BY` clauses, producing a
"Cannot open file 'sql.iem'" Informix error. Mode 1 is single-pass and significantly faster.

In curl calls to the API, always include:
```
--data-urlencode "sql_syntax=1"
```

---

## Known Limitations of Informix 7.23 SE

These are hard engine limitations — no workaround at the query level:

| Feature | Status |
|---------|--------|
| `ORDER BY` | Works with sql_syntax=1 |
| `FIRST N` | **Not supported** — engine error even with sql_syntax=1 |
| `LIMIT N` | **Not supported** — MySQL/PostgreSQL syntax, fails on all modes |
| Cross-database queries | **Not supported** — SE only queries the current database (`denw`) |

### Top-N workaround

Use `MAX()`/`MIN()` in a subquery to find the boundary value, then filter:

```sql
-- Most recent order date, then fetch those orders
SELECT soh_ordref, soh_orddate, soh_account
FROM informix.sohead
WHERE soh_orddate = (SELECT MAX(soh_orddate) FROM informix.sohead)

-- Or filter to a known small date range
WHERE soh_orddate >= MDY(1,1,2026)
```

Alternatively, use `INTO TEMP` for multi-step operations (see below).

---

## Table Names

Always prefix with schema: `informix.tablename`

```sql
SELECT * FROM informix.sohead
```

---

## Date Handling

All of these work with sql_syntax=1:

| Syntax | Description | Example |
|--------|-------------|---------|
| `{d 'yyyy-mm-dd'}` | ODBC escape (processed client-side) | `WHERE soh_orddate = {d '2025-01-01'}` |
| `TODAY` | Current date constant | `WHERE soh_orddate = TODAY` |
| `MDY(m, d, y)` | Construct a date | `MDY(1, 1, 2026)` |
| `YEAR(col)` | Extract year | `WHERE YEAR(soh_orddate) = 2025` |
| `MONTH(col)` | Extract month | |
| `DAY(col)` | Extract day | |
| `WEEKDAY(col)` | Day of week (0=Sunday) | |
| `EXTEND(expr, YEAR TO DAY)` | Truncate datetime precision | |
| `TODAY - 365 UNITS DAY` | Date arithmetic | |
| `col + 30 UNITS DAY` | Add days to a date column | |

---

## Joins

Standard inner join (Informix comma-join style):
```sql
SELECT h.soh_ordref, i.soi_product
FROM informix.sohead h, informix.soitem i
WHERE h.soh_ordref = i.soi_ordref
```

Outer join (Informix-specific keyword — not ANSI syntax):
```sql
SELECT h.soh_ordref, d.sod_deldate
FROM informix.sohead h, OUTER informix.sodeliv d
WHERE h.soh_ordref = d.sod_ordref
```
Rows from `sohead` are kept even when there is no matching row in `sodeliv`.

---

## SELECT Clauses and Syntax

### Column aliases

```sql
SELECT soh_ordval AS order_value, soh_account AS account
FROM informix.sohead
-- Use AS when alias is a reserved word (YEAR, MONTH, DAY, etc.)
SELECT YEAR(soh_orddate) AS YEAR FROM informix.sohead  -- AS required here
```

### Column substrings

```sql
-- Extract characters first..last (1-based)
SELECT soh_account[1,4] FROM informix.sohead
WHERE soh_delpost[1,3] = 'B12'
```

### ORDER BY / GROUP BY with position numbers

```sql
SELECT soh_account, COUNT(*) FROM informix.sohead GROUP BY 1 ORDER BY 2
```

### UNION

```sql
SELECT soh_ordref FROM informix.sohead WHERE soh_status = 'O'
UNION ALL
SELECT sos_ordref FROM informix.sohish WHERE sos_status = 'O'
```

### INTO TEMP

Creates a temporary table from a SELECT result — useful for multi-step queries:

```sql
SELECT soh_ordref, soh_ordval INTO TEMP top_orders
FROM informix.sohead
WHERE soh_orddate >= MDY(1,1,2026)
```

Then query the temp table:
```sql
SELECT * FROM top_orders ORDER BY soh_ordval
```

Temp tables are session-scoped and dropped automatically on disconnect.

---

## Pattern Matching

```sql
-- MATCHES uses * (multi-char) and ? (single-char) wildcards
WHERE soh_account MATCHES 'SNG*'

-- LIKE uses % and _ as usual
WHERE soh_account LIKE 'SNG%'
```

---

## String Operations

```sql
-- Concatenation
SELECT soh_delname || ', ' || soh_delpost FROM informix.sohead

-- BETWEEN
WHERE soh_orddate BETWEEN MDY(1,1,2025) AND MDY(12,31,2025)
```

---

## Aggregates

Standard: `AVG`, `MAX`, `MIN`, `SUM`, `COUNT`, `COUNT(*)`

Informix extras: `RANGE` (max-min), `STDEV`, `VARIANCE`

Deduplication: `DISTINCT` and `UNIQUE` are synonymous.

```sql
SELECT soh_account, COUNT(*) AS orders, SUM(soh_ordval) AS total_value
FROM informix.sohead
WHERE YEAR(soh_orddate) = 2025
GROUP BY soh_account
ORDER BY total_value
```

---

## ODBC Scalar Functions (supported by Vision ODBC driver)

`DAYOFMONTH`, `LENGTH`, `MONTH`, `ROUND`, `TRUNCATE`, `USER`, `YEAR`

Note: These are ODBC-layer functions and only work when the ODBC translation layer
processes them (sql_syntax=2 or 3). With sql_syntax=1, use native Informix equivalents
(`DAY()`, `MONTH()`, `YEAR()`) instead.
