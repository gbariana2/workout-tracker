# FitTrack — Workout Tracker

A multi-page Next.js + Tailwind CSS workout tracking app with progressive overload, data visualization, and animated UI.

## Tech Stack

- **Next.js 14+** (App Router, TypeScript)
- **Tailwind CSS v4** (frosted glass cards, dark mode, gradient accents)
- **Recharts** (line charts, area charts, bar charts)
- **Framer Motion** (page transitions, scroll reveals, animated SVG background paths)
- **Playwright** (13 automated tests)
- **localStorage** for all data persistence (no backend)

## Pages

| Route | Type | Description |
|-------|------|-------------|
| `/` | Homepage | Personalized greeting, suggested workout, week overview, stats, muscle balance, PR highlights, recent activity |
| `/log` | Form page | Workout logging form — exercise search, sets/reps/weight, progressive overload targets, template loading |
| `/workout/[id]` | Dynamic route | Individual workout detail — score badge, exercise breakdown with set-by-set tables |
| `/progress` | Data viz | Workout Score trend, per-exercise weight/volume charts, muscle group volume bar chart |
| `/records` | PRs | Personal records per exercise — max weight, max reps, best volume, estimated 1RM |
| `/templates` | CRUD | Create/edit/delete/reorder workout templates (Push A/B, Pull A/B, Legs A/B) |
| `/overview` | Redirect | Redirects to `/` (consolidated) |

## Data Model

All data stored in `localStorage` under key `workout-tracker-data`.

```
WorkoutState {
  workouts: Workout[]
  templates: WorkoutTemplate[]
  settings: UserSettings
}

Workout {
  id: string (UUID)
  date: string (ISO date, e.g. "2026-04-07")
  exercises: Exercise[]
  createdAt: string (ISO datetime)
}

Exercise {
  id: string
  name: string (e.g. "Bench Press")
  muscleGroup: MuscleGroup
  sets: WorkoutSet[]
  notes?: string
}

WorkoutSet {
  id: string
  reps: number
  weight: number
  unit: "lbs" | "kg"
}

WorkoutTemplate {
  id: string
  name: string (e.g. "Push A — Heavy")
  description?: string
  exercises: TemplateExercise[]
  createdAt: string
}

TemplateExercise {
  id: string
  name: string
  muscleGroup: MuscleGroup
  defaultSets: number
  defaultReps?: number
  defaultWeight?: number
}

UserSettings {
  defaultUnit: "lbs" | "kg"
  theme: "light" | "dark"
  overloadMode: "aggressive" | "manageable" | "chill"
  userName: string
}

MuscleGroup = "chest" | "back" | "shoulders" | "biceps" | "triceps" | "legs" | "core" | "cardio" | "other"
```

## Key Features

- **Progressive overload**: Double-progression system — build reps within a range, then add weight. Three modes (Chill/Manageable/Aggressive) control rep ranges and weight jumps.
- **Workout Score**: 0-100 score per session based on volume relative to personal bests.
- **Demo data**: "Load Demo Data" button on welcome screen seeds 52 weeks of realistic PPL training data (260 workouts, 43 exercises).
- **Animated background**: SVG bezier paths with flowing dash animation via Framer Motion, fixed behind all pages.

## Commands

```bash
npm run dev          # Start dev server
npm run build        # Production build
npx playwright test  # Run 13 automated tests
```
