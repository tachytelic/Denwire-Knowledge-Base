# Denwire Knowledge Base — Claude Context

This repo is the reference knowledge base for the Denwire system. It is used by
Claude Code sessions working on the DenwirePortal project and any future tooling.

---

## System at a Glance

- **Company**: Denwire Ltd, West Midlands, UK
- **ERP**: Strategix (legacy system, not modified directly)
- **Database**: IBM Informix 7.23.UC13 SE on SCO OpenServer 5.0.6 at `192.168.1.2`
- **Database name**: `denw` (271 tables — see [db/README.md](db/README.md))
- **Portal**: PHP 7.4.1 web app at `http://10.1.1.26:8080/` (stays on 7.4.1 — see [system/php-portal.md](system/php-portal.md))
- **Query API**: `POST http://10.1.1.26:8080/query-tool.php?api=1`

---

## Querying the Database

Always use `sql_syntax=1` — see [odbc/sql-syntax-notes.md](odbc/sql-syntax-notes.md) for the full story.

```bash
curl -s -X POST "http://10.1.1.26:8080/query-tool.php?api=1" \
  --data-urlencode "sql=SELECT soh_ordref, soh_orddate, soh_account FROM informix.sohead WHERE soh_orddate = (SELECT MAX(soh_orddate) FROM informix.sohead)" \
  --data-urlencode "sql_syntax=1"
```

**Critical Informix 7.23 SE limitations**:
- `FIRST N` — not supported (server-side engine limitation)
- `LIMIT N` — not supported
- `ORDER BY` — works only with `sql_syntax=1`
- Cross-database queries — not supported (SE only queries `denw`)

**Top-N workaround**: Use `MAX()`/`MIN()` subquery to find the target value, then filter with `WHERE`.

---

## Database Module Overview

Tables are grouped by two-letter prefix corresponding to ERP module:

| Prefix | Module | Key tables |
|--------|--------|------------|
| `so` | Sales Orders | sohead, soitem, soinvoice, sodeliv, sorhead |
| `sa` | Sales Analysis | saday, sacustat, sarepstat, sacuprod |
| `st` | Stock | stock, stitem, stmove, stdeliv |
| `po` | Purchase Orders | porder, poitem, podeliv, pogrn |
| `dl` | Debtors/Ledger | dlcust, dltran, dlcredtr |
| `pl` | Purchase Ledger | plsupp, pltran |
| `gl` | General Ledger | glcode, gltran, glmas |
| `bk` | Bank | bkacct, bkpaymnt, bkstan |
| `cm` | Cost/Manufacturing | cmprod, cmset, cmroute |
| `ad` | Address/Admin | adcomms, adlabel, adpcgaz |
| `lc` | Letters of Credit | lchead, lcitem |
| `tx` | Tax | txtran, txrate, txpaymnt |
| `nd` | Notes/Docs | ndmas, ndcon |

Full table lists and column definitions: [db/README.md](db/README.md), [db/modules/](db/modules/), [db/tables/](db/tables/)

---

## Key Table Relationships (Sales)

```
sohead (soh_ordref)
  ├── soitem      (soi_ordref)   — order lines
  ├── soinvoice   (soinv_ordref) — invoice header
  ├── sodeliv     (sod_ordref)   — delivery records
  ├── sopick      (sopi_ordref)  — pick list
  ├── socomm      (socom_ordref) — comments
  ├── sopay       (sopy_ordref)  — payments
  └── soaudit     (sou_ordref)   — audit trail

sorhead (sorh_retno) — returns
  └── soritem (sori_retno)

saday — denormalised invoice line fact table (best for ad-hoc sales reporting)
```

For full SO table relationships see [db/modules/SO-Tables.md](db/modules/SO-Tables.md).
For SA (Sales Analysis) tables see [db/modules/SA-Tables.md](db/modules/SA-Tables.md).

---

## Important Query Patterns

```sql
-- Most recent orders (no FIRST/LIMIT — use date filter)
SELECT soh_ordref, soh_orddate, soh_account, soh_ordval
FROM informix.sohead
WHERE soh_orddate = (SELECT MAX(soh_orddate) FROM informix.sohead)

-- Sales for an account in a date range
SELECT sad_ordref, sad_docdat, sad_product, sad_qty, sad_value
FROM informix.saday
WHERE sad_account = 'SNG001'
  AND sad_docdat >= MDY(1,1,2025)
  AND sad_icflag = 'I'
ORDER BY sad_docdat

-- Customer transaction history (lightweight)
SELECT sac_product, sac_qty, sac_price, sac_idate
FROM informix.sacuprod
WHERE sac_customer = 'SNG001'
ORDER BY sac_idate
```

---

## Portal & Infrastructure

- PHP portal runs on the Windows host at `10.1.1.26`, proxying to Informix on `192.168.1.2` via SCO Vision ODBC
- Do not upgrade PHP past 7.4.1 — breaks ODBC
- Direct Informix access: `dbaccess denw` on the SCO box (see [system/infrastructure.md](system/infrastructure.md))

---

## Files in This Repo

```
CLAUDE.md                      ← this file (auto-loaded by Claude Code)
system/
  infrastructure.md            ← SCO server, Informix env vars, Python, dbaccess
  php-portal.md                ← PHP 7.4.1, portal architecture, ODBC connection
db/
  README.md                    ← full table list, module prefix guide
  relationships.md             ← cross-module table relationships
  modules/
    SO-Tables.md               ← all 32 SO-prefix tables with columns
    SA-Tables.md               ← all SA-prefix tables with columns
  tables/                      ← raw column definitions (one .txt per table)
odbc/
  sql-syntax-notes.md          ← Informix SQL quirks, workarounds, date handling
  vision-odbc-reference.md     ← full SCO Vision ODBC driver reference
claude/
  commands/
    query-db.md                ← Claude Code skill for querying the database
```
