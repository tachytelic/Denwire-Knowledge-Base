# Strategix Filesystem Layout

Root: `/usr/Strategix` (`$MROOT`)

---

## Top-level hidden files

| File | Purpose |
|------|---------|
| `.license` / `.licence.no` | Current licence files |
| `.OLDlicense` / `.OLDlicence.no` | Previous licence files (kept on upgrade) |
| `.mmach` | Machine identifier |
| `.mosrel` | OS release identifier |
| `.mostype` | OS type identifier |
| `.programs` | Installed program list |
| `.release` | Strategix release version |
| `.tape` | Tape/install media reference |

---

## Directories

### `db/`
Contains `tool/` — the Strategix database tool directory (`$MTOOL`). Used by the ERP
engine for direct Informix access.

---

### `etc/`
Runtime state and configuration (`$MTEMP`). Key files:

| File / pattern | Purpose |
|----------------|---------|
| `.env_params` | Environment parameters loaded at startup |
| `.relhist` | Release history log |
| `startup` | System startup script/config |
| `autopilot` | Automated job runner config |
| `dblog` | Database activity log |
| `locks` | System-wide lock files |
| `error` | Error log |
| `hold` | Jobs/sessions on hold |
| `logs/` | General application logs |
| `printgen` | Print generation config |
| `private` | Private/sensitive config |
| `record` | Session recording |
| `termgen` | Terminal generation config |
| `ttytype`, `ttytype.sav` | Terminal type mappings |
| `TERMNAME2tty` | Terminal name to tty mapping |
| `tmp/` | Temporary files |
| `tty01`, `tty03`–`tty2A` | Per-TTY state files (physical terminals) |
| `ttyp0`–`ttyp11` | Per-TTY state files (pseudo-terminals / SSH sessions) |
| `ept221`–`ept250` | Per-process entry point files (one per active session) |

---

### `homes/`
Per-user home directories within Strategix. Each subdirectory corresponds to a user
account (identified by short code):

```
Tlsi  cloa  data  del   dloa  etc   itc   jce   lan   lsi
lyg   mngr  msa   phi   psm   pth   sfa   shi   sloa  stc   test
```

Notable accounts:
- `mngr` — manager/admin account
- `test` — test account
- `data` — likely a data/batch processing account

---

### `patches/`
Empty — no patches currently applied to this installation.

---

### `prog/`
Compiled program binaries, organised by ERP module prefix (mirrors the database module
prefixes in the `denw` database):

| Subdir | Module |
|--------|--------|
| `ad` | Address / Admin |
| `at` | ? (possibly Audit Trail) |
| `bk` | Bank |
| `cm` | Cost / Manufacturing |
| `cr` | ? (possibly Credit) |
| `cv` | ? (possibly Conversion) |
| `dl` | Debtors Ledger |
| `dm` | ? (possibly Document Management) |
| `gl` | General Ledger |
| `gr` | ? (possibly Goods Received) |
| `in` | ? (possibly Invoicing) |
| `lc` | Letters of Credit |
| `ms` | ? (possibly Master files / System) |
| `mx` | ? |
| `np` | ? (possibly Nominal/Purchase) |
| `pa` | ? (possibly Purchase Analysis) |
| `pl` | Purchase Ledger |
| `po` | Purchase Orders |
| `rp` | ? (possibly Reports) |
| `rs` | ? (possibly Reports/Sales) |
| `sa` | Sales Analysis |
| `script` | Shell scripts (system-level) |
| `so` | Sales Orders |
| `st` | Stock |
| `tx` | Tax |
| `uscript` | User-defined shell scripts |
| `util` | Utilities |

Module prefixes marked `?` are not yet confirmed — cross-reference with the database
module list in [db/README.md](../db/README.md) to fill these in.

---

### `spool/`
Print spooler directory. Contains:

- **Numbered subdirectories** (e.g. `1`–`444`, non-sequential) — individual print job
  queues, each corresponding to a printer or output destination
- `daemon.err` — print daemon error log
- `daemon_lock` — print daemon lock file
- `daemon_pipe` — print daemon IPC pipe
- `locks` — spool lock files
- `Tst20` — test spool destination
