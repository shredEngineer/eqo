# Governance

How the standard grows, and how a body adopts it.

---

## Growth rules

- **Append-only.** Registries grow; identifiers are never recycled and never reinterpreted.
- **New phenomenon leaf** — requires an observable label, a delimitation from neighbouring leaves, and at least one instance.
- **New mechanism node** — requires a status assignment (`established` / `fringe` / `heterodox` / `historical`) with a brief rationale.
- **New signature** — requires a definition over existing registries plus canonical instances.
- **Promotion.** Residual (`SON`) leaves are reviewed periodically; once roughly five similar entries accumulate, a dedicated leaf is normalized.
- **Status revision.** A mechanism's `status` is the one deliberately mobile normative value. It changes only with a documented decision and date, and every theory-embedding grade derived from it is recomputed.
- **Versioning.** Sharpening a label or scope note is a patch. A new leaf, mechanism node, facet value, or signature is a minor version. A change to the principles, the grammar, the class set, or the axis set is a major version.
- **Private extensions.** Reserved local number ranges and a namespaced prefix are available; such extensions must not appear in interchange data without a namespace declaration.

**One rule outranks the rest:** the standard must never grow a scalar credibility score. Regions of the lattice may be named; points may not be summed into a verdict.

## Correcting a record

Corrections are ordinary operations, not incidents. Open an issue against the record identifier, state what is wrong and what the primary source says, and the correction lands as a normal append-only registry operation. Record corrections never block adoption.

## Adoption

**What a body ratifies:** the frozen core — the principles, the grammar, the class set, the axis set — together with the registries as shipped, the corpus releases as the seed dataset, and these governance rules as the amendment procedure.

**What ratification is not:** a verdict on any claim, doctrine, or narrative in the corpus. The standard is engineered so that adoption and disagreement about individual records coexist. Indexing a claim was never an endorsement of it, and indexing a narrative is not an endorsement either — the factual-kernel / lore-layer split exists precisely so a body can reference a contested story with precision.

**The process:**

1. **Review window.** Open issues against any record, node, or rule. Corrections are normal operations and do not block.
2. **Ballot.** The adopting body votes on the frozen core only:
   - [ ] Adopt the frozen core as-is
   - [ ] Adopt with recorded reservations (attach the issue list)
   - [ ] Defer (attach the blocking issues)
3. **Adoption statement.** Published with the version pin and the manifest checksums.
4. **After adoption**, all growth follows the append-only rules above; a change to the axis set requires a major version.

## Attestation semantics

Machine attestation over the shipped files covers **technical integrity only**: syntax validity, identifier and token grammar conformance, closure of every relation and link reference, append-only integrity against prior releases, and checksum correctness.

It explicitly does **not** cover the truth of any claim or the verification of any citation against a primary source. In an append-only standard, "final" means only that a release line is closed and signed. Everything after it belongs to the adopting community.
