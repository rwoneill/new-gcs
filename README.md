# new-gcs

A native ground control station for ArduPilot/PX4 drones, built with Flutter.

Targets Windows desktop and Android. No web UI — real native rendering for stability and reliable drone operations.

## Status

Early development. Project scaffolding only at this point.

## Goals

- Native, dependable GCS for everyday drone operations
- Open source and approachable enough for non-developers to fork and modify (with help from AI tooling like Claude)
- Learn from QGroundControl's patterns without copying them wholesale

## Getting started

Prerequisites:

- [Flutter SDK](https://docs.flutter.dev/get-started/install) 3.41 or newer
- For Windows builds: Visual Studio with the "Desktop development with C++" workload
- For Android builds: Android Studio (with Android SDK)

Run the app:

```bash
flutter pub get
flutter run -d windows   # or: flutter run -d <android-device-id>
```

## License

TBD.
