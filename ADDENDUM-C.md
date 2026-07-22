# EQO/1 Addendum C — Machine-Readable Vocabulary, Registry Addition, Conformance Clarifications
**Status: v1.3.0 · minor version per G.4 (one new normative artifact, one M node, three clarifications)**

## C.1 The vocabulary artifact (normative)

The standard now ships `vocabulary.json`: every registry and enumeration — phenomenon classes and leaves, mechanism nodes with status, context facets and their value tokens, the six axes with grade labels, epistemotypes with their regions, signatures, edge roles, relation types, record kinds, compilation-confidence levels, and the specification anchors where each is defined — in one structured file, validated by `schema/vocabulary.schema.json`.

The artifact also carries the mechanically evaluable rules as data, under `derivation_rules`: the theory-embedding derivation table (edge status × role → grade, aggregated by maximum, with the no-edge grade and the orthodox-anchor convention), the two derived signatures (`S-OFN` at T0, `S-DEK` at T4), and the two exact epistemotype boundaries of §C.3. A validator interprets this table instead of re-transcribing the prose into code — the prose in Part V and §Q.4 remains the human-readable authority the table must match. Signature *compositions* (Part VI) stay prose: they are tagged by judgment, not derived, and encoding them would buy an expression language for nothing.

The rule this creates: **a consumer reads the artifact, never the prose.** A viewer, validator, or build pipeline that needs the vocabulary consumes `vocabulary.json`; parsing `SPECIFICATION.md` text is not a supported interface, because prose changes on a patch while the artifact carries the contract. Where artifact and prose disagree, that is a defect in this repository — CI cross-checks the artifact against the schemas on every push, and the specification remains the human-readable authority the artifact is generated to match.

Adopters pin the artifact exactly as they pin the standard: by version and checksum. A consumer working from a vendored copy records the version it was taken at.

## C.2 Registry addition (per G.1)

| ID | Label | Status | Rationale · instances |
|----|-------|--------|----------------------|
| M-REL | Relativistic kinematics (special/general relativity) | established | The corpus resolves rotation-interferometry and clock-rate claims into relativity; the registry had classical mechanics (M-MCH) but no relativistic node, leaving records like the Sagnac interferometer without an established edge to carry their modern explanation · ex:sagnac-1913 |

## C.3 Conformance clarifications

**Record-level `eqo_version` is satisfied at file level.** §5 requires every observation to carry `eqo_version`. A corpus release file that declares its version once — `eqo_version` or `targets_eqo_version` at the top of the file — satisfies this requirement for every record it contains; a record-level value, where present, overrides the file-level one. This writes down what corpus releases already practice, so that per-record repetition of an identical value is not required for conformance.

**Epistemotype constraints are checkable.** The reference regions of §Q.4 are informal and may overlap; assignment within them is judgment. Two boundaries, however, are exact, and an implementation MAY enforce them mechanically: `EP-0` applies only to records with three or more axes at `x` (an assessed record is never "unquantized"), and `EP-5` requires `T4` ("covered means claimed"). A record violating either carries a wrong assignment, not a defensible one.

**T recomputation at release level.** §Q.6.3 requires `t_computed_at` so that theory embedding stays auditable against mechanism-status revisions. A corpus release that recomputes T for all records at release time MAY record this once, in the release provenance note, rather than per record.

## C.4 Version note

Registries untouched except for M-REL. Ships as v1.3.0 alongside the merged package; ratification and corrections remain normal G.1 operations by the adopting community.
