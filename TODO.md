# Countdown Timer App V3 — Project TODO

Each phase follows this order:
1. Write failing tests
2. Write code to make tests pass
3. Testing (agent) — automated: `npm test`, TypeScript check, spec compliance
4. Expo Go manual tests — you verify in the simulator
5. Acceptance criteria — checked last, after both above pass

---

## Phase 1 — Project Scaffolding ⬜

### Write Tests
- [ ] Smoke test: app renders without crashing (`src/__tests__/smoke.test.ts`)

### Write Code
- [ ] Create `package.json` with correct dependency versions (see `CLAUDE.md`)
- [ ] Create `tsconfig.json`, `app.json`, `jest.config.js`
- [ ] Create `index.ts` and `App.tsx`
- [ ] Create folder structure: `src/types`, `src/engine`, `src/hooks`, `src/context`, `src/screens`, `src/navigation`
- [ ] Create `src/navigation/AppNavigator.tsx` with all 8 screens wired in a stack navigator
- [ ] Create placeholder screen components for all 8 screens
- [ ] Wrap `App.tsx` in `SafeAreaProvider`
- [ ] Run `npm install`

### Testing (Agent)
- [ ] All tests pass (`npm test` — 1/1)
- [ ] No TypeScript errors (`npx tsc --noEmit`)

### Expo Go Manual Tests
- [ ] Run `npm run ios`
- [ ] Confirm app opens without a crash
- [ ] Confirm "My Routines" header is visible

### Acceptance Criteria
- [ ] App launches in iOS Simulator without crashing
- [ ] User sees a screen titled "My Routines"

---

## Phase 2 — Types & Data Models ⬜

### Write Tests
- [ ] No tests needed (pure types) — TypeScript check serves as verification

### Write Code
- [ ] Create `src/types/index.ts` with:
  - `RoutineTimer` interface (id, label, hours, minutes, seconds)
  - `Routine` interface (id, name, timers[], createdAt)
  - `timerDurationSeconds()` utility function
  - `routineTotalSeconds()` utility function
  - `formatDuration()` utility function
  - `formatCountdown()` utility function
  - `nextTimerLabel()` utility function

### Testing (Agent)
- [ ] No TypeScript errors (`npx tsc --noEmit`)

### Acceptance Criteria
- [ ] All interfaces and utility functions are typed correctly

---

## Phase 3 — Timer Engine ⬜

### Write Tests (`src/engine/__tests__/timer.test.ts`)
- [ ] Timer starts from the given duration
- [ ] Timer ticks down by 1 each second
- [ ] Timer stops at zero and does not go negative
- [ ] `onComplete` fires when timer reaches zero
- [ ] Pause freezes the countdown
- [ ] Timer resumes correctly after pause
- [ ] Reset returns to original duration
- [ ] Reset stops the running interval (no ticks after reset)
- [ ] `onComplete` fires again after reset and re-run
- [ ] Calling `start()` twice does not create two intervals

### Write Code (`src/engine/timer.ts`)
- [ ] Implement `createTimer({ duration, onTick, onComplete })`
- [ ] Implement `start()` — begin countdown via `setInterval`
- [ ] Implement `pause()` — clear interval
- [ ] Implement `reset()` — call pause first, then restore duration
- [ ] Implement `getTimeRemaining()`

### Testing (Agent)
- [ ] All engine tests pass (10 tests)
- [ ] No TypeScript errors

### Acceptance Criteria
- [ ] A timer started at a given duration counts down correctly each second
- [ ] A timer that reaches zero does not continue below zero
- [ ] A paused timer does not continue counting down
- [ ] A resumed timer continues from where it paused
- [ ] A reset timer returns to its original starting duration

---

## Phase 4 — useTimer Hook ⬜

### Write Tests (`src/hooks/__tests__/useTimer.test.ts`)
- [ ] Exposes correct initial state (`timeRemaining`, `isRunning`, `isComplete`)
- [ ] `start()` sets `isRunning` to true and begins countdown
- [ ] `pause()` freezes `timeRemaining` and sets `isRunning` to false
- [ ] `reset()` restores original duration, `isRunning`, and `isComplete`
- [ ] `isComplete` becomes true when timer reaches zero
- [ ] `isComplete` resets to false after `reset()`
- [ ] `reset()` stops the interval (no ticks after reset)

### Write Code (`src/hooks/useTimer.ts`)
- [ ] Implement `useTimer(durationSeconds: number)`
- [ ] Wire `setInterval` to engine tick via `createTimer`
- [ ] Expose controls: `start`, `pause`, `reset`
- [ ] Expose state: `timeRemaining`, `isRunning`, `isComplete`

### Testing (Agent)
- [ ] All hook tests pass (7 tests)
- [ ] No TypeScript errors

### Acceptance Criteria
- [ ] A timer started via the hook counts down correctly in a React component
- [ ] A paused timer holds its remaining time until resumed
- [ ] A reset timer displays its original duration again

---

## Phase 5 — useTimerSequence Hook ⬜

### Write Tests (`src/hooks/__tests__/useTimerSequence.test.ts`)
- [ ] First timer starts as `active`
- [ ] All other timers start as `upcoming`
- [ ] `activeIndex` starts at 0
- [ ] `advanceToNext()` moves active index forward
- [ ] Previous timer becomes `completed` after advance
- [ ] `isLastTimer` is false for first timer in a multi-timer routine
- [ ] `isLastTimer` is true when on the final timer
- [ ] `advanceToNext()` does not go past the last timer
- [ ] `initialIndex` param sets starting position correctly

### Write Code (`src/hooks/useTimerSequence.ts`)
- [ ] Implement `useTimerSequence(timers, initialIndex?)`
- [ ] Derive `items` array with `state` ('completed' | 'active' | 'upcoming') for each timer
- [ ] Implement `advanceToNext()`
- [ ] Compute `isLastTimer`

### Testing (Agent)
- [ ] All hook tests pass (8 tests)
- [ ] No TypeScript errors

### Acceptance Criteria
- [ ] Active timer state is correctly tracked as user advances through a routine

---

## Phase 6 — RoutineContext ⬜

### Write Tests (`src/context/__tests__/RoutineContext.test.tsx`)
- [ ] Starts with empty routines list
- [ ] `addRoutine()` creates a routine with the given name and first timer
- [ ] `addRoutine()` persists to AsyncStorage
- [ ] Routines are loaded from AsyncStorage on app mount
- [ ] `updateRoutineName()` changes the routine name
- [ ] `deleteRoutine()` removes the routine
- [ ] `addTimer()` appends a timer to the routine
- [ ] `updateTimer()` changes label and duration
- [ ] `deleteTimer()` removes a timer from the routine
- [ ] `deleteTimer()` on the last timer deletes the entire routine
- [ ] `getRoutine()` returns the correct routine by id

### Write Code
- [ ] Create `src/context/RoutineContext.tsx`
- [ ] Implement `RoutineProvider` component
- [ ] Implement `useRoutines()` hook
- [ ] Load routines from AsyncStorage on mount (`useEffect`)
- [ ] Persist routines on every mutation
- [ ] Update `App.tsx` — wrap in `<RoutineProvider>`

### Testing (Agent)
- [ ] All context tests pass (11 tests)
- [ ] No TypeScript errors
- [ ] Full test suite passes

### Acceptance Criteria
- [ ] Routine data persists across app restarts
- [ ] All CRUD operations (add, read, update, delete) work correctly

---

## Phase 7 — My Routines Screen (Screen 1) ⬜

### Write Tests (`src/screens/__tests__/MyRoutinesScreen.test.tsx`)
- [ ] Renders "My Routines" heading
- [ ] Shows empty state message when no routines exist
- [ ] Shows "Add Routine" button
- [ ] Tapping "Add Routine" navigates to Create Routine screen
- [ ] Renders routine name when routines exist
- [ ] Shows timer count and total duration on routine card
- [ ] Tapping a routine card navigates to Routine Detail
- [ ] Empty state is hidden when routines exist

### Write Code (`src/screens/MyRoutinesScreen.tsx`)
- [ ] Render "My Routines" title
- [ ] Render `FlatList` of routine cards (name + timer count + total duration)
- [ ] Render empty state message when list is empty
- [ ] "Add Routine" CTA button pinned at bottom
- [ ] Long-press on card triggers delete confirmation dialog
- [ ] Navigate to `RoutineDetail` on card tap
- [ ] Navigate to `CreateRoutine` on Add Routine tap

### Testing (Agent)
- [ ] All screen tests pass (8 tests)
- [ ] No TypeScript errors

### Expo Go Manual Tests
- [ ] Confirm "My Routines" heading visible
- [ ] Confirm empty state message visible on first launch
- [ ] Confirm "Add Routine" button visible at bottom
- [ ] Tap "Add Routine" — confirm navigates to Create Routine screen
- [ ] Create a routine, return to home — confirm routine listed with name, count, duration

### Acceptance Criteria
- [ ] When no routines exist, user sees a helpful empty state message
- [ ] User can see "Add Routine" button at all times
- [ ] When routines exist, each is listed with name and total duration
- [ ] User can tap a routine card to view its details

---

## Phase 8 — Create Routine Screen (Screen 2) ⬜

### Write Tests (`src/screens/__tests__/CreateRoutineScreen.test.tsx`)
- [ ] Renders routine name input with correct placeholder
- [ ] Renders timer label input with correct placeholder
- [ ] Renders hours, minutes, seconds inputs (all with "00" placeholder)
- [ ] Save does nothing when routine name is empty
- [ ] Save does nothing when duration is 0:00:00
- [ ] Save creates routine and navigates to Routine Detail
- [ ] Empty timer label defaults to "Timer 1" on save

### Write Code (`src/screens/CreateRoutineScreen.tsx`)
- [ ] Routine name `TextInput` (required, auto-focus)
- [ ] Timer label `TextInput` (optional)
- [ ] Hours / minutes / seconds `TextInput` fields (numeric keyboard, stored as strings)
- [ ] "Save" CTA — disabled if name empty or duration is zero
- [ ] On save: call `addRoutine()`, navigate to `RoutineDetail`
- [ ] Empty label defaults to "Timer 1"

### Testing (Agent)
- [ ] All screen tests pass (7 tests)
- [ ] No TypeScript errors

### Expo Go Manual Tests
- [ ] Tap "Add Routine" → confirm Create Routine screen opens with keyboard focused
- [ ] Tap duration field → confirm numeric keyboard appears
- [ ] Leave name empty, enter duration → confirm Save has no effect
- [ ] Leave duration at 0:00:00, enter name → confirm Save has no effect
- [ ] Leave label blank → confirm defaults to "Timer 1" after saving
- [ ] Fill name + duration → confirm Save navigates to Routine Detail

### Acceptance Criteria
- [ ] User can give their routine a name
- [ ] User can set a label and duration for the first timer
- [ ] If label is left blank, a default label is assigned automatically ("Timer 1")
- [ ] User cannot save with an empty name or zero duration
- [ ] After saving, user is taken to Routine Detail showing the new routine

---

## Phase 9 — Routine Detail Screen (Screen 3) ⬜

### Write Tests (`src/screens/__tests__/RoutineDetailScreen.test.tsx`)
- [ ] Renders routine name as heading
- [ ] Renders total duration
- [ ] Renders all timer labels
- [ ] Renders "Start Routine" button
- [ ] Renders "+ Add Timer" button
- [ ] Tapping "Start Routine" navigates to Running screen
- [ ] Tapping "+ Add Timer" navigates to Add Timer screen
- [ ] Tapping routine name navigates to Edit Routine screen
- [ ] Tapping edit icon on a timer navigates to Edit Timer screen

### Write Code (`src/screens/RoutineDetailScreen.tsx`)
- [ ] Render routine name as tappable heading (→ Edit Routine)
- [ ] Render total duration below heading
- [ ] Render scrollable list of timers (label + duration + edit icon + delete icon)
- [ ] Delete icon triggers confirmation dialog (handles "last timer" special case)
- [ ] "+ Add Timer" button → navigates to Add Timer
- [ ] "Start Routine" CTA button → navigates to Running

### Testing (Agent)
- [ ] All screen tests pass (9 tests)
- [ ] No TypeScript errors

### Expo Go Manual Tests
- [ ] Create routine → confirm Routine Detail shows name, total duration, all timers
- [ ] Confirm "Start Routine" and "+ Add Timer" buttons visible
- [ ] Tap routine name → confirm navigates to Edit Routine screen
- [ ] Tap edit icon on a timer → confirm navigates to Edit Timer screen
- [ ] Tap delete icon on a non-last timer → confirm dialog appears → timer removed
- [ ] Tap delete icon on last timer → confirm special warning dialog appears

### Acceptance Criteria
- [ ] User can see their routine's name and all timers listed with durations
- [ ] User can see the total combined duration of all timers
- [ ] User can add more timers to the routine
- [ ] User can start the routine from this screen
- [ ] User can edit or delete individual timers

---

## Phase 10 — Edit Routine Screen (Screen 4) ⬜

### Write Tests (`src/screens/__tests__/EditRoutineScreen.test.tsx`)
- [ ] Input is pre-filled with current routine name
- [ ] Save updates routine name and goes back
- [ ] Save does nothing when name is empty
- [ ] Cancel goes back without saving
- [ ] "Delete Routine" button is visible

### Write Code (`src/screens/EditRoutineScreen.tsx`)
- [ ] Pre-filled routine name `TextInput`
- [ ] "Save" CTA — disabled if name is empty
- [ ] "Cancel" secondary button → go back
- [ ] "Delete Routine" destructive button → confirmation dialog → delete and navigate to My Routines

### Testing (Agent)
- [ ] All screen tests pass (5 tests)
- [ ] No TypeScript errors

### Expo Go Manual Tests
- [ ] Tap routine name on Routine Detail → confirm Edit Routine screen opens with name pre-filled
- [ ] Change name → Save → confirm updated on Routine Detail
- [ ] Clear name → confirm Save is disabled
- [ ] Tap Cancel → confirm no changes made
- [ ] Tap "Delete Routine" → confirm dialog → routine removed → back on My Routines

### Acceptance Criteria
- [ ] User can rename a routine
- [ ] User cannot save an empty routine name
- [ ] User can delete the entire routine (with confirmation)

---

## Phase 11 — Edit Timer Screen (Screen 5) & Add Timer Screen (Screen 6) ⬜

### Write Tests — Edit Timer (`src/screens/__tests__/EditTimerScreen.test.tsx`)
- [ ] Label field is pre-filled with current timer label
- [ ] Duration fields are pre-filled with current timer values
- [ ] Save updates timer and goes back
- [ ] Save does nothing when duration is 0:00:00
- [ ] Cancel goes back without saving
- [ ] "Delete Timer" button is visible

### Write Tests — Add Timer (`src/screens/__tests__/AddTimerScreen.test.tsx`)
- [ ] Renders timer label input with placeholder
- [ ] Renders hours, minutes, seconds inputs
- [ ] "Save & Continue" does nothing when duration is 0:00:00
- [ ] "Save & Continue" saves timer and returns to Routine Detail
- [ ] Empty label auto-assigns next label (e.g. "Timer 2")

### Write Code (`src/screens/EditTimerScreen.tsx`)
- [ ] Pre-filled label and duration fields
- [ ] "Save" CTA — disabled if duration is zero
- [ ] "Cancel" secondary button → go back
- [ ] "Delete Timer" destructive button → handles normal delete and last-timer special case

### Write Code (`src/screens/AddTimerScreen.tsx`)
- [ ] Timer label `TextInput` (optional, auto-focus)
- [ ] Hours / minutes / seconds `TextInput` fields
- [ ] "Save & Continue" CTA — disabled if duration is zero
- [ ] On save: call `addTimer()`, go back to Routine Detail
- [ ] Empty label defaults to next auto-increment label

### Testing (Agent)
- [ ] All Edit Timer tests pass (6 tests)
- [ ] All Add Timer tests pass (5 tests)
- [ ] No TypeScript errors

### Expo Go Manual Tests
- [ ] Tap edit icon → Edit Timer screen shows pre-filled label and duration
- [ ] Change values → Save → confirm updated on Routine Detail
- [ ] Tap Delete Timer (non-last) → confirmation dialog → timer removed
- [ ] Tap Delete Timer (last) → special warning about deleting routine → navigates to My Routines
- [ ] Tap "+ Add Timer" → Add Timer screen → enter duration → Save & Continue → timer in list
- [ ] Leave label blank on Add Timer → confirm auto-label assigned

### Acceptance Criteria
- [ ] User can edit a timer's label and duration
- [ ] User cannot save a timer with zero duration
- [ ] User can delete a timer (with confirmation)
- [ ] Deleting the last timer in a routine also deletes the routine
- [ ] User can add new timers to an existing routine
- [ ] Auto-label increments correctly ("Timer 2", "Timer 3", etc.)

---

## Phase 12 — Running Screen (Screen 7) ⬜

### Write Tests (`src/screens/__tests__/RunningScreen.test.tsx`)
- [ ] Renders routine name
- [ ] Renders total running time starting at "00:00"
- [ ] Renders all timer labels
- [ ] Active timer card has yellow background (`#fff9c4`)
- [ ] Upcoming timer cards have white background (`#FFFFFF`)
- [ ] Completed timer cards have green background (`#c8f7c5`)
- [ ] Renders "Pause" button
- [ ] Renders "Reset" button
- [ ] "Pause" button changes to "Resume" when tapped
- [ ] Navigates to Timer Done when active timer reaches zero

### Write Code (`src/screens/RunningScreen.tsx`)
- [ ] Render routine name and elapsed total time (counting up)
- [ ] Render scrollable list of timer cards with colour-coded backgrounds
- [ ] Active timer shows large countdown (48pt)
- [ ] Completed timers show checkmark and original duration (muted)
- [ ] Upcoming timers show original duration (muted)
- [ ] Countdown starts automatically on mount
- [ ] Pause/Resume button toggles countdown and elapsed counter
- [ ] Reset button restores active timer to full duration
- [ ] Navigate to Timer Done (via `navigation.replace`) when timer hits zero
- [ ] Intercept back button with "End Routine?" confirmation dialog
- [ ] Use `startAtIndex` route param to start from correct timer (for multi-timer sequences)

### Testing (Agent)
- [ ] All screen tests pass (9 tests)
- [ ] No TypeScript errors

### Expo Go Manual Tests
- [ ] Create routine with 2+ short timers → Start Routine
- [ ] Confirm first timer is yellow (active) with large countdown
- [ ] Confirm remaining timers are white (upcoming)
- [ ] Confirm total running time counts up from 0
- [ ] Tap Pause → countdown freezes, button changes to "Resume"
- [ ] Tap Resume → countdown continues
- [ ] Tap Reset → active timer resets to full duration
- [ ] Let timer reach 0:00 → confirm navigates to Timer Done screen
- [ ] Press back during routine → confirm "End Routine?" dialog appears

### Acceptance Criteria
- [ ] User can see which timer is currently active (yellow background)
- [ ] User can see which timers have been completed (green background)
- [ ] User can see which timers are still to come (white background)
- [ ] User can pause and resume the active timer
- [ ] User can reset the active timer to its full duration
- [ ] When a timer finishes, user is taken to the Timer Done screen automatically

---

## Phase 13 — Timer Done Screen (Screen 8) ⬜

### Write Tests (`src/screens/__tests__/TimerDoneScreen.test.tsx`)
- [ ] Shows "[Timer label] complete!" message (non-last timer)
- [ ] Shows "Start Next" button (non-last timer)
- [ ] "Start Next" replaces screen with Running screen for next timer
- [ ] Shows "Routine complete! 🎉" message (last timer)
- [ ] Shows "Finish" button (last timer)
- [ ] "Finish" navigates to My Routines

### Write Code (`src/screens/TimerDoneScreen.tsx`)
- [ ] Trigger `expo-haptics` success notification on mount
- [ ] Trigger `expo-av` alert sound on mount (best-effort, catches errors)
- [ ] Show large checkmark icon
- [ ] Show "[Timer label] complete!" or "Routine complete! 🎉" based on whether last timer
- [ ] "Start Next" button (non-last) → `navigation.replace('Running', { routineId, startAtIndex: nextIndex })`
- [ ] "Finish" button (last) → `navigation.navigate('MyRoutines')`
- [ ] Add `assets/alert.mp3` sound file

### Testing (Agent)
- [ ] All screen tests pass (6 tests)
- [ ] No TypeScript errors

### Expo Go Manual Tests
- [ ] Let a timer finish → confirm Timer Done screen appears
- [ ] Confirm sound plays (check simulator audio is on)
- [ ] Confirm "[Timer label] complete!" message shown
- [ ] Tap "Start Next" → confirm back to Running with next timer active (yellow)
- [ ] Complete all timers → confirm "Routine complete! 🎉" and "Finish" button shown
- [ ] Tap "Finish" → confirm navigates to My Routines

### Acceptance Criteria
- [ ] User is alerted with sound and vibration when a timer finishes
- [ ] User can see which timer just completed
- [ ] User can manually start the next timer at their own pace
- [ ] When the last timer finishes, "Start Next" is replaced by "Finish"
- [ ] After finishing, user is returned to My Routines

---

## Phase 14 — Final QA & Polish ⬜

### Full Test Suite
- [ ] Run `npm test` — all tests pass, zero failures
- [ ] Run `npx tsc --noEmit` — no TypeScript errors

### Full Flow Test (Slow Cooker Sunday scenario)
- [ ] Create routine "Slow Cooker Sunday"
- [ ] Add timer: "Brown meat" — 10 min
- [ ] Add timer: "Add vegetables" — 5 min
- [ ] Add timer: "Slow cook" — 1 hr
- [ ] Confirm total duration shows 1:15:00
- [ ] Start routine, complete all timers end-to-end
- [ ] Confirm "Routine complete! 🎉" at the end
- [ ] Confirm routine still listed on My Routines after finishing

### Persistence Test
- [ ] Create a routine with 2 timers
- [ ] Force-close the app in the simulator
- [ ] Reopen app → confirm routines are still listed
- [ ] Tap routine → confirm all timers still intact

### Edit Flow Test
- [ ] Tap routine name → Edit Routine → change name → Save → confirm updated
- [ ] Tap edit icon on timer → change duration → Save → confirm updated in list
- [ ] Delete a timer (non-last) → confirm timer removed, routine still exists
- [ ] Delete last timer → confirm routine also deleted, navigated to My Routines
- [ ] Delete routine from Edit Routine screen → confirm removed from My Routines

### Edge Cases
- [ ] Create routine with empty name → Save has no effect
- [ ] Create routine with 0:00:00 duration → Save has no effect
- [ ] Run routine → press back → "End Routine?" dialog → End Routine → back on My Routines
- [ ] Single-timer routine runs to completion → "Routine complete! 🎉" → Finish → My Routines

### MVP Acceptance Criteria (from ProjectOverview.md)
- [ ] User can create a routine with multiple named timers
- [ ] User can save a routine and see it listed on the home screen
- [ ] User can edit timer labels and durations within a routine
- [ ] User can delete entire routines from the home screen
- [ ] User can start a saved routine
- [ ] Each timer in the sequence runs independently and accurately
- [ ] User receives audio + haptic alerts when each timer completes
- [ ] User manually advances to the next timer via "Start Next" button
- [ ] User can complete an entire routine and return to home
- [ ] Saved routines persist across app restarts (local storage only — no cloud sync in MVP)
- [ ] App runs successfully in iOS Simulator
- [ ] App runs successfully in Android Emulator
