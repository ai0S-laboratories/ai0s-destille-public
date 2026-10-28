# VERIFY — ai0S-destille (signed-only-no-anchor)

Independent verification guide for the `ai0S-destille` bundle ("BELOW" — Novella *"DIE DESTILLE / THE STILL-HOUSE"* + Workbook of the Knowledge Distillation Tool inside today's internet).

- **Mode:** `signed-only-no-anchor` (Ed25519 signatures + SHA-256 manifest + parent chain to `ai0S-deepdive-3` and `PID 1`, without OTS/TSA blockchain round)
- **Signer (Ed25519):** `9F4D9A266D720FE6336574D87B410637560297CF` (`Marcus Dilger <private@privacy.law>`)
- **Origin Anchor (`PID 1`):** `ai0S@sha256:b3aeee619d9cb691cc6618466407d56598e830c53c6d024748d4582887c57d13`
- **Parent Anchor (`Series III`):** `ai0S-deepdive-3@sha256:6ea11ce275b8fd2ef8115cd5ed6c0eabd0db80dca823de0ae1975f29244623df`
- **Bundle Root (`SHA256(ROOT.preimage)`):** `3921eeb5ef6b801ed2cd29d220eac89ab8f8552fe9aa30c01b90a334d074ae85`

---

## 1. Import Public Key

```bash
gpg --import pubkey.asc
gpg --fingerprint 9F4D9A266D720FE6336574D87B410637560297CF
```

## 2. Verify Manifest & File Signatures

```bash
gpg --verify MANIFEST.json.sig MANIFEST.json
for s in *.0s.sig NOVELLA-*.md.sig NOVELLE-*.md.sig WORKBOOK-*.md.sig WERKBUCH-*.md.sig README.md.sig; do
  gpg --verify "$s" "${s%.sig}"
done
```

## 3. Verify SHA-256 Checksums Against `MANIFEST.json`

```bash
jq -r '.files[] | "\(.sha256)  \(.path)"' MANIFEST.json | sha256sum -c -
```

## 4. Verify `ROOT.preimage` Hash

```bash
cat MANIFEST.json MANIFEST.json.sig | sha256sum
sha256sum ROOT.preimage
# Expected: 3921eeb5ef6b801ed2cd29d220eac89ab8f8552fe9aa30c01b90a334d074ae85
```
