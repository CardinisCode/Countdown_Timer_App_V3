# Design Specification — Routine Timer App V3

## Design Principles

- **User-first:**
    - Every decision prioritises what feels natural and effortless for the user
- **Hands-free friendly:** 
    - Alerts (sound + vibration) ensure the user doesn't need to watch the screen
- **Progress visibility:** 
    - Colour states let the user instantly see where they are in their routine
- **Manual control:** 
    - The user advances timers at their own pace — nothing happens automatically
- **Easy maintenance:** 
    - Users can edit and delete routines and timers without friction

## Terminology

- **Routine:** 
    - A saved sequence of timers (e.g., "Slow Cooker Sunday")
- **Timer:** 
    - An individual countdown step within a routine (e.g., "Brown meat — 10:00")

## Colour States
- All timers are visible at all times during a running session. Colour indicates state:

| State | Colour | Meaning |
|-------|--------|---------|
| Completed | Green (#c8f7c5) | This timer has finished |
| Active | Yellow (#fff9c4) | This timer is currently counting down |
| Upcoming | White / light grey border | This timer hasn't started yet |

Text on all coloured backgrounds is black (#000000) for readability.

## Typography & Text Styles and Spacing & Layout

### Typography & Text Styles

#### Font Family

- Primary: System default (SF Pro on iOS, Roboto on Android)
- Reason: Native fonts provide better performance and automatic localization support

#### Text Hierarchy

##### Level 1: Screen Titles
- Font size: 28pt
- Font weight: Bold (700)
- Color: #000000 (black)
- Line height: 34pt
- Usage: "My Routines", "Edit Routine", "Add Timer"

##### Level 2: Routine/Timer Names (Headings)
- Font size: 20pt
- Font weight: Semibold (600)
- Color: #000000 (black)
- Line height: 25pt
- Usage: Routine name on Routine Detail screen, countdown timer labels

##### Level 3: Section Labels / Field Labels
- Font size: 16pt
- Font weight: Medium (500)
- Color: #000000 (black)
- Line height: 20pt
- Usage: "Routine name", "Timer label", "Duration"

##### Level 4: Body Text / Timer Duration
- Font size: 16pt
- Font weight: Regular (400)
- Color: #333333 (dark grey)
- Line height: 20pt
- Usage: Timer duration display ("10:00"), timer count ("3 timers · 4:15:00")

##### Level 5: Placeholder Text
- Font size: 16pt
- Font weight: Regular (400)
- Color: #999999 (medium grey)
- Style: Italic
- Line height: 20pt
- Usage: "e.g., Slow Cooker Sunday", "00" in duration fields

##### Level 6: Secondary Text / Helper Text
- Font size: 14pt
- Font weight: Regular (400)
- Color: #666666 (grey)
- Line height: 18pt
- Usage: "Total: 4:15:00", empty state messages

##### Level 7: Button Text (Primary CTA)
- Font size: 17pt
- Font weight: Semibold (600)
- Color: #FFFFFF (white)
- Line height: 22pt
- Usage: "Save", "Start Routine", "Save & Continue"

##### Level 8: Button Text (Secondary)
- Font size: 17pt
- Font weight: Regular (400)
- Color: #007AFF (iOS blue)
- Line height: 22pt
- Usage: "Cancel"

##### Level 9: Button Text (Destructive)
- Font size: 17pt
- Font weight: Semibold (600)
- Color: #FF3B30 (iOS red)
- Line height: 22pt
- Usage: "Delete Routine", "Delete Timer", "Delete Both"

##### Level 10: Large Countdown Display (Running Screen)
- Font size: 48pt
- Font weight: Bold (700)
- Color: #000000 (black)
- Line height: 52pt
- Usage: Active timer countdown on Running screen

##### Level 11: Running Timer Label (Active)
- Font size: 18pt
- Font weight: Medium (500)
- Color: #000000 (black)
- Line height: 22pt
- Usage: Timer label when active on Running screen

### Spacing & Layout

#### Screen-Level Spacing

##### Screen Margins (Horizontal)
- Standard horizontal padding: 20pt from screen edges
- Usage: All content should respect this minimum margin on left/right
- Exception: Full-width swipe actions can extend to edges

##### Screen Margins (Vertical)
- Top margin (below title): 24pt
- Bottom margin (above CTA button): 24pt
- Between sections: 32pt

##### Safe Areas
- Top: Respect device safe area (notch, status bar)
- Bottom: Respect device safe area (home indicator on newer iPhones)
- CTA buttons: Position 24pt above safe area bottom

#### Component Spacing

##### Routine/Timer Cards

###### Card Dimensions:
- Height: Auto (minimum 68pt)
- Horizontal padding (inside card): 16pt
- Vertical padding (inside card): 12pt
- Corner radius: 12pt
- Border: 1pt solid #E5E5E5 (light grey) 

###### Spacing Between Cards:
- Vertical gap between routine cards: 12pt
- Vertical gap between timer cards: 8pt

###### Card Content Spacing:
- Gap between routine name and timer count: 4pt
- Gap between timer label and duration: 8pt

### Input Fields

#### Field Dimensions:
- Height: 48pt
- Horizontal padding (inside field): 12pt
- Corner radius: 8pt
- Border: 1pt solid #D1D1D6 (iOS light grey)
- Border (focused): 2pt solid #007AFF (iOS blue)

#### Duration Fields (Hours/Minutes/Seconds):
- Width: 64pt each
- Height: 48pt
- Horizontal gap between fields: 8pt
- Gap between field and "h"/"m"/"s" label: 4pt

#### Spacing Between Fields:
- Vertical gap between field label and input: 8pt
- Vertical gap between different field groups: 24pt

### Buttons

#### Primary CTA Button:
- Height: 50pt
- Horizontal padding: 32pt
- Corner radius: 12pt
- Background: #007AFF (iOS blue)
- Width: Full width minus screen margins (flexible)

#### Secondary Button:
- Height: 44pt
- Horizontal padding: 24pt
- Corner radius: 8pt
- Background: Transparent
- Border: 1pt solid #007AFF

#### Destructive Button:
- Height: 44pt
- Text only: No background or border
- Padding: 16pt vertical

#### Spacing Between Buttons:
- Vertical gap between Primary and Secondary: 12pt
- Vertical gap before Destructive button: 32pt (visual separator)

#### Touch Targets:
- Minimum tap area: 44 × 44pt (iOS accessibility standard)
- Applies to: All buttons, edit icons, delete icons

### Icon Sizing

#### Edit Icon (Pencil):
- Size: 20 × 20pt
- Color: #007AFF
- Padding around icon: 12pt (total touch target: 44pt)

#### Delete Icon (Trash):
- Size: 20 × 20pt
- Color: #FF3B30
- Padding around icon: 12pt (total touch target: 44pt)

#### Checkmark Icon (Timer Done screen):
- Size: 64 × 64pt
- Color:-  #34C759 (iOS green)

#### Add Icon (+ symbol):
- Size: 24 × 24pt
- Color: #007AFF

### Screen-Specific Layouts

#### Screen 1 — My Routines
```
┌─────────────────────────────────┐
│ [20pt margin]                   │ ← Horizontal screen margin
│                                 │
│ My Routines                     │ ← 28pt Bold
│ [24pt gap]                      │ ← Top margin below title
│                                 │
│ ┌─────────────────────────────┐ │
│ │ [12pt padding]              │ │ ← Card vertical padding
│ │ Slow Cooker Sunday          │ │ ← 20pt Semibold
│ │ [4pt gap]                   │ │
│ │ 3 timers · 4:15:00          │ │ ← 14pt Regular, #666
│ │ [12pt padding]              │ │
│ └─────────────────────────────┘ │
│ [12pt gap]                      │ ← Between cards
│ ┌─────────────────────────────┐ │
│ │ Another Routine             │ │
│ └─────────────────────────────┘ │
│                                 │
│ [flexible space]                │
│                                 │
│ ┌─────────────────────────────┐ │
│ │     Add Routine             │ │ ← 50pt height Primary CTA
│ └─────────────────────────────┘ │
│ [24pt margin]                   │ ← Bottom margin above safe area
└─────────────────────────────────┘
```

#### Screen 2 — Create Routine
```
┌─────────────────────────────────┐
│ [20pt margin]                   │
│                                 │
│ Routine name                    │ ← 16pt Medium field label
│ [8pt gap]                       │
│ ┌─────────────────────────────┐ │
│ │ [12pt padding]              │ │ ← 48pt height input
│ │ e.g., Slow Cooker Sunday    │ │ ← 16pt Italic placeholder
│ └─────────────────────────────┘ │
│ [24pt gap]                      │ ← Between field groups
│                                 │
│ Timer label (optional)          │ ← 16pt Medium
│ [8pt gap]                       │
│ ┌─────────────────────────────┐ │
│ │ e.g., Brown meat            │ │
│ └─────────────────────────────┘ │
│ [24pt gap]                      │
│                                 │
│ Duration                        │ ← 16pt Medium
│ [8pt gap]                       │
│ ┌──┐ h [8pt] ┌──┐ m [8pt] ┌──┐ s
│ │00│        │00│        │00│   │ ← 64pt width each
│ └──┘        └──┘        └──┘   │
│                                 │
│ [flexible space]                │
│                                 │
│ ┌─────────────────────────────┐ │
│ │          Save               │ │ ← 50pt Primary CTA
│ └─────────────────────────────┘ │
│ [24pt margin]                   │
└─────────────────────────────────┘
```

#### Screen 7 — Running
```
┌─────────────────────────────────┐
│ [20pt margin]                   │
│                                 │
│ Slow Cooker Sunday              │ ← 20pt Semibold
│ [8pt gap]                       │
│ Total running: 0:10:18          │ ← 14pt Regular, #666
│ [24pt gap]                      │
│                                 │
│ ┌─────────────────────────────┐ │
│ │ [16pt padding]              │ │ ← Completed (green bg)
│ │ ✓ Brown meat                │ │ ← 16pt Regular
│ │ 10:00                       │ │ ← 14pt, #666
│ │ [16pt padding]              │ │
│ └─────────────────────────────┘ │
│ [8pt gap]                       │
│ ┌─────────────────────────────┐ │
│ │ [20pt padding]              │ │ ← Active (yellow bg)
│ │ Add vegetables              │ │ ← 18pt Medium
│ │ [12pt gap]                  │ │
│ │        4:42                 │ │ ← 48pt Bold countdown
│ │                             │ │
│ │ [20pt padding]              │ │
│ └─────────────────────────────┘ │
│ [8pt gap]                       │
│ ┌─────────────────────────────┐ │
│ │ [16pt padding]              │ │ ← Upcoming (white bg)
│ │ Slow cook                   │ │ ← 16pt Regular, muted
│ │ 4:00:00                     │ │
│ │ [16pt padding]              │ │
│ └─────────────────────────────┘ │
│                                 │
│ [24pt gap]                      │
│                                 │
│ ┌───────────┐  ┌──────────────┐│
│ │  Pause    │  │    Reset     ││ ← 44pt height buttons
│ └───────────┘  └──────────────┘│
│     [12pt gap between buttons]  │
│ [24pt margin]                   │
└─────────────────────────────────┘
```

### Color Usage Summary

#### Text Colors
- Primary text (headings, labels): #000000 (black)
- Body text: #333333 (dark grey)
- Secondary text: #666666 (grey)
- Placeholder text: #999999 (light grey)
- Link/Interactive text: #007AFF (iOS blue)
- Destructive text: #FF3B30 (iOS red)

#### Background Colors
- Screen background: #FFFFFF (white)
- Card background: #FFFFFF (white)
- Primary button: #007AFF (iOS blue)
- Completed timer: #c8f7c5 (light green) — from color states
- Active timer: #fff9c4 (light yellow) — from color states
- Upcoming timer: #FFFFFF (white)

#### Border Colors
- Default border: #E5E5E5 (very light grey)
- Input border (normal): #D1D1D6 (iOS light grey)
- Input border (focused): #007AFF (iOS blue)
- Card separator: #E5E5E5

## Implementation Notes

### Responsive Behavior
- All spacing should scale proportionally on larger devices (iPad)
- Font sizes can increase by 10-20% on iPad
- Maintain minimum touch targets of 44pt regardless of device

### Dark Mode Considerations
- Text colors should invert (white text on dark backgrounds)
- Background colors should adapt (#FFFFFF → #1C1C1E for dark mode)
- Maintain color state meanings (green = completed, yellow = active)
- Ensure sufficient contrast in both light and dark modes

### Accessibility
- All text should support Dynamic Type (iOS font scaling)
- Minimum contrast ratio: 4.5:1 for body text, 3:1 for large text (18pt+)
- Touch targets: Minimum 44 × 44pt for all interactive elements
- Spacing should remain consistent even when text scales

## Screens

### Screen 1 — Home

#### Purpose: 
- Landing screen and saved routines library.

#### Content:

- Title: "My Routines"
- List of saved routines (name + timer count + total duration)
- Each routine card has:
    - Routine name (tap to view details)
    - Timer count and total duration (e.g., "3 timers · 4:15:00")
    - Delete option (swipe-to-delete or long-press menu)
- "Add Routine" CTA button (always visible, bottom of screen)

#### Behaviour:

- Tap a routine card → navigate to Routine Detail (screen 3)
- Swipe left on routine → Delete button appears
- Tap Delete → confirmation dialog → delete routine from storage
- Tap "Add Routine" → navigate to Create Routine (screen 2)
- Empty state: friendly message "No routines yet. Tap Add Routine to begin."

#### Interactions:

- Swipe-to-delete pattern for routine removal
- Tap card for quick access to routine details

### Screen 2 — Create Routine

#### Purpose: 
Name a new routine and add its first timer.

#### Content:

- Section: Routine name
    - Field label: "Routine name"
    - Placeholder: "e.g., Slow Cooker Sunday"
    - Input: TextInput, default keyboard

- Section: First timer
    - Field label: "Timer label"
    - Placeholder: "e.g., Brown meat"
    - Input: TextInput, default keyboard
    - Field label: "Duration"
    - Three inputs: hours / minutes / seconds
    - Placeholders: "00" in each field
    - Input: TextInput, numeric keyboard

- "Save" CTA button

#### Behaviour:

- Routine name: required. Save disabled if empty.
- Timer label: optional. If empty, defaults to Timer1 (auto-incrementing).
- Duration: Save disabled if all three fields are 0.
- Tapping any input field opens the device keyboard automatically.
- "Save" → creates routine with first timer, navigates to Routine Detail (screen 3).

#### Validation:

- Routine name cannot be empty
- Duration must be greater than 0:00:00
- Timer label defaults to "Timer1" if left blank

### Screen 3 — Routine Detail

#### Purpose: 
View and manage all timers in a routine before starting.

#### Content:

- Routine name (heading with edit icon)
- Total duration (sub-heading, e.g., "Total: 4:15:00")
- Scrollable list of timers, each showing:
    - Timer label
    - Duration
    - Edit button (pencil icon or tap-to-edit)
    - Delete button (trash icon)
- "+ Add Timer" button
- "Start Routine" CTA button

#### Behaviour:

- Tap routine name / edit icon → navigate to Edit Routine Name (screen 4)
- Tap edit icon on a timer → navigate to Edit Timer (screen 5)
- Tap delete icon on a timer → confirmation dialog → delete timer from routine
- "+ Add Timer" → navigate to Add Timer (screen 6), returns here on save
- "Start Routine" → navigate to Running (screen 7)
- "Start Routine" is always active (there is always at least one timer from Create Routine)
- Back button → return to "My Routines" (screen 1)

#### Edit/Delete Patterns:

- Inline edit/delete buttons on each timer card
- Confirmation dialog for destructive actions (delete timer)
- If last timer is deleted, user is prompted to add another or delete the routine

### Screen 4 — Edit Routine Name

#### Purpose: 
Update the routine's name or delete the entire routine.

#### Content:

- Title: "Edit Routine"
- Field label: "Routine name"
- Input: TextInput, default keyboard, pre-filled with current name
- "Save" button (primary CTA)
- "Cancel" button (secondary)
- "Delete Routine" button (destructive, at bottom, red text)

#### Behaviour:

- Name field: required. Save disabled if empty.
- "Save" → updates routine name, returns to Routine Detail (screen 3)
- "Cancel" → discards changes, returns to Routine Detail (screen 3)
- "Delete Routine" → shows confirmation dialog → deletes routine and all timers → navigates to Home (screen 1)

#### Validation:

- Routine name cannot be empty

#### Layout:

```
┌─────────────────────────────────┐
│ ← Edit Routine                  │
├─────────────────────────────────┤
│                                 │
│ Routine name                    │
│ ┌─────────────────────────────┐ │
│ │ Slow Cooker Sunday          │ │
│ └─────────────────────────────┘ │
│                                 │
│        [ Save ]                 │ ← Primary CTA (green/blue)
│        [ Cancel ]               │ ← Secondary (grey)
│                                 │
│                                 │
│         ───────                 │
│                                 │
│    [ Delete Routine ]           │ ← Destructive (red, bottom)
└─────────────────────────────────┘
```

### Screen 5 — Edit Timer

#### Purpose:
Update an existing timer's label and duration.

#### Content:
- Title: "Edit Timer"
- Field label: "Timer label (optional)"
- Input: TextInput, default keyboard, pre-filled with current label
- Field label: "Duration"
- Three inputs: hours / minutes / seconds
- Input: TextInput, numeric keyboard, pre-filled with current values
- "Save" button (primary CTA)
- "Cancel" button (secondary)
- "Delete Timer" button (destructive, at bottom, red text)

#### Behaviour:
- Label: optional. Defaults to auto-incremented label if empty.
- Duration: Save disabled if all three fields are 0.
- "Save" → updates timer, returns to Routine Detail (screen 3)
- "Cancel" → discards changes, returns to Routine Detail (screen 3)
- "Delete Timer" → shows confirmation dialog:
    - If NOT the last timer: Standard delete confirmation → deletes timer → returns to Routine Detail (screen 3)
    - If this IS the last timer: Special confirmation warning → deletes timer AND routine → navigates to Home (screen 1)

#### Validation:

- Duration must be greater than 0:00:00
- Label defaults to next available "Timer #" if left blank

#### Layout 

```
┌─────────────────────────────────┐
│ ← Edit Timer                    │
├─────────────────────────────────┤
│                                 │
│ Timer label (optional)          │
│ ┌─────────────────────────────┐ │
│ │ Add vegetables              │ │
│ └─────────────────────────────┘ │
│                                 │
│ Duration                        │
│ ┌──┐   ┌──┐   ┌──┐            │
│ │00│ h │05│ m │00│ s          │
│ └──┘   └──┘   └──┘            │
│                                 │
│        [ Save ]                 │ ← Primary CTA
│        [ Cancel ]               │ ← Secondary
│                                 │
│         ───────                 │
│                                 │
│     [ Delete Timer ]            │ ← Destructive (red, bottom)
└─────────────────────────────────┘
```

### Screen 6 — Add Timer

#### Purpose:
Add a new timer to an existing routine.

#### Content:
- Title: "Add Timer"
- Field label: "Timer label (optional)"
- Placeholder: "e.g., Add sauce"
- Input: TextInput, default keyboard
- Field label: "Duration"
- Three inputs: hours / minutes / seconds
- Placeholders: "00" in each field
- Input: TextInput, numeric keyboard
- "Save & Continue" CTA button

#### Behaviour:

- Label: optional. If empty, defaults to next auto-increment label (e.g., "Timer 1", "Timer 2").
- Duration: Save disabled if all three fields are 0.
- "Save & Continue" → saves timer and returns to Routine Detail (screen 3).

#### Validation:

- Duration must be greater than 0:00:00
- Label auto-increments if left blank (e.g., "Timer 2" if one timer exists, "Timer 3" if two exist)

#### Layout 
```
┌─────────────────────────────────┐
│ ← Add Timer                     │
├─────────────────────────────────┤
│                                 │
│ Timer label (optional)          │
│ ┌─────────────────────────────┐ │
│ │ e.g., Add sauce             │ │ ← Placeholder
│ └─────────────────────────────┘ │
│                                 │
│ Duration                        │
│ ┌──┐   ┌──┐   ┌──┐            │
│ │00│ h │00│ m │00│ s          │
│ └──┘   └──┘   └──┘            │
│                                 │
│    [ Save & Continue ]          │ ← Primary CTA
└─────────────────────────────────┘
```

### Screen 7 — Running

#### Purpose:
Active routine session view showing progress through timers.

#### Content:

- Routine name (heading)
- "Total running: HH:MM:SS" (elapsed time across all timers, counting up)
- Scrollable list of all timers with colour-coded state:
    - Completed timers: green background (#c8f7c5), black text, label + original duration
    - Active timer: yellow background (#fff9c4), black text, label + live countdown (large font, e.g., "8:42")
    - Upcoming timers: white background, grey text, label + original duration (muted)
- "Pause / Resume" button
- "Reset" button (resets active timer to full duration)

#### Behaviour:

- When active timer reaches 0:00:00 → sound + vibration alert fires → navigate to Timer Done (screen 8)
- Pause: freezes countdown. Button label changes to "Resume".
- Resume: continues countdown from where it paused.
- Reset: restores active timer to its original duration, keeps running.
- Back button: confirmation dialog "End routine early?" → return to Home (screen 1)

#### Visual Feedback:

- Active timer card pulses subtly or has animated border
- Completed timers fade to muted green
- Total running time counts up to show session duration
- Large countdown font for active timer (e.g., 24-32pt)

#### Layout 
```
┌─────────────────────────────────┐
│ Slow Cooker Sunday              │
├─────────────────────────────────┤
│ Total running: 0:10:18          │
│                                 │
│ ┌─────────────────────────────┐ │
│ │ ✓ Brown meat                │ │ ← Completed (green)
│ │ 10:00                       │ │
│ └─────────────────────────────┘ │
│                                 │
│ ┌─────────────────────────────┐ │
│ │ Add vegetables              │ │ ← Active (yellow)
│ │        4:42                 │ │ ← Large countdown
│ │      (active)               │ │
│ └─────────────────────────────┘ │
│                                 │
│ ┌─────────────────────────────┐ │
│ │ Slow cook                   │ │ ← Upcoming (white/grey)
│ │ 4:00:00                     │ │
│ └─────────────────────────────┘ │
│                                 │
│   [ Pause ]     [ Reset ]       │
└─────────────────────────────────┘
```

### Screen 8 — Timer Done

#### Purpose:
Notify the user a timer has finished and let them advance manually.

#### Content:

- Checkmark icon (large, celebratory, e.g., ✅ or ✓ in circle)
- "[Timer label] complete!" message (e.g., "Brown meat complete!")
- Sound + vibration alert fires on screen load
- "Start Next" CTA button (or "Finish" if last timer)

#### Behaviour:

- "Start Next" → navigates back to Running (screen 7), next timer becomes active (yellow)
- If this was the last timer → "Start Next" is replaced by "Finish" → navigates back to Home (screen 1)
- Sound: short success tone via expo-av
- Vibration: success haptic via expo-haptics
- Both sound and vibration trigger simultaneously on screen load

#### Celebration:

- If last timer: "Routine complete! 🎉" message instead of "[Timer label] complete!"
- Encourage user with affirming copy (e.g., "Great work!")



#### Confirmation Dialogs

##### Delete Timer (NOT last timer):
```
Title: "Delete Timer?"
Message: "This will remove [Timer Label] from the routine."
Buttons: Cancel | Delete (destructive red)
```

##### Delete Last Timer (deletes entire routine):
```
Title: "Delete Last Timer?"
Message: "This is the last timer in [Routine Name]. Deleting it will also delete the entire routine. This cannot be undone."
Buttons: Cancel | Delete Both (destructive red)
```

#### Layout 
```
┌─────────────────────────────────┐
│                                 │
│                                 │
│           ✅                    │ ← Large checkmark
│                                 │
│      Brown meat                 │
│       complete!                 │
│                                 │
│   🔔 Sound + vibration          │ ← Visual indicator
│                                 │
│                                 │
│      [ Start Next ]             │ ← Primary CTA
│                                 │
└─────────────────────────────────┘
```
Last timer variant:
```
┌─────────────────────────────────┐
│                                 │
│           ✅                    │
│                                 │
│   Routine complete! 🎉          │
│                                 │
│      Great work!                │
│                                 │
│                                 │
│       [ Finish ]                │ ← Navigate to Home
│                                 │
└─────────────────────────────────┘
```

## Complete Navigation Flow — All 8 Screens

### Visual Navigation Map
```
My Routines (1)
  ├── Swipe routine → Delete confirmation → stay on My Routines (1)
  │
  ├── Add Routine → Create Routine (2)
  │                     └── Save → Routine Detail (3)
  │
  └── Tap routine card → Routine Detail (3)
                            ├── Edit routine name → Edit Routine (4)
                            │                          ├── Save → back to Routine Detail (3)
                            │                          ├── Cancel → back to Routine Detail (3)
                            │                          └── Delete Routine → confirmation → My Routines (1)
                            │
                            ├── Tap edit on timer → Edit Timer (5)
                            │                          ├── Save → back to Routine Detail (3)
                            │                          ├── Cancel → back to Routine Detail (3)
                            │                          └── Delete Timer → confirmation:
                            │                                              ├── If NOT last timer → back to Routine Detail (3)
                            │                                              └── If IS last timer → My Routines (1)
                            │
                            ├── Tap delete on timer → confirmation → back to Routine Detail (3)
                            │
                            ├── + Add Timer → Add Timer (6)
                            │                     └── Save & Continue → back to Routine Detail (3)
                            │
                            └── Start Routine → Running (7)
                                                    ├── Pause/Resume → stay on Running (7)
                                                    ├── Reset → stay on Running (7)
                                                    ├── Back → confirmation "End early?" → My Routines (1)
                                                    └── Timer reaches 0:00 → Timer Done (8)
                                                                               ├── Start Next → Running (7) [next timer active]
                                                                               └── Finish (last timer) → My Routines (1)
```

### Screen-by-Screen Navigation

#### Screen 1 — My Routines

- From here, you can go to:
    - Create Routine (2) — via "Add Routine" button
    - Routine Detail (3) — via tap on routine card
    - Delete confirmation dialog — via swipe-to-delete

- You get here from:
    - Create Routine (2) — never goes back here (goes to Routine Detail instead)
    - Edit Routine (4) — after deleting routine
    - Edit Timer (5) — after deleting last timer (which deletes routine)
    - Running (7) — after early exit confirmation
    - Timer Done (8) — after "Finish" button on last timer

#### Screen 2 — Create Routine

- From here, you can go to:
    - Routine Detail (3) — via "Save" button

- You get here from:
    - My Routines (1) — via "Add Routine" button

#### Screen 3 — Routine Detail

- From here, you can go to:
    - My Routines (1) — via back button
    - Edit Routine (4) — via tap on routine name/edit icon
    - Edit Timer (5) — via tap on timer edit button
    - Add Timer (6) — via "+ Add Timer" button
    - Running (7) — via "Start Routine" button
    - Delete confirmation dialog — via tap on timer delete button

- You get here from:
    - My Routines (1) — via tap on routine card
    - Create Routine (2) — after saving new routine
    - Edit Routine (4) — after Save or Cancel
    - Edit Timer (5) — after Save, Cancel, or Delete (if not last timer)
    - Add Timer (6) — after "Save & Continue"

#### Screen 4 — Edit Routine

- From here, you can go to:
    - Routine Detail (3) — via "Save" or "Cancel" button
    - My Routines (1) — via "Delete Routine" button + confirmation
    - Delete confirmation dialog — via "Delete Routine" button

- You get here from:
    - Routine Detail (3) — via tap on routine name/edit icon

#### Screen 5 — Edit Timer

- From here, you can go to:
    - Routine Detail (3) — via "Save", "Cancel", or "Delete Timer" (if not last timer)
    - My Routines (1) — via "Delete Timer" + confirmation (if IS last timer)
    - Delete confirmation dialog — via "Delete Timer" button

- You get here from:
    - Routine Detail (3) — via tap on timer edit button

#### Screen 6 — Add Timer

- From here, you can go to:
    - Routine Detail (3) — via "Save & Continue" button

- You get here from:
    - Routine Detail (3) — via "+ Add Timer" button

#### Screen 7 — Running

- From here, you can go to:
    - My Routines (1) — via back button + "End early?" confirmation
    - Timer Done (8) — when active timer reaches 0:00:00
    - Stays on Running (7) — via Pause, Resume, or Reset

- You get here from:
    - Routine Detail (3) — via "Start Routine" button
    - Timer Done (8) — via "Start Next" button

#### Screen 8 — Timer Done

- From here, you can go to:
    - Running (7) — via "Start Next" button (makes next timer active)
    - My Routines (1) — via "Finish" button (only shown for last timer)

- You get here from:
    - Running (7) — when active timer reaches 0:00:00

### Delete Operation Paths

#### Three Ways to Delete a Routine
```
| Path | Starting Point | Steps | Confirmation | End Point |
|---|---|---|---|---|
|1. Swipe-to-delete | My Routines (1) | Swipe routine card → Tap Delete | "Delete Routine?" | My Routines (1) |
| 2. Edit Routine | Routine Detail (3) → Edit Routine (4) | Tap "Delete Routine" |  Routine""Delete Routine?" | My Routines (1) | 
|3. Delete last time | Routine Detail (3) → Edit Timer (5) | Tap "Delete Timer" on last timer | "Delete Last Timer?" (warns about routine deletion) | My Routines (1) |

```
#### Delete Individual Timer (Not Last)
```
| Starting Point | Steps | Confirmation | End Point | 
|---|---|---|---|
|Option A: Routine Detail (3) | Tap delete icon on timer card | "Delete Timer?" | Routine Detail (3) | 
| Option B: Edit Timer (5) | Tap "Delete Timer" button | "Delete Timer?" | Routine Detail (3) |
```

## Confirmation Dialogs Summary

### Delete Routine (from swipe or Edit Routine screen)
```
Title: "Delete Routine?"
Message: "This will permanently delete [Routine Name] and all its timers. This cannot be undone."
Buttons: Cancel | Delete (destructive red)
Outcome: Navigate to My Routines (1)
```

### Delete Timer (NOT last timer)
```
Title: "Delete Timer?"
Message: "This will remove [Timer Label] from the routine."
Buttons: Cancel | Delete (destructive red)
Outcome: Stay on current screen (or navigate to Routine Detail if from Edit Timer)
```

### Delete Last Timer (deletes entire routine)
```
Title: "Delete Last Timer?"
Message: "This is the last timer in [Routine Name]. Deleting it will also delete the entire routine. This cannot be undone."
Buttons: Cancel | Delete Both (destructive red)
Outcome: Navigate to My Routines (1)
```

### End Routine Early
```
Title: "End Routine?"
Message: "Your progress will be lost."
Buttons: Keep Going | End Routine (destructive)
Outcome: Navigate to My Routines (1)
```

## Quick Reference: All 8 Screens

- My Routines — Landing screen, routine library
- Create Routine — Name routine + add first timer
- Routine Detail — View/manage timers, start routine
- Edit Routine — Update routine name or delete routine
- Edit Timer — Update timer or delete timer
- Add Timer — Add another timer to routine
- Running — Active session with countdown
- Timer Done — Completion alert + manual advance

## Button States 

Note to self: Review the file "Button_states.md" and then copy the info across. 
