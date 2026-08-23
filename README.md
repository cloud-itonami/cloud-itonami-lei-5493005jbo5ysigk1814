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
| Legal name | Phillips 66 — the live GLEIF record spells it `PHILLIPS 66` (language `en`, last updated 2026-03-09); the registry lists no other names, so the casing is the only difference between this README and the registry. |
| LEI | [5493005JBO5YSIGK1814](https://search.gleif.org/#/record/5493005JBO5YSIGK1814) (GLEIF-verified) |
| Jurisdiction | US-DE — the live GLEIF record places the entity in Delaware, registered with the Delaware Division of Corporations, Department of State (`RA000602`, file number `5063903`, OpenCorporates `us_de/5063903`, ISO 20275 legal form `XTIQ` Corporation), created 2011-11-10; legal address c/o Corporation Service Company, 251 Little Falls Drive, Wilmington, DE 19808. This README and `blueprint.edn` previously said US-TX, which is where the registry's **headquarters** address is (P.O. Box 421959, Houston, TX 77242-1959) — a different field from the jurisdiction. `facts.edn` below carries the registry's answer with provenance, and the checker flags US-TX as drift today. |
| Website | https://www.phillips66.com |
| Ticker | NYSE:PSX — a listing named here from discovery context, not read from GLEIF. GLEIF maps **8 ISINs** to this LEI (one page at the cited URL, each mirrored in `facts.edn`); which of them, if any, is the NYSE common stock, and what the others are, is not something GLEIF answers, so nothing beyond the identifiers is asserted. |
| Industry (this repo's discovery context) | ISIC 1920 Petroleum refining |

## Data

See `80-data/public/tos.journal.edn` — an EDN quad-log
`[<doc-id> :attr value <tx> :add]`. See `NOTICE` for copyright/attribution
of the archived third-party text.

- `blueprint.edn` — machine-readable company identity record.
- `facts.edn` — 25 verified registry facts with per-fact provenance (the entity,
  its securities count and the 8 identifiers behind it, issuer and issuer
  accreditation, registration authority, legal form, both parent-reporting
  exceptions, the direct-children count and the 8 children behind it).
  **Generated** — see below.
- `scripts/verify-facts.cljs` — re-fetches every source `facts.edn` cites and
  fails if the live record disagrees. Vendored from `com-junkawasaki/root`
  (`scripts/lei-verify-facts.cljs`); fix issues in the canonical and re-vendor.

## Verifying the record

The LEI claims above used to be assertions with nothing in the repository behind
them — and one of them (the jurisdiction) was wrong. `facts.edn` now carries them
as data, and every value in it was read out of a public registry response whose
URL and retrieval time sit next to the value:

```
nbb scripts/verify-facts.cljs           # check the recorded facts against the live sources
nbb scripts/verify-facts.cljs --write   # re-fetch and rewrite facts.edn
```

Eleven GLEIF/ISO requests back the file (`CHECKED 11` when it was written,
2026-08-23T09:12Z, golden copy 2026-08-23T00:00Z) — the LEI record (legal name
`PHILLIPS 66`, jurisdiction `US-DE`, entity category `GENERAL`, entity
**ACTIVE**, registration **ISSUED** since 2017-12-18 with the next renewal due
2027-04-06, last updated 2026-03-09, `FULLY_CORROBORATED`, conformity flag
`CONFORMING`, no BIC, S&P Global id `27306532`, OpenCorporates `us_de/5063903`;
entity status and registration status are different fields and are recorded
separately), its **8 ISINs** as a count read from `meta.pagination.total` of the
cited page plus one `:security` entity per identifier (the list fits in a single
page, so it is mirrored rather than only counted), its managing LOU and
LEI-issuer accreditation (Bloomberg Finance L.P., LEI `5493001KJTIIGC8Y1R12`,
accredited 2017-04-13), registration authority `RA000602` (Division of
Corporations, Department of State, Delaware), ISO 20275 legal form `XTIQ`
(`Corporation`, `US-DE`), reporting exceptions at both consolidation levels
(`NO_KNOWN_PERSON` — GLEIF's reason code for a level where no person or entity
consolidates this one, so the registry names no parent at either level; this
file records that answer and nothing about who owns this entity is asserted
here), and a measured **8 direct children**, read from `meta.pagination.total`
of the cited page, each mirrored as a `:direct-child` entity: JET Tankstellen
Austria GmbH (`AT`), WRB Refining LLC, DCP Midstream Marketing, LLC, DCP
Midstream Operating, LP and Phillips 66 Company (`US-DE`), Phillips 66
International Trading Pte. Ltd. (`SG`), Phillips 66 Canada Ltd. (`CA-AB`) and
Phillips 66 Limited (`GB`), all `ACTIVE`, all `IS_DIRECTLY_CONSOLIDATED_BY` this
entity. That is the registry's list of entities that report this LEI as their
direct accounting-consolidation parent; it is not a group chart, and a subsidiary
that holds no LEI or reports an exception does not appear in it. The
`direct-parent` and `ultimate-parent` endpoints answered `404` because GLEIF
publishes the exception side of that pair for this entity, which the checker
treats as a fact rather than a failure.

The checker's exit codes are three, not two: `0` every recorded fact matches the
live sources, `1` a citation broke or a fact drifted, `3` the check could not be
performed at all — an absent `facts.edn`, or every request failing at the
transport level. A check that could not run must not be indistinguishable from a
check that ran and found nothing, so it refuses to report a pass rather than
exiting 0. All outcomes were exercised before this landed: unmodified `0`
(`OK all 25 recorded fact(s) still match`); `:company/jurisdiction` rewritten
back to `US-TX` → `1` naming `DRIFT gleif-lei-record :company/jurisdiction`;
`:securities/isin-count` edited `8` → `9` → `1` naming
`DRIFT gleif-isins :securities/isin-count`; one `:security` entity's ISIN
rewritten → `1` naming `DRIFT gleif-isin-us718546al86 :securities/isin`; the
measured `:relationship/direct-child-count` rewritten `8` → `7` → `1` naming
`DRIFT gleif-direct-children-count`; one `:direct-child` entity deleted → `1`
naming it `ADDED` (the live registry still lists it); the direct-level
`:relationship/exception-reason` rewritten to `NON_CONSOLIDATING` → `1` naming
`DRIFT gleif-direct-parent-reporting-exception :relationship/exception-reason`;
file number `5063903` rewritten `5063904` → `1` naming the drift in
`gleif-lei-record` (`:company/registered-as` and `:company/open-corporates-id`)
and `gleif-registration-authority`; `:elf/local-name` rewritten → `1` naming
`DRIFT iso-20275-entity-legal-form :elf/local-name`; `blueprint.edn`'s
`:company/lei` edited → `1` (`facts.edn records a different :company/lei than
blueprint.edn`); the GLEIF host in the checker rewritten to an unresolvable
name → `3` (`INCONCLUSIVE could not reach GLEIF at all … refusing to report a
pass`); and with no `facts.edn` at all → `3` (`INCONCLUSIVE facts.edn is
missing or holds no facts`). Each mutation was reverted and the restored file
compared byte-for-byte against the generated one.

`facts.edn` is not yet on the shared query plane: `manifest/edn-query.cljs` in
`com-junkawasaki/root` has loaders for `blueprint.edn` and the ToS journal and
none for this file, so its datoms load here but are not joinable from
`edn-query`. The superproject's `manifest/repo-taxonomy.edn` row for this LEI
is derived from `blueprint.edn` and still says `US-TX` until it is regenerated.

## License

Repository structure: AGPL-3.0-or-later (see LICENSE). Archived third-party
ToS text: copyright Phillips 66 (see NOTICE).
