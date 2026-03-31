# Denwire Infrastructure

## Network

- **SCO Server IP**: `192.168.1.2` (connected to Paul's datacentre via IPSec VPN to the Denwire office)
- **Portal host IP**: `10.1.1.26` (Windows server running PHP/ODBC bridge)
- **Portal port**: `8080` (planned to move to 80 in future)

---

## SCO OpenServer 5.0.6

The core legacy system runs on SCO OpenServer 5.0.6 (a Unix variant).
This hosts both the Strategix ERP application and the Informix database.

---

## IBM Informix 7.23.UC13 SE

- **Edition**: Standard Engine (SE) — not IDS/Dynamic Server
- **Database name**: `denw`
- **Location**: `/usr/informix`

### Environment variables (required for CLI access)

```bash
export INFORMIXDIR=/usr/informix
export INFORMIXSERVER=local_se
export MROOT=/usr/Strategix
export MTOOL=/usr/Strategix/db/tool/
export MTEMP=/usr/Strategix/etc
```

### Interactive SQL access

```bash
/usr/informix/bin/dbaccess denw
```

### Command-line query / data export

`dbaccess` supports positional parameters for scripted queries. Example (UNLOAD to file):

```sql
UNLOAD TO '/dbexport/pbi/adcomms.txt' DELIMITER '!' SELECT * FROM adcomms
```

### SE limitations

- No `FIRST N` or `LIMIT N` row-limiting syntax
- No cross-database queries (can only query `denw`)
- No varchar or byte data types (SE lacks these — mapped to char/NULL by ODBC driver)
- Max ODBC packet size: 64 KB

---

## Strategix ERP

- Located at `/usr/Strategix`
- Database tool directory: `/usr/Strategix/db/tool`
- Temp/config: `/usr/Strategix/etc`
- The ERP application writes to Informix directly; enhancements are layered on top
  by intercepting print streams and via ODBC from the portal

---

## Python

- Version: **2.7.18** (installed on the SCO box)
- Path: `/opt/py2718/bin/python`
- Used for any server-side scripting on SCO where needed
