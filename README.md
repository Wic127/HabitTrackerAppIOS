# HabitTrackerAppIOS

Native iOS rebuild of HabitOS, based on the React/Vite prototype in `Wic127/HabitTrackerApp`.

## Product Direction

- SwiftUI-first iPhone app.
- Local-only user habit data.
- Native persistence with SwiftData or Core Data.
- Native charts, haptics, animations, and share/export flows.
- Secure Gemini integration without embedding a shared API key in the app bundle.

## Planned Architecture

- `HabitTrackerAppIOS/` - future Xcode app source.
- `docs/` - architecture notes, App Store checklist, migration notes, and security decisions.
- Local persistence: SwiftData preferred unless we hit a compatibility reason to use Core Data.
- AI integration: Firebase AI Logic with App Check is the recommended production path; BYOK Gemini via Keychain is the strict no-managed-proxy fallback.

## Source Reference

Original web app:

https://github.com/Wic127/HabitTrackerApp

Live prototype inspected on May 21, 2026:

https://habitos-282299711638.us-west1.run.app/
