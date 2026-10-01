# crescendo-speech-models

The speech models Crescendo Companion downloads: the Whisper speech-to-text models a person picks as
Best, Balanced or Fastest, and the voice activity detector. Nothing here is built. Each release is
one model set, exactly as `packages/crescendo-speech-models` in `evertz-lvrm/crescendo` names it, and
the app reads the newest release.

## A release

Tagged `models-` and twelve hex digits, a digest of the set's manifest lines, so the same set always
has the same tag. Its assets are flat:

| Asset | What it is |
|---|---|
| `<sha256>` | A model or the detector, named by the SHA-256 of its bytes. |
| `index.json` | The catalogue: each model's name, digest, size and tier, and the detector's. |
| `index.json.<release\|dev>.sig` | The catalogue's ed25519 signature by an update signing key, when the set is signed. |
| `COPYRIGHT` | Where each file comes from, and the terms it is taken under. |

A companion downloads `releases/latest/download/index.json`, checks its signature with the key its
build trusts, then fetches the files of the tier its person picked, by digest, checking each.

## Publishing one

Not by CI. A person runs `packages/crescendo-speech-models/publish-release.sh` from a checkout of
`evertz-lvrm/crescendo` once, when the set changes. A release is never changed after.
