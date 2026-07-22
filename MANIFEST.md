# Manifest

SHA-256 checksums over the shipped files. Regenerate after any change:

```bash
find . -type f \( -name "*.md" -o -name "*.json" \) -not -path "./.git/*" -not -name MANIFEST.md -print0 | sort -z | xargs -0 sha256sum
```

Scope of attestation: technical integrity only — syntax and grammar conformance, checksum correctness. Not a truth certification. See GOVERNANCE.md.

CI verifies on every push that the schemas parse and that this manifest lists every shipped file with a current checksum.

| File | SHA-256 |
|------|---------|
| `ADDENDUM-A.md` | `b53a4c201e4ebe2f79550c020d1e9da90feac28293a5049d723aa96b8f08937c` |
| `ADDENDUM-B.md` | `4aa7e3b3509a3ba93274f1efb35683558d33ebe1d81c718f6d0a0a1c51b78766` |
| `ADDENDUM-C.md` | `4baf6fb90220a13f8abb38ba897764dd3133a9deedf1101d9af2708335fc6c3f` |
| `GOVERNANCE.md` | `99a6d8bab4aee2e163d3380116fee821a1f281b4ae91ccb78f94f08b76eeaf9b` |
| `README.md` | `1ac355cc8d66e49aa4c54d84a51c8b803cbdab2b9fe816273786f69971d23a07` |
| `SPECIFICATION.md` | `6b5e9ee0feb5831e376330b1f320d0d3f12e65ff5816bc0058c9d2e9bd09d1a8` |
| `schema/corpus.schema.json` | `dd453230c09b389f27b1a0c6063ad1e5f5f5b0b832417b6fe3c4eb22e1e1af82` |
| `schema/observation.schema.json` | `5bd9bdbf7895ed494296f62722cec506c00c1bcd49d2eeaa031f03ba894cd5b7` |
| `schema/vocabulary.schema.json` | `78708b3a00d14890f7e8661e024f8c551fde3076e00f8cf5bb67836f5af6dd23` |
| `vocabulary.json` | `a6698c55f9617eab7e3d69aaf5f292c23d8e1498d6c62c42196211267c8c0e4d` |
