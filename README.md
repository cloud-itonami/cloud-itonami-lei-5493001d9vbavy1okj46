# cloud-itonami-lei-5493001d9vbavy1okj46

> **Independent third-party archive/analysis. Not affiliated with, endorsed by, or sponsored by Cumulus Media New Holdings Inc..**

This repository archives publicly published legal/policy documents of
**Cumulus Media New Holdings Inc.**, with source-url and retrieval-date provenance, per
[ADR-2607110300](https://github.com/com-junkawasaki/root/blob/main/90-docs/adr/2607110300-cloud-itonami-lei-corporate-tos-catalog.md)
(`cloud-itonami-lei-corporate-tos-catalog`, `com-junkawasaki/root`). It is a read-only
reference/archive repository — it does not act, propose, or execute anything on the
company's behalf, and is not a governed Advisor/Governor actor.

## Company identity

- **Legal name**: Cumulus Media New Holdings Inc. (GLEIF records it in that form, language `en`)
- **LEI (ISO 17442)**: [5493001D9VBAVY1OKJ46](https://search.gleif.org/#/record/5493001D9VBAVY1OKJ46) (GLEIF-verified)
- **Jurisdiction**: `US-DE` — a Delaware corporation (ISO 20275 legal form `XTIQ`, `Corporation`),
  file number `6837084` at the Division of Corporations, Delaware Department of State
  (`RA000602`). GLEIF's legal address and headquarters address are the same registered-agent
  address (c/o Corporation Service Company, 251 Little Falls Drive, Wilmington 19808), not an
  operating office. `facts.edn` below carries the registry's answer with provenance.
- **Website**: https://www.cumulusmedia.com — the group site, named here from discovery
  context; GLEIF records no website for the entity.
- **Registration status**: the LEI registration is **`LAPSED`** as of the retrieval below
  (next renewal was due 2026-05-31 and the record was last updated 2026-05-30), with
  conformity flag `NON_CONFORMING`, while the entity itself is `ACTIVE`. These are two
  different fields: a live company can hold a lapsed LEI. Nothing here interprets why.

## Contents

- `80-data/public/tos.journal.edn` — EDN quad-log of archived documents, each entry
  carrying `:tos/full-text`, `:tos/source-url`, `:tos/retrieved-at`, `:tos/sha256`,
  `:tos/doc-type`, and a `:tos/supersedes` chain for future revisions.
- `80-data/public/site.journal.edn` — official-website enrichment (title / description /
  reachability) recorded with the same provenance shape.
- `NOTICE` — copyright/attribution statement for the archived third-party text.
- `blueprint.edn` — machine-readable company identity record.
- `facts.edn` — 13 verified registry facts with per-fact provenance (the entity, its
  securities count and the 4 ISINs behind it, issuer and issuer accreditation, registration
  authority, legal form, both parent-reporting exceptions, and the direct-children count).
  **Generated** — see below.
- `scripts/verify-facts.cljk` — re-fetches every source `facts.edn` cites and fails if
  the live record disagrees. Vendored from `com-junkawasaki/root`
  (`scripts/lei-verify-facts.cljs`); fix issues in the canonical and re-vendor.

## Verifying the record

The LEI claims above used to be assertions with nothing in the repository behind them.
`facts.edn` now carries them as data, and every value in it was read out of a public
registry response whose URL and retrieval time sit next to the value:

```
kbb --backend sci scripts/verify-facts.cljk           # check the recorded facts against the live sources
kbb --backend sci scripts/verify-facts.cljk --write   # re-fetch and rewrite facts.edn
```

Eleven GLEIF/ISO requests back the file (`CHECKED 11` when it was written,
2026-08-23T11:44Z, golden copy 2026-08-23T00:00Z) — the LEI record (legal name `Cumulus
Media New Holdings Inc.`, jurisdiction `US-DE`, entity category `GENERAL`, entity
**ACTIVE**, registration **LAPSED** — initially registered 2019-05-14, last updated
2026-05-30, next renewal date 2026-05-31, `FULLY_CORROBORATED`, conformity flag
`NON_CONFORMING`; no BIC; OpenCorporates id `us_de/6837084`, S&P Global id `568754937`;
entity creation date recorded by the registry as `2018-04-08T22:00:00Z`), its **4 ISINs**
as a count read from `meta.pagination.total` of the cited page (one page of 15 — the whole
list fits, so each identifier is also mirrored as its own `:security` entity:
`USU1269CAB01`, `USU1269CAA28`, `US23110AAA43`, `US23110AAB26`; GLEIF's ISIN mapping does
not say what kind of instrument each is, and nothing here claims a listed share line for
this entity), its managing LOU and LEI-issuer accreditation (WM Datenservice —
Herausgebergemeinschaft Wertpapier-Mitteilungen Keppler, Lehmann GmbH & Co. KG, `DE`, LEI
`5299000J2N45DDNE4Y28`, accredited 2017-04-13), registration authority `RA000602`
(Division of Corporations, Department of State, Delaware, United States of America), ISO
20275 legal form `XTIQ` (`Corporation`, `US-DE`, status `ACTV`), reporting exceptions at
both consolidation levels (`NON_CONSOLIDATING` — GLEIF's reason code for an entity that
reports it is not consolidated into a parent's accounts under the applicable accounting
standard; this file records that answer, and nothing about who owns this entity is
asserted here), and a measured **0 direct children**, read from `meta.pagination.total`
of the cited page. That zero is the registry's list of entities that report this LEI as
their direct accounting-consolidation parent; it is not a group chart, and a subsidiary
that holds no LEI or reports an exception does not appear in it — so it is not evidence
that this entity has no subsidiaries. The `direct-parent` and `ultimate-parent`
endpoints answered `404` because GLEIF publishes the exception side of that pair for this
entity, which the checker treats as a fact rather than a failure.

The checker's exit codes are three, not two: `0` every recorded fact matches the live
sources, `1` a citation broke or a fact drifted, `3` the check could not be performed at
all — an absent `facts.edn`, or every request failing at the transport level. A check
that could not run must not be indistinguishable from a check that ran and found
nothing, so it refuses to report a pass rather than exiting 0. All outcomes were
exercised before this landed, each mutation confirmed to have changed the file by a byte
comparison before the run and reverted byte-for-byte after it: unmodified `0` (`OK all 13
recorded fact(s) still match`); `:company/jurisdiction` rewritten to `DE` → `1` naming
`DRIFT gleif-lei-record :company/jurisdiction`; `:securities/isin-count` edited `4` → `5`
→ `1` naming `DRIFT gleif-isins :securities/isin-count`; the measured
`:relationship/direct-child-count` rewritten `0` → `1` → `1` naming `DRIFT
gleif-direct-children-count`; the mirrored `US23110AAB26` `:security` entity deleted →
`1` naming it `ADDED` (the live registry still lists it); both levels'
`:relationship/exception-reason` rewritten to `NO_KNOWN_PERSON` → `1` naming the drift in
both `gleif-direct-parent-reporting-exception` and
`gleif-ultimate-parent-reporting-exception`; file number `6837084` rewritten `6837085` →
`1` naming the drift in `gleif-lei-record` and `gleif-registration-authority`;
`:elf/local-name` rewritten → `1` naming `DRIFT iso-20275-entity-legal-form
:elf/local-name`; `:registration/status` rewritten `LAPSED` → `ISSUED` → `1` naming
`DRIFT gleif-lei-record :registration/status`; `blueprint.edn`'s `:company/lei` edited →
`1` (`facts.edn records a different :company/lei than blueprint.edn`); the GLEIF host in
the checker rewritten to an unresolvable name → `3` (`INCONCLUSIVE could not reach GLEIF
at all … refusing to report a pass`); and with no `facts.edn` at all → `3` (`INCONCLUSIVE
facts.edn is missing or holds no facts`). Independently of the checker, each of the 9
distinct URLs `facts.edn` cites was fetched with `curl` and answered `200`.

`facts.edn` is not yet on the shared query plane: `manifest/edn-query.cljs` in
`com-junkawasaki/root` has loaders for `blueprint.edn` and the ToS journal and none for
this file, so its datoms load here but are not joinable from `edn-query`.

## Design rationale

See ADR-2607110300 in `com-junkawasaki/root` (`90-docs/adr/`) for why this repo exists,
why it is keyed by LEI rather than GTIN or ticker, and why full-text archival (with
provenance) was chosen over excerpt-only storage.
