# Routine Timer App

A mobile app for creating and running sequential timer routines — so you can set up a multi-step sequence once and reuse it every time.

---

## Why I built this

Most timer apps let you run one timer at a time. But a lot of real tasks involve multiple timed steps in a fixed sequence — and there's no good way to save that sequence and run it again later.

Every Sunday I follow the same slow cooker recipe: brown the meat for 10 minutes, add vegetables for 5 minutes, then slow cook for 4 hours. Every time I had to recreate those three timers from scratch. Same problem with my daughter's bedtime routine, and my morning workouts.

This app lets you build a **routine** — a named sequence of timers — and run it with one tap. Each timer counts down independently. When one finishes, you get an audio and haptic alert, then tap "Start Next" when you're ready to move on.

---

## What it does

- Create a routine with as many named timers as you need
- Save it and reuse it — create once, run forever
- Run a routine: timers play in sequence, each with its own countdown
- See your progress at a glance — colour-coded cards show which timers are done (green), active (yellow), and upcoming (white)
- Receive audio and haptic alerts when each timer completes
- Manually advance at your own pace — nothing moves forward until you're ready
- Edit or delete routines and timers at any time
- Data persists on-device across app restarts

---

## Screens

| # | Screen | Purpose |
|---|--------|---------|
| 1 | My Routines | Home screen — your saved routines library |
| 2 | Create Routine | Name a new routine and add its first timer |
| 3 | Routine Detail | View and manage all timers in a routine |
| 4 | Edit Routine | Rename or delete a routine |
| 5 | Edit Timer | Update a timer's label or duration |
| 6 | Add Timer | Add another timer to an existing routine |
| 7 | Running | Live countdown with colour-coded progress |
| 8 | Timer Done | Completion alert — advance to next or finish |

---

## Status

Currently in active development. See [TODO.md](TODO.md) for the full phase-by-phase build plan.

**Key documents:**
- [PRD.md](PRD.md) — problem statement, target users, success criteria, and scope
- [TODO.md](TODO.md) — phase-by-phase build plan and acceptance criteria
- [CLAUDE.md](CLAUDE.md) — architecture rules and development guidelines
- [docs/test-plan.md](docs/test-plan.md) — full list of 94 tests across all phases
- [Design/design_specification.md](Design/design_specification.md) — typography, spacing, colours, and screen layouts
- [Design/Button_states.md](Design/Button_states.md) — button state specifications

---

## Tech stack

- [React Native](https://reactnative.dev/) + [Expo](https://expo.dev/) (SDK 55)
- TypeScript (strict mode)
- React Navigation v7 (native stack)
- AsyncStorage (on-device persistence)
- expo-av (sound alerts)
- expo-haptics (vibration alerts)
- Jest + React Native Testing Library (unit and component tests)

---

## Running the app locally

**Prerequisites:** Node.js 18+, and either an iOS Simulator or Android Emulator.

> Note: This project targets Expo SDK 55. Use the iOS Simulator (`npm run ios`) rather than the Expo Go app on a physical device — Expo Go on the App Store does not yet support SDK 55.

```bash
# Install dependencies
npm install

# Run on iOS Simulator
npm run ios

# Run on Android Emulator
npm run android
```

---

## Running the tests

```bash
# Run all tests
npm test

# Watch mode
npm run test:watch
```
