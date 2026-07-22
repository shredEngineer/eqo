# EQO/1 Addendum D — Reading Notes & Proposed Extensions
**Status: advisory draft — non-normative. No registry, grammar, axis, or schema change; nothing here alters conformance. Candidate content for a future minor release under G.4, subject to the GOVERNANCE.md process.**

## D.1 Reading note: the R axis grades documentation of replication activity, not replication success

Adopters grading real records reliably stumble on one cell: `R3` (*independently attempted, not reproduced*) ranks **above** `R2` (*repeated, same experimenter*). Read as a credence scale that looks inverted — a failed independent replication seems like it should count *against* a claim, not upgrade it.

The axis is behaving as designed, and the design is worth stating explicitly: **R grades how thoroughly the replication question is documented, not how it came out.** A claim that independent hands have actually attempted occupies a better-documented evidential situation than one only its originator ever repeated — the record now contains independent apparatus, independent competence, and an outcome, whichever way it went. The *direction* of that outcome is carried elsewhere: by the replication attempt's own record and its `contradicts`/`replicates`/`confirms_per_source` edge (E-R note, SPECIFICATION § axes: "replication attempts are their own observations").

Practical rule for compilers: assign R from the *documented activity*; let the *edges* say what the activity found. If assigning a grade feels like passing a verdict, the verdict part belongs in a relation, not in the coordinate.

## D.2 Proposed extension: encoding retraction

The 2020s superconductivity episodes (retracted journal claims with the retraction notice as the decisive public document) expose a gap: **retraction is a documented, dated event of a distinctive class, and the standard currently has no first-class slot for it.** Today it can only be carried in `note` prose and in the citation list — invisible to any machine consumer.

Proposed for community consideration (one of, not all):

1. **Optional record field** `retractions: [{date: <ISO date>, ref: <citation>}]` — the minimal, append-only-friendly form; the retraction notice becomes citable data. Schema addition, minor version.
2. **Derived signature** `S-RET` — derivable only if option 1 (or an equivalent field) exists; a signature without a field would reintroduce hand-set derived values, which Addendum A's T-axis lesson argues against.
3. **Status quo** — leave retraction in `note` + `refs`, on the argument that a retraction is an examination like any other and belongs in a linked examination record. The counter-argument: a retraction is issued by the *publication channel*, not by an examining party, and self-retraction by an author list has no natural second record to live in.

The compilers' current practice (pending a decision): retraction date, issuing party, and the notice's stated grounds go verbatim-faithful into `note`; the retraction notice itself is a `refs` entry. Records of this class in the reference corpus: `ex:dias-csh-2020`, `ex:dias-luh-2023`.

## D.3 Reading note: `record_kind` coverage is intentionally sparse

`record_kind` (Addendum B.2) defaults to `observation`; compilers set it only where the distinction carries information (a design that was never built, a demonstration without instruments, an analysis of others' claims). Absence of the field is the default, not an omission.
