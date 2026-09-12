# Wyvern Wings

Server control plane for Wyvern Panel. Built on Pterodactyl Wings (see `NOTICE.md`).

## Status

Unmodified from upstream `v1.13.3`. This repository exists so that Wyvern-specific daemon
changes have a home when they are needed; the panel's current features ride on the stock
Wings API (`/files/pull`, `/files/decompress`, `/commands`).

## Build

```
go build -o wings wings.go
```

Requires Go 1.24+.

## Fork discipline

Same rules as the panel: upstream is merged, never rebased, and modified upstream files are
tracked in `WYVERN_TOUCHPOINTS.md`.

## License

MIT — see `LICENSE`.
