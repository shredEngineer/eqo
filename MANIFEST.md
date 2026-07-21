# Manifest

SHA-256 checksums over the shipped files. Regenerate after any change:

```bash
find . -type f \( -name "*.md" -o -name "*.json" \) -not -path "./.git/*" -not -name MANIFEST.md -print0 | sort -z | xargs -0 sha256sum
```

Scope of attestation: technical integrity only — syntax and grammar conformance, checksum correctness. Not a truth certification. See GOVERNANCE.md.

CI verifies on every push that the schemas parse and that this manifest lists every shipped file with a current checksum.

| File | SHA-256 |
|------|---------|
| `ADDENDUM-A.md` | `c6051457ad25df2300a1ecaf326f5770d7fc68eea8f6f043fd8ef964d052cd53` |
| `ADDENDUM-B.md` | `e941002c2ff39909f67ad82c62ff7f788181c9d45ccc311d206d768de871fa63` |
| `GOVERNANCE.md` | `99a6d8bab4aee2e163d3380116fee821a1f281b4ae91ccb78f94f08b76eeaf9b` |
| `README.md` | `7e7e31c76e49fc187f35ed9c3e0d1139802ad331c94cf6917650a569b1fa87a2` |
| `schema/corpus.schema.json` | `dd453230c09b389f27b1a0c6063ad1e5f5f5b0b832417b6fe3c4eb22e1e1af82` |
| `schema/observation.schema.json` | `c026b1efe8e0d1aa6a67f778e7a8b3ad9524c59f6c405782304fd8f901a23f7c` |
| `SPECIFICATION.md` | `926cf7ce4276555d07a421caf147cce0b7da60402b189781531a0f2ec88728e3` |
