# Test Plan — Countdown Timer App V3

All tests are written before implementation code (TDD). Each test file mirrors its source file path under `src/.../` → `src/.../__tests__/`.

Run all tests: `npm test`
Run a single file: `npm test -- --testPathPattern=<filename>`

---

## `src/__tests__/smoke.test.ts`

| # | Test | Purpose |
|---|------|---------|
| 1 | `true === true` | Verifies the test runner is configured and working |

---

## `src/engine/__tests__/timer.test.ts`

Tests for the pure countdown engine. No React, no mocks needed. Uses `jest.useFakeTimers()`.

| # | Test | Purpose |
|---|------|---------|
| 1 | Timer starts from the given duration | `onTick` is called with `duration - 1` after 1 second |
| 2 | Decrements correctly each second | Ticks produce [duration-1, duration-2, ..., 0] |
| 3 | Stops at zero and does not go negative | All tick values are ≥ 0 |
| 4 | `onComplete` fires when reaching zero | Callback called exactly once at the end |
| 5 | Pause freezes the countdown | No ticks after `pause()` is called |
| 6 | Resumes correctly after pause | Ticking continues from where it stopped |
| 7 | Reset returns to original duration | `getTimeRemaining()` returns original value after reset |
| 8 | Reset stops the running interval | No more ticks after `reset()` is called |
| 9 | `onComplete` fires again after reset and re-run | Callback fires on second run |
| 10 | Calling `start()` twice does not create two intervals | `onTick` called only once per second |

---

## `src/hooks/__tests__/useTimer.test.ts`

Tests for the React hook wrapping the timer engine. Uses `renderHook` and `jest.useFakeTimers()`.

| # | Test | Purpose |
|---|------|---------|
| 1 | Exposes correct initial state | `timeRemaining` = duration, `isRunning` = false, `isComplete` = false |
| 2 | `start()` sets `isRunning` to true and begins countdown | `isRunning` becomes true, `timeRemaining` decrements |
| 3 | `pause()` freezes `timeRemaining` and sets `isRunning` to false | Time does not change after pause |
| 4 | `reset()` restores original duration, `isRunning`, and `isComplete` | All state returns to initial values |
| 5 | `isComplete` becomes true when timer reaches zero | `isComplete` = true, `isRunning` = false |
| 6 | `isComplete` resets to false after `reset()` | State is clean after reset |
| 7 | `reset()` stops the interval (no ticks after reset) | `timeRemaining` does not change after reset |

---

## `src/hooks/__tests__/useTimerSequence.test.ts`

Tests for the sequence state hook. Uses `renderHook`.

| # | Test | Purpose |
|---|------|---------|
| 1 | First timer starts as `active` | `items[0].state === 'active'` |
| 2 | All other timers start as `upcoming` | `items[1+].state === 'upcoming'` |
| 3 | `activeIndex` starts at 0 | Initial value is 0 |
| 4 | `advanceToNext()` moves active index forward | `activeIndex` becomes 1 |
| 5 | Previous timer becomes `completed` after advance | `items[0].state === 'completed'` after first advance |
| 6 | `isLastTimer` is false for first timer | False when multiple timers exist |
| 7 | `isLastTimer` is true when on the final timer | True after advancing to last position |
| 8 | `advanceToNext()` does not go past the last timer | `activeIndex` stays at `timers.length - 1` |
| 9 | `initialIndex` param sets starting position | Starts at index 1 when `initialIndex = 1` is passed; index 0 is `completed` |

---

## `src/context/__tests__/RoutineContext.test.tsx`

Tests for the global state and AsyncStorage layer. Mocks `AsyncStorage`.

| # | Test | Purpose |
|---|------|---------|
| 1 | Starts with empty routines list | `routines` is `[]` on first mount |
| 2 | `addRoutine()` creates a routine with name and first timer | Correct name and timer in state |
| 3 | `addRoutine()` persists to AsyncStorage | `AsyncStorage.setItem` called with serialised data |
| 4 | Loads routines from AsyncStorage on mount | Pre-stored JSON is parsed and loaded |
| 5 | `updateRoutineName()` changes the routine name | Correct name in state after update |
| 6 | `deleteRoutine()` removes the routine | Routine no longer in `routines` list |
| 7 | `addTimer()` appends a timer to the routine | Timer appears at end of `routine.timers` |
| 8 | `updateTimer()` changes label and duration | Correct values in state after update |
| 9 | `deleteTimer()` removes a timer from the routine | Timer no longer in `routine.timers` |
| 10 | `deleteTimer()` on the last timer deletes the entire routine | `routines` is empty; routine removed |
| 11 | `getRoutine()` returns the correct routine by id | Returns matching routine object |

---

## `src/screens/__tests__/MyRoutinesScreen.test.tsx`

Tests for Screen 1. Mocks `useRoutines`.

| # | Test | Purpose |
|---|------|---------|
| 1 | Renders "My Routines" heading | Title text visible |
| 2 | Shows empty state message when no routines exist | "No routines yet" message visible |
| 3 | Shows "Add Routine" button | CTA button visible |
| 4 | Tapping "Add Routine" navigates to CreateRoutine | `navigation.navigate('CreateRoutine')` called |
| 5 | Renders routine name when routines exist | Routine name visible in list |
| 6 | Shows timer count and total duration on routine card | "2 timers · 08:00" format visible |
| 7 | Tapping a routine card navigates to RoutineDetail | `navigation.navigate('RoutineDetail', { routineId })` called |
| 8 | Empty state is hidden when routines exist | "No routines yet" message not present |

---

## `src/screens/__tests__/CreateRoutineScreen.test.tsx`

Tests for Screen 2. Mocks `useRoutines`.

| # | Test | Purpose |
|---|------|---------|
| 1 | Renders routine name input with correct placeholder | "e.g., Slow Cooker Sunday" placeholder visible |
| 2 | Renders timer label input with correct placeholder | "e.g., Brown meat" placeholder visible |
| 3 | Renders hours, minutes, seconds inputs | Three inputs with "00" placeholder |
| 4 | Save does nothing when routine name is empty | `addRoutine` not called |
| 5 | Save does nothing when duration is 0:00:00 | `addRoutine` not called |
| 6 | Save creates routine and navigates to RoutineDetail | `addRoutine` called; `navigate('RoutineDetail', ...)` called |
| 7 | Empty timer label defaults to "Timer 1" on save | `addRoutine` called with `label: 'Timer 1'` |

---

## `src/screens/__tests__/RoutineDetailScreen.test.tsx`

Tests for Screen 3. Mocks `useRoutines`.

| # | Test | Purpose |
|---|------|---------|
| 1 | Renders routine name as heading | Name text visible |
| 2 | Renders total duration | Formatted total duration visible |
| 3 | Renders all timer labels | Each timer label visible in list |
| 4 | Renders "Start Routine" button | CTA button visible |
| 5 | Renders "+ Add Timer" button | Add timer button visible |
| 6 | Tapping "Start Routine" navigates to Running | `navigate('Running', { routineId })` called |
| 7 | Tapping "+ Add Timer" navigates to AddTimer | `navigate('AddTimer', { routineId })` called |
| 8 | Tapping routine name navigates to EditRoutine | `navigate('EditRoutine', { routineId })` called |
| 9 | Tapping edit icon on a timer navigates to EditTimer | `navigate('EditTimer', { routineId, timerId })` called |

---

## `src/screens/__tests__/EditRoutineScreen.test.tsx`

Tests for Screen 4. Mocks `useRoutines`.

| # | Test | Purpose |
|---|------|---------|
| 1 | Input is pre-filled with current routine name | `getByDisplayValue('Old Name')` finds the input |
| 2 | Save updates routine name and goes back | `updateRoutineName` called; `goBack()` called |
| 3 | Save does nothing when name is empty | `updateRoutineName` not called |
| 4 | Cancel goes back without saving | `updateRoutineName` not called; `goBack()` called |
| 5 | "Delete Routine" button is visible | Button text visible |

---

## `src/screens/__tests__/EditTimerScreen.test.tsx`

Tests for Screen 5. Mocks `useRoutines`.

| # | Test | Purpose |
|---|------|---------|
| 1 | Label field is pre-filled with current timer label | `getByDisplayValue('Brown meat')` finds the input |
| 2 | Duration fields are pre-filled with current values | Minutes field shows "10" |
| 3 | Save updates timer and goes back | `updateTimer` called; `goBack()` called |
| 4 | Save does nothing when duration is 0:00:00 | `updateTimer` not called |
| 5 | Cancel goes back without saving | `updateTimer` not called; `goBack()` called |
| 6 | "Delete Timer" button is visible | Button text visible |

---

## `src/screens/__tests__/AddTimerScreen.test.tsx`

Tests for Screen 6. Mocks `useRoutines`.

| # | Test | Purpose |
|---|------|---------|
| 1 | Renders timer label input with placeholder | "e.g., Add sauce" placeholder visible |
| 2 | Renders hours, minutes, seconds inputs | Three inputs with "00" placeholder |
| 3 | "Save & Continue" does nothing when duration is 0:00:00 | `addTimer` not called |
| 4 | "Save & Continue" saves timer and returns to Routine Detail | `addTimer` called; `goBack()` called |
| 5 | Empty label auto-assigns "Timer 2" when one timer exists | `addTimer` called with `label: 'Timer 2'` |

---

## `src/screens/__tests__/RunningScreen.test.tsx`

Tests for Screen 7. Mocks `useRoutines`, uses `jest.useFakeTimers()`.

| # | Test | Purpose |
|---|------|---------|
| 1 | Renders routine name | Name text visible |
| 2 | Renders total running time starting at "00:00" | Elapsed counter starts at zero |
| 3 | Renders all timer labels | All labels visible |
| 4 | Active timer card has yellow background (`#fff9c4`) | First card background colour correct |
| 5 | Upcoming timer cards have white background (`#FFFFFF`) | Subsequent card background colour correct |
| 6 | Completed timer cards have green background (`#c8f7c5`) | After advance, completed card background correct |
| 7 | Renders "Pause" button | Pause button visible |
| 8 | Renders "Reset" button | Reset button visible |
| 9 | "Pause" changes to "Resume" when tapped | Button label changes on press |
| 10 | Navigates to TimerDone when active timer reaches zero | `navigation.replace('TimerDone', { routineId, completedTimerIndex, totalTimers })` called |

---

## `src/screens/__tests__/TimerDoneScreen.test.tsx`

Tests for Screen 8. Mocks `useRoutines`, `expo-av`, `expo-haptics`.

| # | Test | Purpose |
|---|------|---------|
| 1 | Shows "[Timer label] complete!" (non-last timer) | Correct message when more timers remain |
| 2 | Shows "Start Next" button (non-last timer) | CTA label correct |
| 3 | "Start Next" replaces with Running for next timer | `navigation.replace('Running', { routineId, startAtIndex: nextIndex })` called |
| 4 | Shows "Routine complete! 🎉" (last timer) | Correct message on last timer |
| 5 | Shows "Finish" button (last timer) | CTA label changes to "Finish" |
| 6 | "Finish" navigates to My Routines | `navigation.navigate('MyRoutines')` called |

---

## Test Count Summary

| File | Tests |
|------|-------|
| `smoke.test.ts` | 1 |
| `timer.test.ts` (engine) | 10 |
| `useTimer.test.ts` | 7 |
| `useTimerSequence.test.ts` | 9 |
| `RoutineContext.test.tsx` | 11 |
| `MyRoutinesScreen.test.tsx` | 8 |
| `CreateRoutineScreen.test.tsx` | 7 |
| `RoutineDetailScreen.test.tsx` | 9 |
| `EditRoutineScreen.test.tsx` | 5 |
| `EditTimerScreen.test.tsx` | 6 |
| `AddTimerScreen.test.tsx` | 5 |
| `RunningScreen.test.tsx` | 10 |
| `TimerDoneScreen.test.tsx` | 6 |
| **Total** | **94** |
