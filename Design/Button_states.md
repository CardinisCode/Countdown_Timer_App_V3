# Button States

## Overview

All interactive buttons must provide clear visual feedback across four states: Normal, Pressed, Disabled, and Focus. This ensures users understand when buttons are tappable and receive immediate feedback on interaction.

---

## Primary CTA Buttons

**Usage:** "Save", "Start Routine", "Save & Continue", "Start Next", "Finish"

### Normal State (Default)
- **Background color:** #007AFF (iOS blue)
- **Text color:** #FFFFFF (white)
- **Text style:** 17pt Semibold
- **Opacity:** 100%
- **Border:** None
- **Shadow:** 0 2pt 4pt rgba(0, 0, 0, 0.1) (subtle elevation)
- **Corner radius:** 12pt
- **Height:** 50pt

### Pressed State (Active Touch)
- **Background color:** #0051D5 (darker blue, 30% darker)
- **Text color:** #FFFFFF (white)
- **Opacity:** 100%
- **Scale:** 98% (subtle shrink effect)
- **Shadow:** 0 1pt 2pt rgba(0, 0, 0, 0.15) (reduced elevation)
- **Transition duration:** 0.1s ease-out
- **Visual effect:** Button appears to press down slightly

### Disabled State (Validation Failed)
- **Background color:** #E5E5E5 (light grey)
- **Text color:** #999999 (medium grey)
- **Opacity:** 60%
- **Border:** None
- **Shadow:** None
- **Cursor:** Not allowed (on web)
- **Touch:** No response to tap
- **Visual cue:** Clearly not interactive

### Focus State (Accessibility/Keyboard Navigation)
- **Background color:** #007AFF (iOS blue)
- **Text color:** #FFFFFF (white)
- **Border:** 3pt solid #005BB5 (darker blue outline)
- **Shadow:** 0 0 8pt rgba(0, 122, 255, 0.5) (blue glow)
- **Opacity:** 100%
- **Usage:** When navigating with external keyboard or VoiceOver

---

## Secondary Buttons

**Usage:** "Cancel"

### Normal State (Default)
- **Background color:** Transparent
- **Text color:** #007AFF (iOS blue)
- **Text style:** 17pt Regular
- **Opacity:** 100%
- **Border:** 1pt solid #007AFF
- **Shadow:** None
- **Corner radius:** 8pt
- **Height:** 44pt

### Pressed State (Active Touch)
- **Background color:** rgba(0, 122, 255, 0.1) (10% blue tint)
- **Text color:** #0051D5 (darker blue)
- **Border:** 1pt solid #0051D5
- **Opacity:** 100%
- **Scale:** 98%
- **Transition duration:** 0.1s ease-out

### Disabled State (If Applicable)
- **Background color:** Transparent
- **Text color:** #D1D1D6 (light grey)
- **Border:** 1pt solid #D1D1D6
- **Opacity:** 50%
- **Touch:** No response

### Focus State (Accessibility)
- **Background color:** rgba(0, 122, 255, 0.05) (5% blue tint)
- **Text color:** #007AFF
- **Border:** 3pt solid #007AFF (thicker border)
- **Shadow:** 0 0 6pt rgba(0, 122, 255, 0.3) (subtle glow)

---

## Destructive Buttons

**Usage:** "Delete Routine", "Delete Timer", "Delete Both", "End Routine"

### Normal State (Default)
- **Background color:** Transparent (text-only button)
- **Text color:** #FF3B30 (iOS red)
- **Text style:** 17pt Semibold
- **Opacity:** 100%
- **Border:** None
- **Shadow:** None
- **Height:** 44pt
- **Padding:** 16pt vertical

### Pressed State (Active Touch)
- **Background color:** rgba(255, 59, 48, 0.1) (10% red tint)
- **Text color:** #D70015 (darker red)
- **Opacity:** 100%
- **Scale:** 98%
- **Transition duration:** 0.1s ease-out
- **Visual effect:** Subtle background appears on press

### Disabled State (If Applicable)
- **Background color:** Transparent
- **Text color:** #FFB3AD (light red/pink)
- **Opacity:** 50%
- **Touch:** No response
- **Note:** Destructive buttons are rarely disabled

### Focus State (Accessibility)
- **Background color:** rgba(255, 59, 48, 0.05)
- **Text color:** #FF3B30
- **Border:** 2pt solid #FF3B30
- **Shadow:** 0 0 6pt rgba(255, 59, 48, 0.3) (red glow)

---

## Icon Buttons (Edit / Delete)

**Usage:** Edit pencil icon, Delete trash icon on timer/routine cards

### Edit Icon Button

#### Normal State
- **Icon color:** #007AFF (iOS blue)
- **Icon size:** 20 × 20pt
- **Background:** Transparent
- **Touch target:** 44 × 44pt (padding around icon: 12pt)
- **Opacity:** 100%

#### Pressed State
- **Icon color:** #0051D5 (darker blue)
- **Background:** rgba(0, 122, 255, 0.15) (15% blue tint, circular)
- **Scale:** 95%
- **Transition duration:** 0.1s ease-out

#### Disabled State
- **Icon color:** #D1D1D6 (light grey)
- **Background:** Transparent
- **Opacity:** 40%
- **Touch:** No response

#### Focus State
- **Icon color:** #007AFF
- **Background:** rgba(0, 122, 255, 0.2) (20% blue tint, circular)
- **Border:** 2pt solid #007AFF (circular outline)

### Delete Icon Button

#### Normal State
- **Icon color:** #FF3B30 (iOS red)
- **Icon size:** 20 × 20pt
- **Background:** Transparent
- **Touch target:** 44 × 44pt (padding around icon: 12pt)
- **Opacity:** 100%

#### Pressed State
- **Icon color:** #D70015 (darker red)
- **Background:** rgba(255, 59, 48, 0.15) (15% red tint, circular)
- **Scale:** 95%
- **Transition duration:** 0.1s ease-out

#### Disabled State
- **Icon color:** #FFB3AD (light red/pink)
- **Background:** Transparent
- **Opacity:** 40%
- **Touch:** No response

#### Focus State
- **Icon color:** #FF3B30
- **Background:** rgba(255, 59, 48, 0.2) (20% red tint, circular)
- **Border:** 2pt solid #FF3B30 (circular outline)

---

## Swipe-to-Delete Reveal Button

**Usage:** Delete button that appears when user swipes left on routine card

### Normal State (Visible After Swipe)
- **Background color:** #FF3B30 (iOS red)
- **Text color:** #FFFFFF (white)
- **Text style:** 17pt Semibold
- **Width:** 80pt
- **Height:** Full card height (minimum 68pt)
- **Corner radius:** 0 12pt 12pt 0 (rounded on right side only)
- **Opacity:** 100%

### Pressed State (Tap Delete)
- **Background color:** #D70015 (darker red)
- **Text color:** #FFFFFF
- **Opacity:** 100%
- **Visual effect:** Slight darken on press

### Animation
- **Reveal animation:** Slide in from right, 0.3s ease-out
- **On tap:** Immediate trigger, no delay
- **After delete:** Fade out card, 0.2s ease-in

---

## Routine/Timer Card (As Interactive Button)

**Usage:** Tappable routine cards on My Routines screen, timer cards on Routine Detail screen

### Normal State
- **Background color:** #FFFFFF (white)
- **Border:** 1pt solid #E5E5E5 (light grey)
- **Shadow:** 0 1pt 3pt rgba(0, 0, 0, 0.08) (subtle elevation)
- **Corner radius:** 12pt
- **Opacity:** 100%

### Pressed State (Tap Card)
- **Background color:** #F7F7F7 (very light grey)
- **Border:** 1pt solid #D1D1D6 (slightly darker grey)
- **Shadow:** 0 0 0 (no shadow, appears to press down)
- **Scale:** 99% (very subtle shrink)
- **Transition duration:** 0.1s ease-out

### Focus State (Accessibility)
- **Background color:** #FFFFFF
- **Border:** 3pt solid #007AFF (blue outline)
- **Shadow:** 0 0 8pt rgba(0, 122, 255, 0.3) (blue glow)

### Disabled State (If Applicable)
- **Background color:** #FAFAFA (very light grey)
- **Border:** 1pt solid #E5E5E5
- **Opacity:** 50%
- **Touch:** No response
- **Note:** Cards are rarely disabled

---

## Pause/Resume Toggle Button

**Usage:** Pause/Resume button on Running screen (state changes based on timer state)

### Normal State (Pause - Timer Running)
- **Background color:** #007AFF (iOS blue)
- **Text color:** #FFFFFF (white)
- **Text:** "Pause"
- **Text style:** 17pt Semibold
- **Border:** None
- **Shadow:** 0 2pt 4pt rgba(0, 0, 0, 0.1)
- **Corner radius:** 8pt
- **Height:** 44pt
- **Width:** 48% of screen width (in two-button layout)

### Normal State (Resume - Timer Paused)
- **Background color:** #34C759 (iOS green)
- **Text color:** #FFFFFF (white)
- **Text:** "Resume"
- **Text style:** 17pt Semibold
- **Visual cue:** Color change indicates different state

### Pressed State (Either Mode)
- **Background color:** Darkened by 30% (blue → #0051D5, green → #1E8B3C)
- **Text color:** #FFFFFF
- **Scale:** 98%
- **Transition duration:** 0.1s ease-out

### Disabled State
- **Background color:** #E5E5E5 (grey)
- **Text color:** #999999
- **Opacity:** 60%
- **Note:** Disabled when timer not running and not paused (edge case)

---

## Reset Button

**Usage:** Reset button on Running screen (resets active timer to full duration)

### Normal State
- **Background color:** Transparent
- **Text color:** #FF9500 (iOS orange)
- **Text:** "Reset"
- **Text style:** 17pt Semibold
- **Border:** 1pt solid #FF9500
- **Corner radius:** 8pt
- **Height:** 44pt
- **Width:** 48% of screen width (in two-button layout)

### Pressed State
- **Background color:** rgba(255, 149, 0, 0.15) (15% orange tint)
- **Text color:** #CC7700 (darker orange)
- **Border:** 1pt solid #CC7700
- **Scale:** 98%
- **Transition duration:** 0.1s ease-out

### Disabled State
- **Background color:** Transparent
- **Text color:** #FFD9A6 (light orange)
- **Border:** 1pt solid #FFD9A6
- **Opacity:** 50%
- **Note:** Disabled when timer is at full duration (nothing to reset)

---

## Quick Reference Table: Button States

| Button Type | Normal BG | Pressed BG | Disabled BG | Focus Border |
|-------------|-----------|------------|-------------|--------------|
| **Primary CTA** | #007AFF (blue) | #0051D5 (darker blue) | #E5E5E5 (grey) | 3pt #005BB5 |
| **Secondary** | Transparent | rgba(0,122,255,0.1) | Transparent | 3pt #007AFF |
| **Destructive** | Transparent | rgba(255,59,48,0.1) | Transparent | 2pt #FF3B30 |
| **Edit Icon** | Transparent | rgba(0,122,255,0.15) | Transparent | 2pt #007AFF (circle) |
| **Delete Icon** | Transparent | rgba(255,59,48,0.15) | Transparent | 2pt #FF3B30 (circle) |
| **Swipe Delete** | #FF3B30 | #D70015 | N/A | N/A |
| **Card** | #FFFFFF | #F7F7F7 | #FAFAFA | 3pt #007AFF |
| **Pause** | #007AFF | #0051D5 | #E5E5E5 | 3pt #005BB5 |
| **Resume** | #34C759 (green) | #1E8B3C | #E5E5E5 | 3pt #1E8B3C |
| **Reset** | Transparent | rgba(255,149,0,0.15) | Transparent | 2pt #FF9500 |

---

## Transition & Animation Specs

### Press Feedback
- **Duration:** 0.1s (100ms)
- **Easing:** ease-out
- **Scale change:** 98% (2% reduction)
- **Color transition:** Immediate (no fade)

### Focus Ring Animation
- **Duration:** 0.2s (200ms)
- **Easing:** ease-in-out
- **Effect:** Fade in border and glow
- **Trigger:** Keyboard navigation or VoiceOver focus

### Swipe-to-Delete
- **Reveal duration:** 0.3s (300ms)
- **Easing:** ease-out
- **Delete animation:** Card fade + slide out, 0.25s ease-in
- **Trigger:** Swipe gesture (minimum 60pt distance)

---

## Implementation Notes

### Haptic Feedback (iOS)
- **Primary CTA tap:** Light impact (`Haptics.impactAsync(Haptics.ImpactFeedbackStyle.Light)`)
- **Destructive button tap:** Medium impact (`Haptics.impactAsync(Haptics.ImpactFeedbackStyle.Medium)`)
- **Swipe-to-delete reveal:** Selection feedback (`Haptics.selectionAsync()`)
- **Delete confirmation:** Warning notification (`Haptics.notificationAsync(Haptics.NotificationFeedbackType.Warning)`)

### Android Considerations
- Use Material Design ripple effect on button press
- Maintain same color states
- Use elevation changes instead of shadows where appropriate
- Haptic feedback: Use `Vibration.vibrate(50)` for button presses

### Accessibility Requirements
- **Focus state must be visible:** Minimum 3pt border, high contrast
- **Disabled buttons must be obvious:** Minimum 40% opacity difference from normal state
- **Touch targets:** All buttons meet 44×44pt minimum
- **VoiceOver hints:** "Button. Double tap to activate" for all interactive elements

### Dark Mode Adjustments
- **Primary CTA:** Use lighter blue (#0A84FF) for better contrast
- **Destructive:** Use lighter red (#FF453A)
- **Disabled:** Increase opacity to 80% for visibility on dark backgrounds
- **Card pressed state:** Use #2C2C2E instead of #F7F7F7
- **Shadows:** Increase shadow intensity (darker shadows on dark backgrounds)

---

## Common Mistakes to Avoid

❌ **No visual feedback on press** — Users won't know the button registered their tap  
❌ **Disabled state looks interactive** — Must be clearly non-tappable  
❌ **Inconsistent press animation** — All buttons should use same timing (0.1s)  
❌ **Missing focus state** — Required for keyboard navigation and accessibility  
❌ **Touch target too small** — Minimum 44×44pt always  
❌ **Slow transitions** — Anything over 0.2s feels laggy for button presses  
❌ **Color-only states** — Combine color with opacity/border for accessibility  

---

## Validation Checklist

Before implementation, verify:
- [ ] All button types have Normal, Pressed, Disabled, and Focus states defined
- [ ] Press feedback is instant (0.1s transition)
- [ ] Disabled buttons are visually distinct (opacity/color difference)
- [ ] Focus states meet accessibility contrast requirements
- [ ] Touch targets are minimum 44×44pt
- [ ] Haptic feedback is implemented for key interactions
- [ ] Dark mode variants are specified
- [ ] Transitions feel responsive (no lag)