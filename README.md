# cloud-itonami-lei-5493005jbo5ysigk1814

**独立した第三者による分析/アーカイブであり、Phillips 66 と提携・後援関係にありません。**
This is an independent third-party archive/analysis. Not affiliated with,
endorsed by, or sponsored by Phillips 66.

## What this is

A per-company reference/archive repository in the `cloud-itonami-lei-*`
family (ADR-2607110300, [com-junkawasaki/root design
rationale](https://github.com/com-junkawasaki/root/blob/main/90-docs/adr/2607110300-cloud-itonami-lei-corporate-tos-catalog.md)).
It archives Phillips 66's publicly published Terms of Service / Terms of Use
text, keyed by the company's ISO 17442 Legal Entity Identifier (LEI), with
full source-url + retrieved-at + sha256 provenance for every entry so the
document's revision history can be tracked over time via git history.

This is a **read-only reference/archive**, not an Advisor⊣Governor actuation
actor — it proposes or executes nothing on Phillips 66's behalf.

## Company identity

| Field | Value |
|---|---|
| Legal name | Phillips 66 |
| LEI | [5493005JBO5YSIGK1814](https://search.gleif.org/#/record/5493005JBO5YSIGK1814) |
| Jurisdiction | US-TX |
| Website | https://www.phillips66.com |
| Ticker | NYSE:PSX |
| Industry (this repo's discovery context) | ISIC 1920 Petroleum refining |

## Data

See `80-data/public/tos.journal.edn` — an EDN quad-log
`[<doc-id> :attr value <tx> :add]`. See `NOTICE` for copyright/attribution
of the archived third-party text.

## License

Repository structure: AGPL-3.0-or-later (see LICENSE). Archived third-party
ToS text: copyright Phillips 66 (see NOTICE).
