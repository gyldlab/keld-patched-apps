# Evidence index — draw.io V10

Evidence date: 2026-11-02. Snapshot publication date: 2026-11-03.

## Original macOS native proof

| Receipt ID | Test result | Exact observation |
| --- | --- | --- |
| V10f64A | exit 0 | Dirty Close → Save; file saved; window closed without merge/overwrite; real native Quit; owned stage removed |
| V10f64B | exit 0 | Fresh process reopened prior save; dirty Cancel kept window/edit; dirty Discard closed window without changing saved bytes; native Quit; stage removed |

The local first-party receipt used the following digests:

- Host in V10f64A/V10f64B: `0f62b9689ba7a10452a1e8e4f970992fd48e8d99d008511745df9f9ab2c53d36`.
- Native test executable in those runs: `9e53850ad1577438daaeca27ad5dd2d70e36fd8bdbab3424203226e54914a4fc`.
- Original `input.drawio`: `6a4f0c9cc38d4e09925c2a62c9119f96655a6bdb9242e4fedc9bc44902310d8d`.
- Saved modified test file: `91010de0762fb046f8e4f63ce231bc3a083a2be55f2d3a08e3db712f0a2683d5`.

## Timestamp precision

The application first reported an External Changes warning for an unchanged file.
The native diagnostic measured an `mtimeMs` discrepancy of `0.000244140625`
milliseconds, or one floating-point unit in the observed case.
The KELD Rust parser was updated to use serde_json's `float_roundtrip` option.
A failing numeric regression test passed after the change.
The real application then saved and closed without the false warning.

Fix scope:
`crates/keld-wv/Cargo.toml`, `crates/keld-wv/src/wv_link.rs`.

The correction does not disable real file-conflict detection.

## Rust and TypeScript component runs

- `cargo nextest run --locked --workspace --profile ci --no-fail-fast --test-threads 4`:
  exit 0; 2,133 tests passed, 21 skipped.
- `just --no-deps typescript`: exit 0 on the post-fix component gate.
- Prior TypeScript full component result: 833 passed.
- `cargo clippy --locked --workspace --all-targets -- -D warnings`: exit 0.
- `cargo doc --locked --workspace --no-deps`: exit 0.
- `cargo fmt --all -- --check`, `git diff --check`, `just js-fmt-check`: exit 0.

Caution: These are local workspace receipts, not a hosted pull-request
approval or an exact-head release CI receipt.

## Open CI gate

The full `just ci` command stopped at workspace admission. The active
worktree contained a nested retained `.keld-work` evidence directory.
Other active workspace metadata did not match the registered checkouts.
The evidence was preserved. No successful full CI result is claimed.

## Snapshot / current binary distinction

The ZIP contains the then-current development Host with SHA-256
`d695ec963eb20a115e7c1ecd37bedef6dd68034bb10a423442058f539dba2280`.
The successful app-flow proof used Host
`0f62b9689ba7a10452a1e8e4f970992fd48e8d99d008511745df9f9ab2c53d36`.
A current or copied executable must be requalified before an end-to-end
behavior claim can be extended to it.

This index summarizes retained first-party machine receipts.
It does not include private absolute paths, session controls, or raw logs.
