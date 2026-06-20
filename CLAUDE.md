# CLAUDE.md — Countdown Timer App V3

Guidelines for Claude when working on this project.

---

## Project Overview

React Native / Expo app for creating and running sequential timer routines.

**Two core entities:**
- **Routine** — a saved, named sequence of timers (e.g. "Slow Cooker Sunday")
- **Timer** — an individual countdown step within a routine (e.g. "Brown meat — 10:00")

See `design/design_specification.md`, `design/Button_states.md`, and `ProjectOverview.md` for full design details.

---

## Mandatory: Test-Driven Development

**Always write failing tests before writing implementation code. No exceptions.**

Order for every piece of work:
1. Before writing any tests, read `docs/test-plan.md` and find the section for the current phase/file
2. Write the tests listed there — confirm they fail
3. Write the minimum code to make them pass
4. Confirm all tests pass before moving on

If asked to implement a feature, consult `docs/test-plan.md` first, then write the listed tests before any code. If asked to fix a bug, write a failing test that reproduces it first.

**`docs/test-plan.md` is the source of truth for what tests to write.** Do not invent new test cases or skip listed ones without discussion.

---

## Phase Structure

Work is broken into phases in the implementation plan (`docs/superpowers/plans/`). Each phase has:
- **Write Tests** — failing tests written first
- **Write Code** — implementation to pass the tests
- **Acceptance Criteria** — automated checks that must pass
- **Expo Go Manual Tests** — tasks for the user to verify in the iOS/Android Simulator

Complete phases in order. Do not start Phase N+1 until all acceptance criteria for Phase N pass.

---

## Architecture Rules

Layers are strictly separated. No exceptions.

| Layer | Path | Responsibility |
|---|---|---|
| Types | `src/types/index.ts` | Shared interfaces and pure utility functions. No React. |
| Engine | `src/engine/timer.ts` | Pure countdown logic. No React, no imports from react or react-native. |
| Hooks | `src/hooks/` | React hooks only. Wraps engine. No direct UI. |
| Context | `src/context/RoutineContext.tsx` | Global routine state + AsyncStorage. No business logic beyond CRUD. |
| Screens | `src/screens/` | UI only. Reads from hooks/context, renders UI. No business logic. |
| Navigation | `src/navigation/AppNavigator.tsx` | Stack navigator wiring only. |

---

## Screens (8 total)

| Screen | File | Route Name |
|---|---|---|
| My Routines | `MyRoutinesScreen.tsx` | `MyRoutines` |
| Create Routine | `CreateRoutineScreen.tsx` | `CreateRoutine` |
| Routine Detail | `RoutineDetailScreen.tsx` | `RoutineDetail` |
| Edit Routine | `EditRoutineScreen.tsx` | `EditRoutine` |
| Edit Timer | `EditTimerScreen.tsx` | `EditTimer` |
| Add Timer | `AddTimerScreen.tsx` | `AddTimer` |
| Running | `RunningScreen.tsx` | `Running` |
| Timer Done | `TimerDoneScreen.tsx` | `TimerDone` |

---

## Colour States (Running Screen)

| State | Colour | Hex |
|---|---|---|
| Completed | Green | `#c8f7c5` |
| Active | Yellow | `#fff9c4` |
| Upcoming | White / default | `#FFFFFF` |

All text on coloured backgrounds must be black (`#000000`).

---

## Validation Rules

| Field | Rule |
|---|---|
| Routine name | Required. Save disabled if empty. |
| Timer label | Optional. Auto-assign `Timer 1`, `Timer 2`... if empty. |
| Timer duration | Save disabled if hours + minutes + seconds all equal 0. |

---

## Input Handling (Critical — learned from V1)

**Store duration inputs as raw strings, not numbers.**
Parse to a number only when the value is needed for calculation or saving.
Using numbers as the `value` prop of a `TextInput` on iOS causes the field to fight the controlled value on each keystroke, making the field appear uneditable.

```tsx
// Correct
const [inputHours, setInputHours] = useState('');
<TextInput value={inputHours} onChangeText={(v) => setInputHours(v.replace(/[^0-9]/g, ''))} />

// Wrong — do not do this
const [hours, setHours] = useState(0);
<TextInput value={String(hours).padStart(2, '0')} />
```

---

## Reset Rule (Critical — learned from V1)

When calling `reset()` in any hook that holds an interval, always call `pause()` (or equivalent cleanup) before nullifying the ref. The underlying `setInterval` will keep running silently otherwise.

---

## Navigation Pattern for Running → Timer Done → Running

Use `navigation.replace()` (not `navigate` or `push`) when transitioning between Running and Timer Done screens. This prevents stack accumulation across multiple timers and ensures each screen mounts fresh with correct state.

---

## Dependency Versions

Do not upgrade dependencies without discussion. Pinned versions exist for a reason — react-native 0.83.4 must match Expo SDK 55.

| Package | Version |
|---|---|
| expo | ~55.0.14 |
| react | 19.2.5 |
| react-native | 0.83.4 |
| expo-status-bar | ~55.0.5 |
| expo-haptics | ~55.0.14 |
| expo-av | ~16.0.8 |
| @react-native-async-storage/async-storage | ~2.1.2 |
| @react-navigation/native | ^7.2.2 |
| @react-navigation/native-stack | ^7.14.10 |
| react-native-safe-area-context | ~5.6.2 |
| react-native-screens | ~4.23.0 |
| jest | ^29.7.0 |
| jest-expo | ~55.0.15 |
| @testing-library/react-native | ^13.3.3 |
| @types/jest | ~29.5.14 |
| @types/react | ~19.2.2 |
| react-test-renderer | 19.2.5 |
| typescript | ~5.9.2 |

---

## UX Principles

- Every decision must prioritise the user experience
- The user is often not watching the screen (cooking, brushing teeth) — alerts must be reliable
- Keyboard must appear automatically when the user taps any input field
- Colour states must be instantly readable at a glance
- Never disable a button without making it visually obvious why
- Minimum touch target: 44 × 44pt for all interactive elements

---

## Running Tests

```bash
npm test            # run all tests
npm run test:watch  # watch mode
```

## Running the App

```bash
npm run ios         # open in iOS Simulator
npm run android     # open in Android Emulator
```

---

## File Naming

- Screens: `PascalCase` + `Screen.tsx` suffix (e.g. `MyRoutinesScreen.tsx`)
- Tests: mirror source path under `__tests__/` with `.test.ts` or `.test.tsx`
- Hooks: `camelCase` with `use` prefix (e.g. `useTimer.ts`)
