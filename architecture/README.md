# Architecture

Global decisions: `scope: global`, binding on every governed project, numbered as
ordinary decisions (D-0xx) and never edited once accepted, only superseded.

The platform itself is NOT designed here. It lives in the AI Architecture Tower
project and its living doc:
https://claude.ai/code/artifact/336e1b53-42d4-4e95-b03b-2e96c6e03c4b

The Tower's duty toward it is fivefold: retain rather than reinvent, keep a status
line and refresh it by re-reading, enforce it on every governed app before calling a
deployment done, propagate changes when open decisions resolve, and do not freeze
today's specifics.

Current platform snapshot, as of 2026-09-20, re-read before relying on it:
Mac mini at home (not yet ordered), one Portal container as the single entry point
and app registry,each app its own Docker container behind Caddy on its own subdomain,
Cloudflare Tunnel plus Access as the public login layer, Tailscale for private admin,
one shared Postgres, Jellyfin for media, and the Portal itself installed as the PWA.
