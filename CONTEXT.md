# Project Context for Claude

> When starting a new Claude session in this directory, prompt with:
> *"Read CONTEXT.md before doing anything else."*
>
> Everything below is durable context — read it once, treat it as committed defaults, don't relitigate.

---

## What this project is

**new-gcs** — a native ground control station for ArduPilot / PX4 drones, built with Flutter.

- **Targets:** Windows desktop and Android.
- **Public repo:** https://github.com/rwoneill/new-gcs
- **Started:** 2026-04-28 (pivoted away from forking QGroundControl).
- **Open-source goal:** approachable enough for other non-developers to fork and modify with Claude's help. Stack and structure choices should respect that.

## Who you're working with

- User is `rwoneill` on GitHub. **Self-described non-developer** — relies on Claude to write and modify code. Explanations should be clear without assuming dev background.
- ArduPilot operator. Previously used custom QGroundControl builds (terrain-follow, hostname-support).
- Member of Overhead-Intelligence org but uses personal GitHub for this project.

## Stack decisions — already settled

- **Flutter 3.41.8 + Dart.** Native Skia rendering. No web UI anywhere.
- **Platforms:** Windows + Android only. (Other Flutter targets like iOS/macOS/Linux are intentionally not enabled.)
- **Org / package:** `com.overheadintelligence`, package `new_gcs`.
- **MAVLink:** plan is pure-Dart (`dart_mavlink` or hand-rolled) for v1. Optional "connect to an external MAVProxy via UDP" mode for power users — but **MAVProxy is NOT bundled** with the app.

### Rejected options (don't suggest these)

- **Electron / Tauri / Capacitor / PWAs** — all use webviews/HTML rendering. Ruled out because drones need a stable native app; web UIs perceived as less stable.
- **React Native** — JS-based UI, same concern.
- **Qt / QML** — what QGroundControl uses. Ruled out: worst Claude-effectiveness for non-dev contributors. (QGC is fine as a *reference* for patterns/algorithms — just not as a base to fork.)
- **C# WPF / WinUI** — would have been the Windows-only stability champion, but ruled out because Android matters too.
- **Bundling MAVProxy as the comms backend** — kills Android cleanly (Python-on-Android is painful), bundling Python makes the installer brittle, and the app still has to parse MAVLink anyway.

## User preferences (apply across all work)

- **No web UI for drone or safety-adjacent apps.** Native rendering only. This is a hard line.
- **Don't put dev projects on the Google Shared Drive** (`G:\Shared drives\...`). Active source lives at `C:\dev\<project>`. The shared drive is for distributing finished binaries — Drive sync chokes on large dev trees (`node_modules`, Flutter `.dart_tool`, etc.) and causes lock errors.
- **Inspired by QGC, not a fork.** Treat QGC as a reference, not a base.

## Current state (as of 2026-04-28)

**Done:**
- Flutter SDK 3.41.8 installed at `C:\dev\flutter`; `C:\dev\flutter\bin` on user PATH.
- Project scaffolded with `flutter create --platforms windows,android`. **App is the default counter template — no GCS code yet.**
- Git initialized, initial commit pushed to GitHub `main` branch.
- Local git config (this repo only): `user.name=rwoneill`, `user.email=125233733+rwoneill@users.noreply.github.com`. Global git config left untouched.

**Toolchains installed and verified green on 2026-04-28:**
- Visual Studio Build Tools 2022 17.14.31 with C++ workload (`C:\Program Files (x86)\Microsoft Visual Studio\2022\BuildTools`).
- Android Studio 2025.3.4.6 + Android SDK 36.1.0 (`C:\Users\roger\AppData\Local\Android\Sdk`).
- Android cmdline-tools (build 14742923) installed at `<SDK>\cmdline-tools\latest`.
- All Android SDK licenses accepted.
- `flutter doctor` reports "No issues found" — Windows desktop and Android builds both ready.

**Outstanding work:**
- License field in `pubspec.yaml` and `README.md` still says "TBD" — pick one (MIT and Apache-2.0 are the conventional defaults for an open-source GCS).
- Pick MAVLink dialect target: ArduPilot only, PX4 only, or both. (Decision affects which `dart_mavlink` dialect we generate from / how strict to be.)
- Replace the default counter template with an actual GCS shell. Reasonable v0: a connection screen (UDP/TCP), a basic telemetry panel, and a map widget showing vehicle position.
- Sanity-check that builds work: `flutter run -d windows` from the project dir should launch the default counter app.

## Useful paths and links

| | |
|---|---|
| **Project source** | `C:\dev\new-gcs` |
| **Flutter SDK** | `C:\dev\flutter` (on PATH) |
| **GitHub** | https://github.com/rwoneill/new-gcs |
| **Old custom QGC binaries (reference only)** | `G:\Shared drives\OI-Engineering\Software & Firmware\QGC\` |

## Sanity check

Before making changes, you should be able to answer these without re-asking:
- What framework? **Flutter.**
- What platforms? **Windows + Android.**
- Why not Electron / Tauri? **No web UI on drone apps — stability.**
- Why not C# (which would be more Claude-friendly)? **Android matters, .NET MAUI is too immature.**
- How does MAVLink work in this app? **Pure-Dart in v1; MAVProxy is optional and external, never bundled.**
- Where do dev files go? **`C:\dev\new-gcs`, never the shared drive.**
