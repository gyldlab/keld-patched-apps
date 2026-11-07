# draw.io on KELD

**Current record:** [2026-11-07 macOS V9 source-only record](snapshots/2026-11-07/README.md) · **Earlier record:** [2026-11-03 developer snapshot](snapshots/2026-11-03/README.md)

The original draw.io Desktop 31.7.0 now has a locally built, ad-hoc signed
KELD macOS ARM64 `.app` and DMG, using the explicitly declared Legacy profile.
The V9 installed original editor completed Save, Cancel, Discard and post-Bun
generation-2 recovery Save on a real Mac. An ordinary Host's kernel-zero exit
was observed. The recovery Host also exited zero, but its same-birth exit
observer was not pre-registered; see the [V9 evidence limits](snapshots/2026-11-07/EVIDENCE.md).

This repository's **current packet is source-only**. It carries the bounded
original-main patch, reproducibility hashes, attribution and evidence, with no
signed app, installer, binaries or vendor files. The earlier ZIP is a separate
developer snapshot and remains **not** a verified standalone installer.
Neither record establishes public notarization, a second Mac, Windows/Linux
compatibility, or a performance benchmark.
