# Screen Time Manager: instructions for Codex

## Product direction

Develop a parental-control application for Windows and Android, with Kaspersky
Safe Kids as a functional reference. Keep the upstream MIT license and attribution.
The current application supports Windows only; Android is a planned client.
See `docs/PROJECT_PLAN.md` for scope, evidence and milestones.

## Working with this repository

- Preserve existing Windows behavior while extracting platform-independent logic.
- Keep Win32 APIs in Windows modules. Share policies and domain types through a
  Rust library; Android needs native integration, not a repackaged Windows binary.
- Apply policies locally when offline. Define time-zone, midnight, restart and
  clock-change behavior before changing time accounting.
- Treat pairing, PINs, device credentials and remote commands as security-sensitive.
  Do not log secrets or keep new credentials in plaintext.
- Use visible parental-control enrollment and clear permission explanations.
- Do not run installation scripts or input-blocking binaries in the cloud executor.

## Validation

The upstream executable requires Windows. Its existing release workflow uses
`windows-latest`; Linux-only checks cannot establish Windows runtime behavior.
On Windows, run `cargo check --locked` and `cargo build --release --locked`.
Test shared Rust policy logic on Linux once that library exists. Build and verify
Android on its own toolchain and physical devices. State which checks ran and which
platforms were unavailable. Do not claim an EXE or APK is ready without building it.

## Release workflow

The existing workflow publishes when pushing to `release`. Use feature branches
for development. Review fork-specific naming, release destinations and update
behavior before publishing; do not automatically publish an upstream version
under the new project's identity.
