# Project Overview

## Problem Statement (What)

- People performing multi-step tasks need timed reminders at each phase, but existing timer apps don't let them group related timers into reusable routines.

### Current pain points:

- **Can't group related timers as a routine**
    - Even though iOS saves individual timers, you can't save multiple related timers together (e.g., "Slow Cooker Sunday" with 3 different timings). 
    - Each time you cook the same recipe, you recreate the same 3 timers.
- **Can't pre-configure routines in advance**
    - You can't set up a timer routine the night before to be ready when you need it. 
    - You have to configure it right when you're about to start the task.
- **No visual progress tracking through sequences**
    - You have to constantly watch the timer to know when to switch tasks and where you are in a multi-step routine. 
    - Example: When brushing your daughter's teeth, you have to keep checking the timer to know when 30 seconds is up to switch quadrants. 
    - There's no visual indicator showing "Step 2 of 4" or which steps are done vs. upcoming.

### Example scenarios:

- **Home cook:** 
    - Following a slow cooker recipe with 3 distinct timing phases (brown meat 10 min, add veg 5 min, slow cook 4 hours)
    - has to recreate these timers every Sunday
- **Parent:** 
    - Brushing daughter's teeth using proper 2-minute routine (4 × 30-second quadrants) 
    — has to constantly watch timer to know when to switch or set 4 separate timers
- **Parent with bedtime routine:** 
    - Bath (15 min), story time (10 min), quiet time (5 min) 
    — recreates the same sequence every night
- **Athlete:** 
    - Running interval training routine (warm-up 5 min, sprint 2 min, rest 1 min × 5 rounds) 
    — recreates the same pattern every workout

## Target Users (Who)

### Primary: 

- Anyone who regularly performs multi-step tasks that require timed phases.

### User archetypes:

- **Home cooks** 
    — Following recipes with multiple timed steps
- **Fitness enthusiasts** 
    — Interval training, HIIT workouts, stretching routines
- **Parents** 
    — Managing structured routines (bedtime, morning prep, homework time)
- **People with ADHD/executive function challenges** 
    — Need external structure for task sequences
    - Need minimal strain on executive functioning
- **Professionals** 
    — Pomodoro technique users, meeting facilitators running timed agenda segments

### Common traits:

- Perform the same multi-step sequences repeatedly
- Need hands-free operation (often cooking, exercising, or busy with kids)
- Value consistency and routine
- Want to focus on the task, not managing timers

## Product Concept (What problem)

A mobile app that lets users create, save, and run sequential timer routines where each step has a name and duration, and the user manually controls progression through the sequence.

### Core Concept

A Routine is a saved sequence of named Timers.

Each Timer in the sequence:
- **Has a label**
    - Examples: "Brown meat", "Add vegetables", "Slow cook"
- **Has a duration**
    - Examples:  hours, minutes, seconds
- **Runs as an independent countdown**

### User Flow

#### Setup (once): 
User creates a routine and adds timers to it

- Example: "Slow Cooker Sunday" routine with 3 timers
- Timer 1: "Brown meat" — 10 minutes
- Timer 2: "Add vegetables" — 5 minutes
- Timer 3: "Slow cook" — 4 hours
- Save routine for future use

#### Execution (every time): 
User selects the saved routine and runs it

1. Tap "Slow Cooker Sunday" from saved routines list
2. Tap "Start" to begin the sequence
3. Timer 1 counts down from 10:00 → reaches 0:00 → ALARM (sound + vibration)
4. User taps "Start Next" when ready
5. Timer 2 counts down from 5:00 → reaches 0:00 → ALARM
6. User taps "Start Next" when ready
7. Timer 3 counts down from 4:00:00 → reaches 0:00 → ALARM
8. Routine complete → return to home

#### Note: 
- on toothbrushing example: 
    - In MVP, a 2-minute toothbrushing routine would be set up as 4 separate 30-second timers (Upper Left → Upper Right → Lower Right → Lower Left), each requiring manual "Start Next". This provides the visual progress and checkpoint alerts. 
    - A future version would add auto-advance mode, as a potential toggle, where the user would have the opton to have all 4 timers run continuously with automatic alerts.

### Key Differentiators

- **Save and reuse** 
    — Create once, use forever
- **Manual progression** 
    — User controls when to start each timer (crucial for tasks where timing isn't perfectly predictable)
- **Visual progress** 
    — See where you are in the sequence at a glance
- **Hands-free operation** 
    — Audio and haptic alerts mean users don't need to watch their phone
- **Named steps** 
    — Each timer has context (not just "10 minutes" but "Brown meat")

## Succcess Criteria 

### User Success Metrics

A user has successfully adopted the app when they:
- Create at least one routine and save it
- Reuse a saved routine at least 3 times without modifying it
- Complete a full routine from start to finish without abandoning it mid-sequence
- Edit or delete routines to keep their library organized and relevant
- Report they save time compared to setting individual timers each time

### Product Success Metrics

The app is successful when:
- **90%+ of routines created are multi-timer (≥2 timers in the sequence)**
    — validates the core use case
- **Users complete routines at a 80%+ rate** 
    - start → finish without abandoning 
    — validates the UX works
- **Average routine is used 5+ times** 
    — validates "save and reuse" solves a real problem
- **Users can create a routine in under 2 minutes** 
    — validates setup isn't a barrier

### Technical Success Criteria

The app must:
- **Run in development environments** 
    — Works reliably in iOS Simulator during development (via Expo Go)
    - Works reliably in Android Emulator during development
- **Run reliably** 
    — Alarms fire when they should, even if phone is locked
- **Persist data** 
    — Routines saved on the device survive app restarts
- **Work hands-free** 
    — Alerts are loud/strong enough to notice without watching screen
- **Launch quickly** 
    — From tap to first screen in <2 seconds

### MVP Acceptance Criteria

Version 1.0 is shippable when:

- [ ] User can create a routine with multiple named timers
- [ ] User can save a routine and see it listed on the home screen
- [ ] User can edit timer labels and durations within a routine
- [ ] User can delete entire routines from the home screen
- [ ] User can start a saved routine
- [ ] Each timer in the sequence runs independently and accurately
- [ ] User receives audio + haptic alerts when each timer completes
- [ ] User manually advances to the next timer via "Start Next" button
- [ ] User can complete an entire routine and return to home
- [ ] Saved routines persist across app restarts 
    (local storage only — no cloud sync in MVP)
- [ ] App runs successfully in iOS Simulator via Expo Go
- [ ] App runs successfully in Android Emulator via Expo Go
- [ ] App ready for iOS App Store submission (TestFlight beta testing complete)

## Monetization Strategy

Freemium Model: 
- Free core product with premium collaboration features.

### Free Tier (MVP + Phase 2)

#### Features:
- Create and save unlimited routines
- Edit and delete routines and timers (full CRUD)
- Run routines with manual advancement
- Auto-advance mode (Phase 2)
- Local device storage
- **Core value proposition:**
    - Save time on recurring multi-step tasks

#### Goal: 

Build user base, prove product-market fit, generate organic growth through word-of-mouth.

### Premium Tier (Phase 3+)

#### Features:

- Family/multi-user accounts 
    — Multiple users accessing shared routines
- Real-time sync across devices
- Cloud backup of routines
- Potential additional features: 
    - custom sounds
    - advanced analytics
    - routine templates

#### Goal: 

Monetize collaborative use cases where multiple people benefit from the same subscription.

#### Pricing: 

- To be determined based on market research and competitive analysis. 
- Likely monthly/annual subscription model targeting families and power users.

#### Why users would upgrade - Value Proposition: 

- Families with shared routines (bedtime, cooking, chores) get immediate value from multi-user access. 
- Solo users who want cloud backup and cross-device sync also benefit.


## Out of Scope for MVP

These are valuable features but NOT required for V1:

### Phase 2 Features (High Priority for Future)

- **Auto-advance mode** 
    — Timers that run continuously with automatic alerts at checkpoints 
    - Example: 2-minute timer with automatic notifications at 0:30, 1:00, 1:30, 2:00. MVP uses manual advancement only - user clicks "Start Next" between timers.
    - This would make toothbrushing and workout routines fully hands-free.
    - Would be a toggle that the user can set, to determine which type of alarm routine they wish to use

### Other Deferred Features

- **Family/multi-user accounts** 
    — Multiple users accessing shared routines, including routines already in progress. 
    Example: Both parents accessing the same bedtime routine, or husband taking over cooking timer mid-routine when helping with dinner. Note: 
    - This feature is a strong candidate for monetization (Premium/Pro tier) as it requires backend infrastructure and provides clear value for families.
- Reordering timers within a routine (drag-and-drop)
- Duplicating routines or timers
- Background execution when app is fully closed
    - Alarms continue firing even when app is terminated (best-effort when minimized in MVP)
- Customizable alert sounds per timer
    - Different sounds for different timers (single default sound in MVP) 
- Repeating/looping routines
    - Auto-restart a routine when complete
    - Would be a toggle on the routine setup screen
- Timer statistics or history
- Cloud sync or sharing routines with others
    -   Export/import routine configurations
    - Letting other family members see the progress of the routine and the set timers
- Auto-advance
    - Toggle present on the routine setup screen
    - Would allow us to determine if the app should automatically cycle between the alarms without requiring any user engagement.
- **Android Play Store deployment**
  — App code is cross-platform and tested in Android Emulator during development, but Play Store submission is deferred until after iOS App Store launch validates product-market fit.