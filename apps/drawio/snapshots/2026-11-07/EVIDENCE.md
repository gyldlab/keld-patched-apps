# Evidence — draw.io Desktop 31.7.0 / KELD macOS V9

This is an index of source and **local** macOS acceptance evidence for [GH1404](https://github.com/gyldlab/keld/issues/1404) and its [framework draft PR #1447](https://github.com/gyldlab/keld/pull/1447). It does not distribute a binary or independently reproduce every native observation.

## 1. Source patch and unchanged application assets

| Check | Evidence and result |
| --- | --- |
| Upstream desktop source | `2edf9fb97eff9bd94bdda33abfe1ee9e7f7bb55e`; pristine `src/main/electron.js` SHA-256 `55505e690d37070344be172a68ad997ab48c687302dc5dee30a988d4f153770d` |
| Embedded webapp | Upstream commit `24b76c2cbd55d88e354042e8d329a2e4708972bc`; no webapp/renderer file in this patch |
| Original preload | **Unmodified**, SHA-256 `1091fd21ef727a52ef89bde814aa662eed4a0c3ce32beb858a068a96b285bf98`; independently matches the V9 packaged preload |
| Adapted main | SHA-256 `17ba6d13732fe2b2b055340e5933b41c722a82d5c1212c65f866beb6aacc7208`; independently matches V9 packaged main |
| Forward patch | `patches/electron-main.patch` SHA-256 `ac64e351e051ffb998dbbba45f9d916cf21cceb5bf8b7276d21d1cbd4198ffcc` |
| Reverse patch fingerprint | SHA-256 `dd5206e829baaba5c27872363dcf605e1bf45d0e068d75e76851fd2920102ee3` (a historical review artifact; reverse patch file not included here) |
| Zero-fuzz controls | On 2026-11-07, `patch --dry-run --fuzz=0 -p1` passed against the immutable pristine desktop tree; `patch --dry-run --fuzz=0 -R -p1` passed against the immutable amended V7 candidate. Both source hashes were independently checked. The source candidate bytes match V9's packaged main. Both commands exited **0**, without modifying the source trees. |

Bounded source approval: [GH1404 review comment 6700147830](https://github.com/gyldlab/keld/issues/1404#issuecomment-6700147830). It covers the reviewed original-main patch and its recovery startup behavior, not unrestricted Electron API parity, every framework file, or every packaged/native effect. The framework implementation is identified by **commit `69ce0730c2b23a631dc8324bafb4264f90a4e394`**, [draft PR #1447](https://github.com/gyldlab/keld/pull/1447).

## 2. V9 application build and packaging

The V9 product was **actually built** as a local ad-hoc signed `.app` and `.dmg` for macOS ARM64, draw.io version 31.7.0. This is a separate product result; patch correctness alone does not establish it.

| Artifact / input | SHA-256 or result |
| --- | --- |
| Qualified source manifest | `4e314351ee48280dd3e50435c26b2c34b00eade7a1c04583d5c0a06ab246c06e` |
| V9 qualification receipt | `909429159ec34fa8e57dfee8a4d0c0a765cd2e949dbd0924a5bcc0aa68dce987` |
| Raw optimized Host input | `d685ce76e56558fae14c28cf909c6cdf298c469f023b7abf55b4457747d30beb` |
| Raw optimized CLI input | `d5ed5d6d4c867b93ab9f09f1e644032ebaeb6a36f290961fc8a5d80050afea39` |
| Signed Host **inside** the V9 app | `7897b55a57e55b3399d79e68403a4f65c48e74a84ef87bb2f5b7f95bf07391ca` (post-signing bytes differ from raw optimized input) |
| V9 DMG | **PASS built**; SHA-256 `b0984a9ba0666169a24438d0ca404d6f9e4634ee058ef969a740a5ac1717a9d4` |
| V9 pack receipt | `c74385bfe100728457bb33a22aef1c9bd4b7a4b8509aaca6968e17077b06986e` |

The `.app` is a directory; it has no single normal file SHA-256. The build receipt inventories its signed files. These product artifacts and detailed native logs remain owned by the GH1404 framework record; **none are committed to this source-only repository**. The source manifest and qualification hashes are machine-independent identifiers, not public download URLs.

## 3. Tests and native behavior

| Gate | Recorded status | Scope |
| --- | --- | --- |
| Rust workspace | **PASS**, 2,093 tests passed; 17 skipped | Root's final source-bound Rust suite |
| KIPC, API and Electron SDK | **PASS**, 6/6 test/typecheck commands, exit 0 each | Source- and SDK-level controls; separate from native clicks |
| Static/tooling | **PASS** — Clippy, formatting, generated `llms` corpus check, agent instructions and atomic-protocol gates | Root's final framework source closure |
| Native editor | **PASS** — Save, Cancel and Discard | Installed **V9** original draw.io macOS editor |
| Actual Bun recovery | **PASS** — real generation-2 (G2) successor request and post-recovery Save | V9 installed native workflow, not mocked runtime |
| Ordinary clean Host exit | **PASS** — separately observed kernel exit status `0` | Ordinary V9 Host; proof does not automatically transfer to recovered Host |
| Recovery Host exit | **LIMITED** — recovery Host was observed to exit with kernel status `0`, but its same-birth exit observer was **not registered before execution** | Do **not** call this a pre-registered same-birth kernel terminal proof; that stronger recovery-shutdown acceptance remains unproven |

Root also reports an installed tamper/refusal control passing. The current V9 native success does not erase historical V6 crash-recovery failures or imply watcher replay, in-flight callback replay, broad multi-window support, or generalized compatibility.

## 4. Public-release and platform limits

The bundle/DMG is for **local ad-hoc development installation**. There is **no verified Developer ID notarization or public publisher trust**, no separate second-Mac installation proof, no performance or application-size comparison score, and no Windows/Linux implementation or native acceptance. The explicit Legacy profile is **not** proof of Strict-profile sandboxing.

This index is intentionally public-safe: it excludes machine-specific absolute paths, private logs, files containing user diagrams, binaries, provider archives and secrets.
