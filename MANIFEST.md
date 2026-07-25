# Manifest

SHA-256 checksums over the shipped files. Regenerate after any change:

```bash
find . -type f \( -name "*.md" -o -name "*.json" \) -not -path "./.git/*" -not -name MANIFEST.md -print0 | sort -z | xargs -0 sha256sum
```

Scope of attestation: technical integrity only — syntax and grammar conformance, checksum correctness. Not a truth certification. See GOVERNANCE.md.

CI verifies on every push that the schemas parse and that this manifest lists every shipped file with a current checksum.

| File | SHA-256 |
|------|---------|
| `GOVERNANCE.md` | `ccc2585db900f5e0c41871d312c5f4accfc2ced4870b7a05aa8fc686b96bec5b` |
| `README.md` | `764349982836e4aaf81b0cf2ce016aa45ec3892f0f69223c3f3c103b36a68c4d` |
| `SPECIFICATION.md` | `32437491ba88ad4d9ba27a6d59764ad2d67060a3be775e0a2a3602273f538384` |
| `schema/corpus.schema.json` | `dd453230c09b389f27b1a0c6063ad1e5f5f5b0b832417b6fe3c4eb22e1e1af82` |
| `schema/observation.schema.json` | `9b00e81f6466dcf2c73a3330a99163acbf56d68971d05b109db03ec0ea71b81c` |
| `schema/vocabulary.schema.json` | `29920fa46dda0d5cf824d3aa4f04e301af11edb7262be0576a0badfd2ac66552` |
| `vocabulary.json` | `e28553fcd2af04a97c1fc22adee81a6558a06a6ed04b6621edb4705aa3076e23` |
