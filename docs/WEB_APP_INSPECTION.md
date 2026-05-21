# Web App Inspection

Inspection date: May 21, 2026

## Deployment

URL:

https://habitos-282299711638.us-west1.run.app/

Observed behavior:

- Static React/Vite app served from Cloud Run / Google Frontend.
- Local habit data stored in browser `localStorage` under `habitos_data_v2`.
- Gemini requests are made directly from the browser bundle through `@google/genai`.
- The deployed bundle contained the placeholder `MY_GEMINI_API_KEY`, not a real `AIza...` key.
- Gemini calls failed with `API key not valid`, which suggests the inspected live deployment was not leaking a working key.

## Native Screens To Rebuild

- Dashboard with greeting, consistency score, categories, habit cards, weekly completion row, and bottom navigation.
- Create Habit form with name, daily goal, frequency, category, and primary action.
- AI Habit Builder with prompt input and popular idea chips.
- Habit Details with stats, habit tree entry, and quarter calendar.
- Edit Habit sheet with daily segments stepper and delete flow.
- Habit Tree list and empty state.
- Create Sub-Habit form.
- Insights screen with category filters, KPI cards, completion chart, summary metrics, and CSV export.
- AI Coach screen with forecast, KPIs, tips, category suggestions, adaptive goal suggestions, loading, empty, and error states.

## Issues To Improve In Native Version

- AI errors should render a user-facing fallback instead of leaving the Coach screen empty.
- Chart layout should reserve space above bottom navigation.
- Export should use a native share sheet.
- Haptics should use native iOS feedback APIs.
- Production AI calls must not rely on a shared API key embedded in a client bundle.
