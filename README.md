# Denwire Knowledge Base

Reference knowledge base for the Denwire legacy ERP system and portal.

This repo captures everything needed to work with the Denwire system — database schema,
query patterns, ODBC configuration, infrastructure details, and Claude Code tooling.

## Quick Start

If you're using Claude Code, add this repo as context in your project's `CLAUDE.md`:

```
See the denwire-knowledge-base repo for full schema and query reference.
```

Or clone it alongside your project and point Claude at it directly.

## Contents

| Path | Description |
|------|-------------|
| [CLAUDE.md](CLAUDE.md) | Auto-loaded Claude Code context — start here |
| [system/infrastructure.md](system/infrastructure.md) | SCO server, Informix, env vars, Python |
| [system/php-portal.md](system/php-portal.md) | PHP 7.4.1 portal, ODBC bridge, API |
| [db/README.md](db/README.md) | Full table list grouped by module |
| [db/modules/SO-Tables.md](db/modules/SO-Tables.md) | All 32 Sales Order tables with columns |
| [db/modules/SA-Tables.md](db/modules/SA-Tables.md) | Sales Analysis tables with columns |
| [db/tables/](db/tables/) | Raw column definitions (one .txt per table, 248 tables) |
| [odbc/sql-syntax-notes.md](odbc/sql-syntax-notes.md) | Informix SQL quirks, workarounds, date handling |
| [odbc/vision-odbc-reference.md](odbc/vision-odbc-reference.md) | SCO Vision ODBC driver full reference |
| [claude/commands/query-db.md](claude/commands/query-db.md) | Claude Code /query-db skill |

## System Overview

- **ERP**: Strategix (legacy, not modified directly)
- **Database**: IBM Informix 7.23.UC13 SE on SCO OpenServer 5.0.6
- **Portal**: PHP 7.4.1 at `http://10.1.1.26:8080/`
- **Access method**: SCO Vision ODBC driver (Windows → SCO TCP)

## Using the Claude Skill

Copy `claude/commands/query-db.md` into your project's `.claude/commands/` directory
to enable the `/query-db` slash command in Claude Code sessions.
