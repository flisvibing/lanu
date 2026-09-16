# Lanu

> **Coming soon.**

Lanu is a minimalist, self-hosted, high-performance embedded database engine written in Rust. No artificial limits, no SQL parsing overhead, no JSON bloat — just raw binary speed with zero-knowledge encryption.

## Why Lanu?

- **Fast** — Raw binary storage format. No text parsing, no JSON overhead.
- **Unlimited** — No product-imposed data caps. The only limit is your own disk.
- **Open source** — MIT licensed, fully self-hosted, no vendor lock-in.
- **Zero-knowledge encryption** — AES-256-GCM at the record level. Your data is unreadable without your key — including to you, without it.
- **Minimal** — Built with a small, audited dependency footprint. No ORM, no unnecessary abstraction.

## How it works

Lanu splits each table horizontally into 500 MB chunks (`.ln` files). Each chunk has a paired offset index (`.idx`) for O(1)-style row lookups via byte-seeking, so nothing needs to be scanned or fully decrypted to answer a query. Schema changes are lazy — adding a column never rewrites existing data. Deletes are tombstoned and reclaimed later through background compaction, which never blocks readers.

Lanu runs as a standalone server process. Applications, websites, and games never touch the database files directly — everything goes through a gRPC API secured with mutual TLS (mTLS).

## Ecosystem

| Tool | Purpose |
|---|---|
| `lanu` | The core embedded storage engine |
| `lanu-dbx` | Read-only interactive CLI for inspecting `.lnf` database archives |

`.lnf` files package an entire database (all `.ln` chunks, `.idx` files, and metadata) into a single archive for backup, transport, and inspection.

## Status

Lanu is currently in active architecture and development. Not yet ready for production use — star/watch the repo to follow progress.

## License

MIT
