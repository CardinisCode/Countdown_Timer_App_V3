# Routine Timer App

A mobile app for creating and running sequential timer routines — so you can set up a multi-step sequence once and reuse it every time.

---

## Why I built this

I find cooking stressful and overwhelming. I slow cook most of my meals, and most recipes need more than one timer running at different points — one for the meat, one to remind me to add an ingredient, another to start the rice or prepare a side dish. I cook dinner a couple of times a week, and every time I'd end up juggling multiple separate timers with no labels and no memory of which was which.

I also have a daughter who needs a 2-minute timer for brushing her teeth — split into sections so she knows when to move to the next part of her mouth.

What I actually needed wasn't more timers. It was a way to build a named sequence for each recipe or routine, save it, and just tap to run it next time. That's what this app does.

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
