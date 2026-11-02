# ACCESS PC

Free, open-source accessibility layer for desktop computers. It sits on top of the operating system's own accessibility services and adds alternative input (voice, head, gaze, switch) and, later, a safe AI assistant.

ACCESS PC does not replace the OS screen reader or built-in accessibility features. It is not a medical or emergency device.

Status: **pre-alpha scaffold** for Release 1 (see `docs/`). Licence: GPL-3.0-or-later.

## Layout

| Path | Purpose |
|---|---|
| `core/` | Rust core: action bus, safety gate, emergency stop, audit log (safety-critical, keep small and heavily tested) |
| `protocol/` | Shared message types between UI, core, workers and plugins |
| `adapters/` | Per-OS platform adapters: `windows` (SendInput), `macos` (CGEvent), `linux` (X11 XTest). First drafts, untested. Only place OS-specific code may live |
| `workers/` | Supervised speech and vision worker processes |
| `plugins/` | Out-of-process optional integrations (eye-tracker SDKs, cloud AI). Never bundled |
| `ui/` | Tauri 2 + React/TypeScript front end |
| `docs/` | PRD, architecture diagrams, ADRs, licence inventory, M0 spike plan (`docs/spikes/`) |

## Try the core

```
cargo test
cargo run -p access-core
```

## Design rules (from PRD v1.1)

1. Every action that touches the OS flows through one safety gate.
2. Emergency stop is a lock-free flag checked by every adapter, handled on its own thread.
3. Every function reachable by at least two input methods.
4. Offline by default. Network use is opt-in per feature and indicated on screen.
5. Camera and microphone off until granted, with a persistent indicator drawn by the core.
