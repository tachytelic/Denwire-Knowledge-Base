# SCO Vision ODBC Driver Reference

Full reference for the SCO Vision ODBC driver used to connect from the Windows PHP
portal to IBM Informix on SCO OpenServer.

---

## Connection String Parameters

| Parameter | Values / Default | Description |
|-----------|-----------------|-------------|
| `DRIVER` | `{SCO Vision ODBC}` | Driver name |
| `DSN` | string | Data source name (omit to use connection string directly) |
| `UID` / `PWD` | string | Login credentials |
| `Hostname` | string | Hostname or IP of the SCO server |
| `ServerID` | `Informix` | Database type |
| `DBname` | string | Database name (e.g. `denw`) |
| `DBuser` / `DBauth` | string | DBMS-level credentials |
| `ReadOnly` | `0`/`1` (default 0) | Open data source read-only |
| `CacheMemory` | Kbytes (max 64, default 32) | Fetch cache size |
| `CacheRows` | num (default 0 = disabled) | Cache size in rows (set CacheMemory=0 to use this) |
| `CacheIdle` | ms (default 100) | Wait time before refilling cache |
| `FetchCache` | `0`/`1` (default 1) | Enable/disable caching |
| `VirtualServer` | `0`/`1` (default 0) | Single real connection per app (read-only only) |
| `Timeout` | minutes (default 0 = none) | Idle timeout before server exits |
| `QueryTimeout` | seconds (default 0 = none) | Query execution timeout |
| `Port` | num | Port override (bypasses RPC portmapper) |
| `TCPOptions` | `0`/`1`/`2`/`3` (default 1) | TCP_NODELAY and keepalive options |

---

## SQLSyntax Parameter

Controls how ODBC SQL grammar is translated to native Informix SQL.

| Value | Behaviour |
|-------|-----------|
| `0` | Translate to native SQL (strict — error on non-ODBC syntax) |
| `1` | **No translation — SQL passed directly to DBMS** ← recommended |
| `2` | Translate to native SQL (lenient — passes non-ODBC syntax through) |
| `3` | Try native first, translate on error if DBMS returns error ← **avoid** |

**Default is 3.** Always override to 1 for Informix queries.
Mode 3 causes double round-trips and corrupts `ORDER BY` clauses.

---

## ServerOptions Flags

Decimal values — add together for combined options.

| Value | Description |
|-------|-------------|
| `0` | None |
| `1` | Allow write access to tables when using Microsoft Access (default) |
| `4` | Use owner names in catalog functions |
| `8` | Hold cursor support enabled |
| `16` | **Disable** support for expressions in `ORDER BY` |
| `32` | Hold commit requests until all transactions complete (autocommit) |
| `64` | Disable reporting Informix DECIMAL precision as 15 (report as 16 instead) |
| `128` | Disable reporting of Ingres hash/isam/btree indices |
| `256` | Enclose owner names in quotes during SQL processing |
| `512` | Disable reporting period `.` as qualifier name separator |
| `32768` | Enable MS Access to perform local/remote table joins more efficiently |

---

## Debug Options

Enable debug by setting `DebugOptions` to the sum of desired values:

| Value | Captures |
|-------|---------|
| `0` | No debug |
| `1` | Connect/disconnect/free |
| `2` | GetInfo/GetTypeInfo |
| `4` | Connect/statement options |
| `8` | Prepare/cursor/params |
| `16` | Execute/ExecDirect/NativeSQL |
| `32` | Fetch/bind/rowcount |
| `64` | Catalog functions (columns, tables, etc.) |
| `256` | Host-end datatype conversion |
| `512` | Host-end SQL syntax translation |

Default log paths:
- PC: `C:\Vwodbc.txt`
- Host: `~/vwodbc.log`

Override with `DebugPCFile` and `DebugHostFile`.

---

## ODBC to Informix Data Type Mapping

### ODBC → Informix (for parameterised queries)

| ODBC Type | Informix Type |
|-----------|--------------|
| SQL_CHAR | char |
| SQL_VARCHAR | varchar (char on SE) |
| SQL_DECIMAL | decimal |
| SQL_NUMERIC | numeric |
| SQL_SMALLINT | smallint |
| SQL_INTEGER | integer |
| SQL_REAL | smallfloat |
| SQL_FLOAT / SQL_DOUBLE | float |
| SQL_LONGVARCHAR | varchar (char on SE) |
| SQL_BIT / SQL_TINYINT | smallint |
| SQL_BIGINT | decimal |
| SQL_DATE | date |
| SQL_TIME | datetime (hour to second) |
| SQL_TIMESTAMP | datetime |

Note: SE does not have `varchar` or `byte` — mapped to `char` and `NULL` respectively.

### Informix → ODBC (for result sets)

| Informix Type | ODBC Type |
|--------------|-----------|
| char | SQL_CHAR |
| varchar | SQL_VARCHAR |
| smallint | SQL_SMALLINT |
| integer | SQL_INTEGER |
| smallfloat | SQL_REAL |
| float | SQL_DOUBLE |
| decimal / money | SQL_DECIMAL |
| serial | SQL_INTEGER |
| date | SQL_DATE |
| datetime | SQL_TIMESTAMP |
| datetime (hour to second) | SQL_TIME |
| interval | SQL_VARCHAR |

---

## Datetime Mapping Note

When mapping Informix `datetime` to `SQL_TIMESTAMP`, unused fields are filled with
lowest allowed values: year=0000, month/day=01, hours/minutes/seconds=00.

Example: `01:30` → `0000-01-01 01:30:00.000000000`

---

## DECIMAL Precision Note

Informix DECIMAL default precision is 16, but ODBC spec recommends max 15.
The driver reports DECIMAL precision as 15 by default, which can cause some apps
to map DECIMAL columns to character columns (breaking aggregates).

To disable this behaviour, add `64` to the `ServerOptions` value.

---

## Scalar Functions Supported

`DAYOFMONTH`, `LENGTH`, `MONTH`, `ROUND`, `TRUNCATE`, `USER`, `YEAR`

These are processed by the ODBC translation layer and only work with
`SQLSyntax=2` or `SQLSyntax=3`. With `SQLSyntax=1`, use native Informix
equivalents (`DAY()`, `MONTH()`, `YEAR()`).

---

## Host-Side Files

| Path | Purpose |
|------|---------|
| `/usr/local/vision/bin/sqlr.inf40.d` | ODBC server program for Informix |
| `/usr/local/vision/sqlrrm.inf` | Removal script |
| `/usr/local/vision/etc/infsqld.conf` | Environment config (sets INFORMIXDIR, SQLEXEC etc.) |

The `infsqld.conf` file can also be placed in the user's login directory
as `.infsqld.conf` for per-user overrides.

---

## Error Message Format

```
[vendor][ODBC-component][data-source] error-message
```

Example from Informix:
```
[SCO Vision][ODBC Driver][Informix] Cannot open file 'sql.iem'
```

The `sql.iem` error typically means the Informix engine received SQL syntax it
cannot parse — usually caused by using SQLSyntax=3 with ORDER BY, or using
FIRST/LIMIT which are not supported by Informix 7.23 SE.
