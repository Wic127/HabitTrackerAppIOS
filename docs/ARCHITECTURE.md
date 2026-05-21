# HabitTrackerAppIOS Architecture

## Goals

- Keep habit data on the user's device.
- Avoid a custom backend, hosted database, or server-side user data.
- Do not ship a shared Gemini API key in the iOS binary.
- Preserve the core flows from the web prototype:
  - Dashboard
  - Create/Edit Habit
  - AI Habit Builder
  - Habit Details Calendar
  - Habit Tree / Sub-Habits
  - Insights
  - AI Coach
  - CSV export/share

## Recommended Stack

- UI: SwiftUI
- Persistence: SwiftData
- Charts: Swift Charts
- Haptics: `UIImpactFeedbackGenerator` / `UINotificationFeedbackGenerator`
- Secrets: Keychain for user-provided credentials, if BYOK is chosen
- AI: Firebase AI Logic with App Check, or user-provided Gemini key as fallback

## Gemini Security Decision

The React prototype calls Gemini directly from the client bundle. That pattern is not acceptable for a production app using a shared developer-owned API key.

Recommended production option:

- Use Firebase AI Logic and App Check.
- Do not store habit data in Firebase.
- Send only the minimal habit summary required for AI coaching.
- Make AI features optional and transparent in privacy text.

Strict no-managed-proxy option:

- Let users provide their own Gemini API key.
- Store the key only in Keychain.
- This avoids a hosted backend but creates a less polished onboarding flow.

## Local Data Model Draft

```swift
@Model
final class Habit {
    var id: UUID
    var name: String
    var category: String?
    var goalDescription: String?
    var icon: String
    var startDate: Date
    var completedDates: [String]
    var streak: Int
    var segments: Int
    var segmentUnit: String?
    var dailyProgress: [String: Int]
    var difficultyRating: Int
    var weeklyTarget: Int
    var subHabits: [SubHabit]
}

@Model
final class SubHabit {
    var id: UUID
    var name: String
    var goalDescription: String?
    var target: Int
    var unit: String?
    var completedHistory: [String]
    var streak: Int
}
```

The exact SwiftData representation may need adjustment because array/dictionary persistence has practical constraints. If needed, completion history can move into child entities rather than encoded arrays.
