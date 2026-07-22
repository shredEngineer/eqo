# EQO — Epistemic Quantization of Observables

**A discrete evidence coordinate for documented observation claims.**

EQO classifies *what* was observed and grades *how well it is documented* — orthodox and heterodox cases in a single vocabulary, on six ordered axes. It assigns coordinates, never verdicts.

> **A note on the name, for physicists:** *quantization* here means discretization onto a finite lattice, in the sense used in signal processing — not quantum mechanics. An *observable* here is a documented observation, not a Hermitian operator. The borrowing is deliberate and the meaning is classical.

---

## The idea in three sentences

Every documented observation of an effect gets phenomenon leaves from a ten-class taxonomy, physical context facets, mechanism edges tagged with the role the source assigns them (`claimed` / `discussed` / `excluded_per_source`), and a six-axis epistemic coordinate: documentation, replication, controls, provenance, theory embedding, quantification. **Anomaly is a graph property, not a label** — it is the absence of a documented edge to an established mechanism, which makes it a computed fact rather than an opinion. Because the coordinate is discrete, corpora become clusterable: observations with the same evidential structure land in the same region of the lattice regardless of what was claimed.

The standard **must not** be extended with a scalar credibility score. Vectors, not verdicts. That prohibition is what lets one vocabulary carry a cold-fusion calorimetry run, a radiometer, and a documented hoax without the schema itself taking a side.

## What is here

| Path | What it is |
|------|-----------|
| `SPECIFICATION.md` | The specification — principles, the five registries, the axis definitions, the quantization module, the data model with the corpus tiers and the retraction field, governance and extension |
| `vocabulary.json` | Every registry and enumeration as one structured file — the interface for viewers, validators and build pipelines |
| `schema/` | JSON Schema (draft 2020-12) for observation records, for a corpus file, and for the vocabulary artifact |
| `GOVERNANCE.md` | How the registries grow, and how an adopting body ratifies |

Releases 1.1.0–1.3.0 shipped as addenda; version 1.4.0 consolidated them into the specification body. The release lineage lives in the repository history.

**This repository is the standard, not a dataset.** It defines how to classify and grade; it ships no corpus. That separation is deliberate — a standard carrying one particular body of records reads as that body's vehicle rather than as an instrument anyone can adopt.

A reference corpus built to this standard, together with a viewer for it, lives at [exotic-science-timeline](https://github.com/shredEngineer/exotic-science-timeline) — 207 identifiers across seven append-only releases spanning 1150 to the present, published at [timeline.advanced-rediscovery.com](https://timeline.advanced-rediscovery.com/).

## What attestation covers

Machine attestation over the shipped files covers technical integrity only — syntax validity, grammar conformance, and checksums. It does **not** certify that any claim classified with this standard is true, nor that any citation was checked against a primary source. That labour, and the authority to ratify, belong to whoever adopts the standard.

A corpus built to this standard carries its own provenance statement; this repository makes no claim about anyone's data.

## Using it

Read `SPECIFICATION.md` first — the registries and the axis semantics are short, and the worked example in the quantization module shows the payoff: one can ask *which phenomena share the same evidential situation* and *which evidential situations share the same phenomenon*, independently.

Building software against the standard? Consume `vocabulary.json` — it carries every registry and enumeration in one validated file, with anchors back to where each is defined. Parsing the specification prose is not a supported interface.

Two semantics are easy to get wrong and worth stating twice. **Unknown is never the lowest grade** — an unassessed axis is missing data, not a zero, and distance computations drop it pairwise rather than treating it as a minimum. **Theory embedding is time-indexed** — it derives from a revisable mechanism status, so an assignment records when it was computed and is recomputed when that status moves. The radiometer is the canonical case: an open anomaly in 1874, fully explained today, the same record migrating across the lattice.

## Contributing

Registries are **append-only**; identifiers are never recycled and never reinterpreted. A new phenomenon leaf needs an observable label, a delimitation from its neighbours, and at least one instance. A new mechanism node needs a status assignment with a brief rationale. A new signature needs a definition over existing registries plus instances. Private extensions use the reserved local number range or a namespaced prefix and must not appear in interchange data without a namespace declaration.

Corrections to individual records are normal governance operations, not blockers. See `GOVERNANCE.md`.

## License

Specification and schemas: **CC BY 4.0** (`LICENSE`). Code — any tooling and CI: **Apache-2.0** (`LICENSE-CODE`), which carries an explicit patent grant.

Attribute as: **Dr.-Ing. Paul Wilhelm, *EQO — Epistemic Quantization of Observables*, CC BY 4.0.** A single collective credit satisfies the attribution requirement when this specification is bundled with other material.

Attribution is not incidental here. A standard whose entire subject is the honest reporting of provenance would be inconsistent if it shed its own.
