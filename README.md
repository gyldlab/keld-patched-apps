# KELD Patched Apps

This repository records application migration snapshots for KELD.
Each snapshot has its own status, evidence, and known limits.

## Recorded snapshots

| Application | Snapshot date | Platform | Status | Evidence |
| --- | --- | --- | --- | --- |
| [draw.io](apps/drawio/README.md) | 2026-11-07 | macOS Apple Silicon | V9 local ad-hoc app/DMG built; native workflows passed; stronger recovery-exit proof limited; **source-only record** | [Source and evidence](apps/drawio/snapshots/2026-11-07/README.md) |
| [draw.io](apps/drawio/README.md) | 2026-11-03 | macOS Apple Silicon | Verified native workflow; developer snapshot only | [Snapshot report](apps/drawio/snapshots/2026-11-03/README.md) |

## Status terms

- **Verified workflow** means that the specified action passed on the stated test system.
- **Developer snapshot** means a preserved set of application and framework files.
- **Installable build** means a tested application package that a user can install.
- **Public release** means an installable build that passed the release acceptance tests.

A verified workflow is not an installable build.
Do not infer other application compatibility from one snapshot.

This repository stores application snapshots and technical facts only.

## Repository layout

`apps/<application>/snapshots/<date>/` contains a snapshot report, an evidence index, and a checksum file.
Large archives are stored as GitHub Release assets, not in Git history.

## Licensing

Preserve each application's copyright and license terms.
See the license notes in each snapshot before redistribution.
