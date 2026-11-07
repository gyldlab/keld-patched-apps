# draw.io Desktop 31.7.0 — KELD macOS V9 source record

**Snapshot:** 2026-11-07 · **Platform:** macOS Apple Silicon (arm64) · **Profile:** explicitly declared Legacy

**Record type:** source-only reproduction packet for [KELD GH1404](https://github.com/gyldlab/keld/issues/1404). The tested application is draw.io Desktop 31.7.0 with a locally built, ad-hoc signed KELD `.app` and DMG. **This repository contains no application bundle, DMG, vendor dependencies, runtime binary or SDK archive.** It does not offer a downloadable installer or claim a publicly trusted release.

## Source and attribution

- Desktop upstream commit: `2edf9fb97eff9bd94bdda33abfe1ee9e7f7bb55e`.
- Embedded draw.io webapp commit: `24b76c2cbd55d88e354042e8d329a2e4708972bc`.
- Pristine `src/main/electron.js` SHA-256: `55505e690d37070344be172a68ad997ab48c687302dc5dee30a988d4f153770d`.
- Adapted `src/main/electron.js` SHA-256: `17ba6d13732fe2b2b055340e5933b41c722a82d5c1212c65f866beb6aacc7208`.
- Original **unchanged** `src/main/electron-preload.js` SHA-256: `1091fd21ef727a52ef89bde814aa662eed4a0c3ce32beb858a068a96b285bf98`.
- Source patch: [`patches/electron-main.patch`](patches/electron-main.patch), SHA-256 `ac64e351e051ffb998dbbba45f9d916cf21cceb5bf8b7276d21d1cbd4198ffcc`.

The patch adapts original-main event authentication, native close handling, Exit and optional first-window zoom behavior, and the bounded recovery-startup handoff after Bun replacement. It neither replaces the original webapp nor edits the original preload. Source ownership and redistribution obligations are explained in [LICENSES.md](LICENSES.md).

## Reproduce the source change

1. Check out the **exact** desktop and embedded webapp commits in [SOURCE.json](SOURCE.json), including upstream license files.
2. Verify the SHA-256 of the pristine main and preload before applying any patch.
3. Apply [the unified source patch](patches/electron-main.patch) to the desktop root with zero fuzz. A read-only `patch --dry-run --fuzz=0 -p1` passed against the immutable pristine original in the 2026-11-07 evidence check.
4. Verify that the resulting main SHA-256 is `17ba6d13732fe2b2b055340e5933b41c722a82d5c1212c65f866beb6aacc7208`. Reverse the same patch with zero fuzz and confirm the pristine digest is restored. The independent reverse dry run also passed.
5. Use the exact KELD framework implementation commit `69ce0730c2b23a631dc8324bafb4264f90a4e394` from [GH1404 draft PR #1447](https://github.com/gyldlab/keld/pull/1447), as recorded in [SOURCE.json](SOURCE.json). Verify the separately recorded provider, source-manifest and local packaging receipts before attempting a reproduction.

## Qualified observations and remaining limits

Root reports one locally ad-hoc signed **V9** macOS `.app`/DMG build and real original-draw.io Save, Cancel, Discard, and post-Bun-G2 recovery Save workflows passing. The V9 DMG SHA-256 is `b0984a9ba0666169a24438d0ca404d6f9e4634ee058ef969a740a5ac1717a9d4`. An **ordinary** installed Host had a separately observed kernel exit status of zero; a recovered Host was also observed exiting zero, but its same-birth exit observer had **not** been pre-registered. Recovery shutdown therefore lacks that stronger independent observer proof. [EVIDENCE.md](EVIDENCE.md) separates source proof, packaging proof, native workflow proof, and that terminal-proof limit.

No Developer ID/public notarization, cross-Mac installation, Strict containment, Windows/Linux behavior, general Electron compatibility, application-wide feature parity, or performance/size score is claimed. The recorded build is a **local development installer only**.

See [SOURCE.json](SOURCE.json) for machine-independent reproducibility metadata and [SHA256SUMS.txt](SHA256SUMS.txt) for this packet's file hashes.
