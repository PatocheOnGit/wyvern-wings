# Wyvern Wings

The server control plane for [Wyvern Panel](https://github.com/PatocheOnGit/wyvern-panel-next):
it runs on each node, talks to Docker, and answers the panel's API.

Derived from Pelican Wings, itself derived from Pterodactyl Wings — see [`NOTICE.md`](NOTICE.md).

## Status

**The Go source is unmodified from upstream `v1.0.0-beta29`.** This repository exists for two
reasons: so that Wyvern installs pull their daemon from Wyvern's own releases rather than
someone else's, and so Wyvern-specific daemon changes have a home the day they are needed.
The panel's current features ride on the stock Wings API (`/files/pull`, `/files/decompress`,
`/commands`).

This is a personal project, published for transparency and for its own installs. There is no
support and no stability promise. If you need a daemon you can rely on, use
[Pelican](https://pelican.dev) upstream.

## Install

Don't install this by hand — [`wyvern-installer`](https://github.com/PatocheOnGit/wyvern-installer)
provisions the panel, the daemon and their dependencies in one pass. It fetches the binary from
this repository's releases and verifies it against `checksums.txt`.

Manually, on a node:

```sh
curl -fsSLo /usr/local/bin/wings \
  https://github.com/PatocheOnGit/wyvern-wings/releases/latest/download/wings_linux_amd64
chmod +x /usr/local/bin/wings
```

Use `wings_linux_arm64` on ARM.

## Build

```sh
go build -o wings -trimpath -ldflags="-s -w" github.com/pelican/wings
```

Requires Go 1.25+. The Go module path stays `github.com/pelican/wings`: renaming it would touch
every import in the tree for no functional gain, and would conflict on every upstream merge.

## Versioning

Tags are `v<upstream version>.<wyvern build>` — this release is `v1.0.0-beta29.1`, meaning
upstream `v1.0.0-beta29`, Wyvern build 1. Unlike the panel, the daemon does **not** get its own
numbering: its version is a protocol fact, read by the panel from every node and compared against
the newest release of this repository to decide whether a node is out of date. Keeping upstream's
number in the tag keeps that comparison meaningful, and the trailing build number keeps our tags
from colliding with upstream's on a clone that has both remotes.

## Fork discipline

Upstream is merged, never rebased. Any upstream file Wyvern modifies is listed in
[`WYVERN_TOUCHPOINTS.md`](WYVERN_TOUCHPOINTS.md) — every entry there is a future merge
conflict, so the list stays short.

## License

MIT — see [`LICENSE`](LICENSE) and [`NOTICE.md`](NOTICE.md).
