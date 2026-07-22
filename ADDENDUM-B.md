# EQO/1 Addendum B — Doctrine & Narrative Tiers, record_kind, Attestation Semantics
**Status: v1.2.0 "Unification Release" · minor version per G.4 (new tiers, one M node, one record field)**

## B.1 Why two new tiers

The mandate is unified referenceability: theory and practice, documented or not, hoaxes and conspiracy narratives included. The observable-primacy principle (Principle 1) stays untouched — theories and narratives are not observations and MUST NOT pose as observation records. They become referenceable as **their own object types**:

- **`doctrines`** — theory-first corpora (a body of claims about how the world works, without or beyond a bench-observation corpus). Fields: `id (doc:*)`, `label`, `principals`, `years`, `summary`, `linked_instances` (observation records that cite the doctrine, if any), `compilation_confidence`, `note`.
- **`narratives`** — lore and conspiracy complexes. Fields: `id (nar:*)`, `label`, `emergence` (when the *narrative* first appears), `narrative_provenance` (its documentation trail — the EQO move: a narrative is itself a documented textual phenomenon with D/P-like provenance), **`factual_kernel`** (what is independently documented), **`lore_layer`** (what the narrative adds), `linked_instances`, `compilation_confidence`.

The kernel/lore split is the epistemic core of this tier: it lets the community reference a conspiracy theory precisely — affirming its existence and its documented seed while cleanly delimiting the undocumented growth. Indexing a narrative is not endorsing it, exactly as indexing an observation was never a truth verdict.

**Hoaxes** need no new tier: a documented hoax is an observation record whose resolution edge is `M-ART-FAB` or `M-ART-AUF` `claimed` — see ex:redheffer-1812 / ex:fulton-exposure-1813 for the full pattern (claim record + exposure record + `contradicts`).

## B.2 New record field: `record_kind`

Mining the medieval layer exposed a latent ambiguity: Bhaskara's wheel is a *description*, Redheffer's wheel was a *demonstration*, Hutchison footage is an *observation*, Leonardo's notebook pages are an *analysis*. New optional enum, default `observation`:

`record_kind: observation | demonstration_claim | design_description | analysis`

## B.3 Registry addition (per G.1)

| ID | Label | Status | Rationale · instances |
|----|-------|--------|----------------------|
| M-MCH | Classical mechanics (statics/dynamics) | established | The corpus resolves many claims into plain Newtonian mechanics; the node was missing · ex:leonardo-refutation-1494 |

## B.4 Attestation vs. ratification (honest semantics)

What this release **certifies** (technical attestation by the compiler): syntax validity of every file, grammar conformance of every ID/token/signature, closure of all relation and link references, append-only integrity against v1.0.0, SHA-256 checksums (MANIFEST).

What it **does not and cannot certify**: the truth of any claim, the verification of citations against primary sources, or community adoption. **Ratification is the community's act** — GOVERNANCE.md provides the process and ballot. "Final" in an append-only standard means: this release line is closed and signed; everything after it belongs to the adopting community.
