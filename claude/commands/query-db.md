The user wants you to query the Denwire Informix database.

Use the Bash tool to run curl and POST to the query tool API. Always include `sql_syntax=1` to bypass the ODBC translation layer:

```bash
curl -s -X POST "http://10.1.1.26:8080/query-tool.php?api=1" \
  --data-urlencode "sql=<SQL QUERY HERE>" \
  --data-urlencode "sql_syntax=1"
```

The API returns JSON:
```json
{ "cols": ["col1", "col2"], "rows": [{"col1": "val", ...}], "count": 42 }
```
Or on error:
```json
{ "error": "error message" }
```

Display the results as a markdown table. Show the row count. If there is an error, show it clearly.

Important notes for Informix queries:
- Table names are prefixed with schema: informix.tablename
- Use comma-join style: FROM informix.tableA a, informix.tableB b WHERE a.id = b.id
- **`ORDER BY` works** when using `sql_syntax=1`. Without it, the ODBC translation layer corrupts ORDER BY clauses causing a "Cannot open file 'sql.iem'" error.
- **`FIRST N` and `LIMIT N` do not work** — both fail with a server-side error. Informix 7.23 SE does not support these row-limiting syntaxes. To get top-N results, use a WHERE clause to filter by date/value range and rely on the result set being small, or fetch all rows and truncate client-side.
- **`sql_syntax` values:** 0=translate strict, 1=no translation (pass direct), 2=translate lenient, 3=try native then translate on error (old default). Always use 1 unless there is a specific reason not to.

### Date handling
- ODBC escape `{d 'yyyy-mm-dd'}` still works with sql_syntax=1 (processed client-side before transmission)
- Native alternatives (all confirmed working):
  - `TODAY` — current date constant
  - `MDY(month, day, year)` — construct a date, e.g. `MDY(1,1,2026)`
  - `YEAR(col)`, `MONTH(col)`, `DAY(col)`, `WEEKDAY(col)` — extract date components
  - `EXTEND(expr, YEAR TO DAY)` — truncate/extend datetime precision
- Date arithmetic: `TODAY - 365 UNITS DAY`, `soh_orddate + 30 UNITS DAY`

### Other useful Informix-specific syntax
- `MATCHES` — pattern matching like LIKE but with `*` (multi-char) and `?` (single-char) wildcards
- `||` — string concatenation operator
- `BETWEEN x AND y` — confirmed supported
- Aggregates: `AVG`, `MAX`, `MIN`, `SUM`, `COUNT`, `COUNT(*)` plus `RANGE`, `STDEV`, `VARIANCE`
- `DISTINCT` / `UNIQUE` — synonymous for deduplication in SELECT and aggregates
- `OUTER` keyword for outer joins (Informix-specific): `FROM tableA a, OUTER tableB b WHERE a.id = b.id` — rows from `tableA` are kept even if no match in `tableB`
- Column substrings: `col[first,last]` e.g. `WHERE city[1,3] = 'San'` or `SELECT name[1,20]`
- Column aliases: `SELECT expr alias` or `SELECT expr AS alias` — use `AS` when alias is a reserved word (e.g. `AS YEAR`)
- `ORDER BY` and `GROUP BY` accept position numbers: `ORDER BY 1, 2` (references 1st and 2nd SELECT columns)
- `INTO TEMP tablename` — creates a temporary table from a SELECT result: `SELECT ... INTO TEMP mytmp` — useful for multi-step top-N workarounds
- `UNION` / `UNION ALL` — confirmed supported for combining result sets
- **SE limitation**: can only query the current database (`denw`) — cross-database queries are not supported

The user's query or question is: $ARGUMENTS
