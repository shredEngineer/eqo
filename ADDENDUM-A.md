# EQO/1 Addendum A — Compilation Metadata & Registry Additions (Release B)
**Status: v1.1.0 · minor version per G.4 (new nodes, new patterns, one new record-level field)**

## A.1 Compilation metadata (normative for corpus releases)

A corpus record now distinguishes two things that are not the same:

- **E axes (D, R, C, P, T, Q)** — how well *the world* documented the case. `D1 P1 R0 T0` is a first-class record, not a defective one. Obscurity is never an exclusion criterion.
- **`compilation_confidence: high | medium | low`** — how reliable *the compiler's recall* of name, principals, era, and phenomenology is. This is compiler metadata, not case evidence.

Threshold for an `instances` record: name + principal(s) + rough decade + phenomenology. Everything beyond that — exact years, patent numbers, citations, measured values — appears only at high recall confidence; otherwise `x` or omission. Reconstructed citations and plausibly guessed numbers are prohibited.

**`candidates` tier:** names and leads known to the compiler only as recurring mentions in secondary compilations. Each entry carries what is recalled plus a `verify` note. Candidates are referenceable without posing as validated records — maximal inclusion without diluting the corpus.

## A.2 Registry additions (per G.1: status + rationale + instances)

**New M nodes:**

| ID | Label | Status | Rationale · instances |
|----|-------|--------|----------------------|
| M-TOR | Torsion fields | heterodox | Distinct Russian lineage (Akimov/Shipov program), not reducible to M-SCW · ex:akimov-shipov-torsion |
| M-ODK | Odic force | historical | Reichenbach's Od, ancestor of orgone-type claims · ex:reichenbach-od |
| M-ANI | Animal magnetism | historical | Mesmerism as claimed mechanism · ex:mesmer-magnetism |
| M-RDN | Radionics | heterodox | Instrument-mediated diagnosis/treatment-at-distance lineage · ex:abrams-era |
| M-ART-SUG | Suggestion/expectancy | established | Placebo, demand characteristics; artifact class missing until now · ex:franklin-commission-1784 |
| M-ART-IDE | Ideomotor movement | established | Standard account for dowsing/pendulum responses · ex:enright-reanalysis |
| M-ART-FAB | Fabricated report | established | Print/media hoaxes as documented finding · ex:kowsky-frost-1927 |

**New S patterns:**

| ID | Pattern | Definition | Canonical instances |
|----|---------|-----------|---------------------|
| S-AET | Aether drift | OPT-MED-01 ∧ absolute-motion claim (K-MOD orientation/astronomical) | Michelson–Morley (⊕ null), Miller, Marinov, Sagnac (migrated) |
| S-RDN | Radionics | (INS ∨ BIO-WRK) ∧ M-RDN edge | Abrams, Drown, de la Warr, Hieronymus |

## A.3 Promotion counters opened (per G.2)

`P-EMG-SON-01` now holds charge-quantization anomalies (ex:ehrenhaft-subelectrons); a dedicated leaf is normalized when the counter reaches ~5. Same for light-speed anisotropy currently filed under `P-OPT-MED-01`.

## A.4 Version note

The base corpus (87 records) is untouched — append-only; Release B ships as a separate file in the corpus's own repository (the standard ships no data). The registry additions above target **v1.1.0**. Ratification, corrections, and rejections of individual records are normal G.1 operations by the adopting community.
