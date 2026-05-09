# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Repo Is

A curated DNS allowlist/blocklist for [AdGuard Home](https://adguard.com/en/adguard-home/overview.html). There is no build system, no scripting, and no tests — this is purely a collection of plain-text rule files.

The list is privacy- and security-focused, with an Australian-user perspective. Apple products, social media, most shopping sites, ads, trackers, and telemetry are intentionally not whitelisted.

## Rule Syntax

All files use **AdGuard/Adblock-style syntax** (requires AdGuard Home v0.107.36+):

- `@@|example.com^$important` — allowlist (whitelist) a domain
- `||example.com^$important` — blocklist a domain
- `||*^$important` — block everything (used in `base.txt` as the catch-all block rule)
- Wildcards: `@@|*-*.example.com^$important`
- Comments: lines starting with `#`

Reference: https://github.com/AdguardTeam/AdGuardHome/wiki/Hosts-Blocklists

## File Structure

| File | Purpose |
|------|---------|
| `base.txt` | Blocklist — the catch-all `||*^$important` rule plus a small set of explicit blocks/allows |
| `whitelist.txt` | Full allowlist (~5800+ rules) — all modules combined into one file |
| `whitelist_slim.txt` | Slim allowlist — core rules only, intended to be paired with individual modules |
| `dns_disallowed_domains.txt` | Domains to add to AdGuard's "Disallowed domains" to suppress query log noise |
| `upstream_dns_servers.txt` | Recommended upstream DNS server URLs (Cloudflare security) |
| `Modules/` | Optional per-category allowlist files for modular usage |

### Module Categories

`Modules/` is organized into subdirectories: `Apps/`, `Countries/`, `Entertainment/`, `Managers/`, `Media/`, `Organizations/`, `Research/`, `Shopping/`, `Tech/`, `Testing/`, `Torrents_and_Usenet/`.

`Testing/` contains experimental or archived rules not ready for production use.

## How Users Consume This

**Standard mode**: Add `base.txt` as a blocklist and `whitelist.txt` as an allowlist in AdGuard Home.

**Modular mode**: Add `base.txt` as a blocklist and `whitelist_slim.txt` as an allowlist, then add individual `Modules/*.txt` files as additional allowlists.

## Editing Guidelines

- When adding domains to `whitelist.txt`, also add them to the relevant `Modules/` file (and `whitelist_slim.txt` if core enough).
- Keep entries sorted alphabetically within each file where possible.
- Commented-out rules (e.g., `# @@|domain^$important`) indicate intentionally excluded domains — include a note explaining why.
- The `$important` modifier is used on all rules so they take priority over other filter lists.
