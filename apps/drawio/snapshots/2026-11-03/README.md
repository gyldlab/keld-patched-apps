# draw.io V10 — macOS developer snapshot

**Snapshot date:** 2026-11-03 (UTC+05:30)
**Native test evidence:** 2026-11-02
**Application:** original draw.io desktop application, version 31.7.0
**Framework:** KELD macOS MVP
**Platform:** macOS, Apple Silicon (arm64)
**Security profile:** explicitly declared Legacy
**Status:** verified native workflow; **not** an installable or production build

## 1. Purpose

This record preserves the first documented draw.io migration snapshot.
It reports what the tested build did. It also reports what is not verified.

The experiment used the original draw.io JavaScript application with
KELD-specific configuration and installed KELD compatibility packages.
The snapshot is a test artifact. It is not evidence of complete Electron
compatibility.

## 2. Snapshot artifact

**Download:** [macOS arm64 developer snapshot ZIP](https://github.com/gyldlab/keld-patched-apps/releases/download/drawio-v10-macos-dev-snapshot-2026-11-03/KELD-drawio-V10-mac-arm64-DEVELOPER-PREVIEW.zip)

| Field | Value |
| --- | --- |
| Archive | `KELD-drawio-V10-mac-arm64-DEVELOPER-PREVIEW.zip` |
| Actual size | 133,540,034 bytes (133.54 MB; 127.35 MiB) |
| SHA-256 | `a420b00b2450b89ef31bdff6e1ef40f93e4f6c817110fc40e09a4f39540057c7` |
| Archive integrity | ZIP CRC verification passed |
| Contents | Original app copy, installed KELD providers, Bun runtime, KELD development binaries, a sample diagram, and a native test binary |
| Packaging | ZIP developer snapshot, not an app installer |
| Portability | No successful independent launch on another Mac is claimed |

The archive has a read-only environment check script. It does not provide
a working standalone draw.io launcher. Do not bypass a KELD admission check.

## 3. Verified behavior

The native macOS acceptance runs used the real draw.io editor.
They did not use a mock editor for the listed user workflow.

| Operation | Result | Evidence |
| --- | --- | --- |
| Start the original draw.io editor in KELD | PASS in the qualified native test run | V10f64A/V10f64B |
| Open a disposable `.drawio` test file | PASS | V10f64A |
| Edit a diagram label | PASS | V10f64A |
| Close with unsaved changes and select **Save** | PASS | V10f64A |
| Save without the false External Changes prompt | PASS with timestamp-precision fix | V10f64A |
| Reopen the saved copy in a new process | PASS | V10f64B |
| Close dirty document and select **Cancel** | PASS; editor stays open | V10f64B |
| Close dirty document and select **Discard** | PASS; previously saved bytes unchanged | V10f64B |
| Quit using native macOS application controls | PASS in both qualified runs | V10f64A/V10f64B |
| Remove the owned temporary stage | PASS | V10f64A/V10f64B |
| Keep the original input file unchanged | PASS; SHA-256 verified | Both runs |

These claims apply only to the tested macOS build and test files.
They do not certify other draw.io features or other operating systems.

## 4. Tests and source validation

The retained local receipts show:

- **Rust:** 2,133 tests passed and 21 skipped, on a complete four-thread workspace run.
- **TypeScript:** 833 tests passed in the established component run.
- **Rust Clippy:** passed with warnings denied after the timestamp fix.
- **Rust documentation and formatting checks:** passed in recorded component runs.
- **Native D1 Host qualification:** passed in the original tested Host/test pair.
- **Timestamp precision:** an exact binary64 discrepancy failed before the fix and passed after it.

An earlier full Rust attempt had a Guardian shutdown failure.
Two isolated reruns passed, and the later complete 2,133-test run passed.
The first intermittent failure was not fully explained. Do not call that
failure resolved solely because the rerun passed.

The complete `just ci` command was **not green**. Its workspace-admission
check rejected retained nested evidence and stale worktree records. Do not
disable this check, discard worker data, or replace it with a component-pass claim.

## 5. Known limits

- The ZIP does not include a signed, notarized macOS `.app` or `.dmg`.
- The original editor currently launches through a private, approved-graph
  first-party test caller. Ordinary `keld dev` does not provide that admission.
- The bundled current development Host has a different SHA-256 than the Host
  used in V10f64A/V10f64B. Those proofs do not automatically qualify this ZIP
  as a portable executable application.
- The profile is **Legacy**. Do not claim KELD Strict containment.
- External file-change notifications remain outside the tested channel grants.
- Automatic updates are not a shipped function of this snapshot.
- Comprehensive draw.io features such as export, print, clipboard,
  drag-and-drop, multi-window operations, and general file association were
  not accepted as a complete product matrix.
- Windows and Linux draw.io acceptance is not established.
- Exact integrated source, review gates, full CI, packaging, and release
  qualification remain incomplete.

## 6. Next acceptance gates

1. Preserve existing test files and original native receipts.
2. Requalify the exact application, Host, SDK, and runtime byte set.
3. Provide a portable launch path that uses the approved graph admission.
4. Prove fresh installation and native operation on a second supported Mac.
5. Resolve or explicitly gate remaining reliability and compatibility issues.
6. Run full CI on the exact committed integration and complete independent review.
7. Build and independently verify installer, signing, and notarization.
8. Publish an installable release only after these checks pass.

## 7. Evidence and integrity

Read [EVIDENCE.md](EVIDENCE.md) and [SHA256SUMS.txt](SHA256SUMS.txt).
For source origin and license notes, read [LICENSES.md](LICENSES.md).

**Claim allowed:** “The original draw.io editor completed the documented
Open/Edit/Save/Reopen/Cancel/Discard/Quit workflow on KELD on a real Mac.”

**Claim not allowed:** “draw.io is fully compatible with KELD or ready for
public installation.”
