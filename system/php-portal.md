# Denwire Portal — PHP & ODBC

## Overview

The portal is a PHP web application running on a Windows server at `10.1.1.26:8080`.
It acts as an ODBC bridge between external tools/web interfaces and the Informix database
on the SCO box at `192.168.1.2`.

Enhancements to the legacy Strategix ERP are built in two ways:
1. **Print-stream interception** — manipulating the output originally bound for plain text printers
2. **ODBC database access** — direct SQL queries via the portal's query API

---

## PHP Version

**PHP 7.4.1 — do not upgrade.**

A newer PHP version was tested and broke ODBC connectivity. The version is deliberately
pinned at 7.4.1 to retain the `php_odbc` extension functionality.

---

## ODBC Connection

Driver: **SCO Vision ODBC** (connects from Windows to Informix on SCO over TCP)

Base connection string (from `php/db-config.php`):
```
DRIVER={SCO Vision ODBC};DBname=denw;ServerID=Informix;Hostname=192.168.1.2;ReadOnly=1;CacheMemory=64
```

**Always append `SQLSyntax=1`** when executing queries — see [odbc/sql-syntax-notes.md](../odbc/sql-syntax-notes.md).

Credentials: stored in `php/db-config.php` (not committed to this repo).

---

## Query API

**Endpoint**: `POST http://10.1.1.26:8080/query-tool.php?api=1`

**Parameters** (POST body, URL-encoded):
- `sql` — the SQL query
- `sql_syntax` — SQLSyntax value (always use `1`)

**Response** (JSON):
```json
{ "cols": ["col1", "col2"], "rows": [{"col1": "val"}], "count": 42 }
```
or on error:
```json
{ "error": "error message" }
```

**Example curl**:
```bash
curl -s -X POST "http://10.1.1.26:8080/query-tool.php?api=1" \
  --data-urlencode "sql=SELECT soh_ordref FROM informix.sohead WHERE soh_orddate = TODAY" \
  --data-urlencode "sql_syntax=1"
```

---

## Portal URL

- Main portal: `http://10.1.1.26:8080/`
- Query tool (browser UI): `http://10.1.1.26:8080/query-tool.php`
- Query tool (API): `http://10.1.1.26:8080/query-tool.php?api=1`

Note: Port 8080 is current; may move to port 80 in future.
