# Product Requirements Document
## DreamLog — Dream Journal & Sleep Insight Tracker
**Version:** 1.0  
**Date:** April 19, 2026  
**Status:** Draft  
**Platform:** Mobile (iOS & Android via React Native / V0 by Vercel)

---

## 1. Overview

### 1.1 Product Summary
DreamLog is a mobile journaling app that empowers users to record their dreams and track the lifestyle factors that influence them. DreamLog surfaces patterns and insights that help users better understand their subconscious mind by connecting pre-sleep behaviors such as activities, media consumption, stress, and mood to the dreams users experience.

### 1.2 Problem Statement
Most people have no structured way to remember or analyze their dreams. Existing journaling apps are generic and don't connect dream content to the behaviors and emotions that may precede or follow them. Users who are curious about their dream patterns or lucid dreaming have no low-effort tool to explore them.

### 1.3 Goals
- Provide a fast, frictionless way to log a dream immediately upon waking
- Track pre-sleep lifestyle factors (activities, media consumed, stress level)
- Surface meaningful metrics and trends through a visual summary dashboard
- Make the experience feel personal, calming, and non-clinical

### 1.4 Non-Goals (V1)
- Social sharing or community features
- AI-powered dream interpretation
- Integration with wearables or sleep tracking hardware
- Web version

---

## 2. Target Users

### Primary User Persona
**The Curious Dreamer**
- Age: 18–40
- Interested in self-reflection, journaling, wellness, or psychology
- Not necessarily tech-savvy and values simplicity
- Wants to understand recurring themes, moods, or whether habits affect their dreams

### Secondary Persona
**The Sleep Optimizer**
- Tracks lifestyle habits closely (fitness, diet, media)
- Motivated by data and wants to see correlations between behavior and dream quality
- Comfortable exploring charts and analytics

---

## 3. Core Features

### 3.1 Dream Log Entry
The primary action in the app. Users log a dream immediately after waking or at any point during the day.

**Fields:**
| Field | Type | Required |
|---|---|---|
| Date | Auto-populated, editable | Yes |
| Dream Title | Short text | No |
| Dream Description | Long-form text (journal entry) | Yes |
| Emotion / Mood | Tag selector (see list below) | Yes |
| Dream Type | Tag (e.g., Lucid, Nightmare, Recurring, Vivid) | No |
| Stress Level | Slider (0–10) | Yes |
| Clarity | Slider (0–10, how clearly they remember) | No |

**Emotion Tags (selectable, multi-choice):**
Joy, Fear, Sadness, Confusion, Excitement, Anxiety, Peace, Anger, Wonder, Nostalgia

### 3.2 Pre-Sleep Factors Log
After or alongside the dream entry, users can log what they did the day/evening before the dream.

**Fields:**
| Field | Type |
|---|---|
| Activities | Multi-select tags (e.g., Exercise, Walk, Yoga, Social Event, Travel, Work, Other) |
| Food & Substances | Multi-select tags (e.g., Alcohol, Caffeine, Heavy Meal, Fasting, Junk Food, Healthy Foods, Other) |
| Media Consumed | Multi-select tags (e.g., Horror Film, News, Social Media, Book, Video Game, Music, Other) |
| Screen Time Before Bed | Single-select (None / <30 min / 30–60 min / >1 hr) |
| Notes | Optional free text |

### 3.3 Dream Calendar
A monthly calendar view that provides a visual overview of the user's dream history.

**Behavior:**
- Each day with a logged dream is highlighted
- Color-coding reflects the dominant emotion of that day's dream (e.g., yellow = joy, purple = fear, green = peace, red = stress, blue = sad, gray = neutral)
- Tapping a highlighted day opens the log entry for that date
- Days with no entry appear as neutral/empty
- Users can swipe between months

### 3.4 Summary Dashboard
A dedicated screen displaying metrics and visualizations of the user's dream data.

**Metrics Displayed:**
- **Dreams this month** — total count
- **Average stress level** — numeric, with trend arrow (vs. prior month)
- **Average clarity score** — numeric
- **Most common moods** — top 3 emotion tags with icon
- **Dream type breakdown** — small donut or bar chart (lucid / nightmare / recurring / vivid / other)
- **Stress level over time** — line graph (x-axis: dates, y-axis: stress score 1–10), filterable by week / month / 3 months
- **Top pre-sleep factors** — ranked list of the most frequently logged activities/media

### 3.5 Search & Filter
Users can search past entries by keyword, filter by emotion, date range, or dream type.

---

## 4. Navigation Structure

```
Bottom Tab Bar
├── 📖 Journal       — Chronological list of all dream entries
├── 📅 Calendar      — Monthly calendar view
├── ➕ Log Dream     — Floating action or center tab to create new entry
├── 📊 Summary       — Dashboard with metrics and charts
└── ⚙️  Settings     — Profile, notifications, theme, export
```

---

## 5. User Flows

### 5.1 Primary Flow: Log a Dream
1. User opens app → taps **Log Dream**
2. Enters dream description (required)
3. Selects emotion tags
4. Sets stress level slider
5. Optionally adds dream title, type, and clarity
6. Taps **Next** → Pre-Sleep Factors screen
7. Selects relevant activity/media tags
8. Taps **Save** → Entry appears on calendar and journal list

### 5.2 View Past Entry
1. User opens **Calendar** tab
2. Taps a highlighted date
3. Full entry expands with all logged details

### 5.3 View Monthly Summary
1. User opens **Summary** tab
2. Sees current month metrics by default
3. Scrolls to see stress graph
4. Taps graph filter to switch between week / month / 3 months

---

## 6. Design Guidelines

### Visual Style
- **Tone:** Calm, introspective, slightly mystical — think dark mode-first with deep purples, midnight blues, and soft pinks and golds
- **Typography:** Clean and readable; a serif for headings, sans-serif for body
- **Animations:** Gentle transitions, no harsh flashes or jarring motion
- **Iconography:** Soft, rounded icons — moons, stars, clouds

### Accessibility
- Minimum 4.5:1 contrast ratio for all text
- All interactive elements have accessible labels
- Support system font size scaling

---

## 7. Technical Considerations (for V0 Build)

### Recommended Stack
- **Frontend:** React Native (scaffolded via V0 by Vercel for UI components)
- **Local Storage:** AsyncStorage or SQLite (via Expo) for offline-first journaling
- **Charts:** Victory Native or Recharts (React Native compatible)
- **State Management:** React Context or Zustand for lightweight state
- **Navigation:** React Navigation (bottom tabs + stack)

### V0-Specific Notes
- Use V0 to generate individual screen components: Entry Form, Calendar View, Dashboard, Entry Card
- Prompt V0 with the emotion tag color system and dark/cosmic aesthetic for consistent output
- Export V0 components as `.tsx` files and integrate into an Expo or bare React Native project

### Data Model (Simplified)
```json
DreamEntry {
  id: string,
  date: ISO string,
  title: string,
  description: string,
  emotions: string[],
  dreamType: string,
  stressLevel: number (0–10),
  clarityScore: number (0–10),
  preSleepFactors: {
    activities: string[],
    food: string[],
    media: string[],
    screenTime: string,
    notes: string
  },
  createdAt: ISO string
}
```

---

## 8. Out of Scope for V1

| Feature | Rationale |
|---|---|
| AI dream interpretation | Adds complexity; consider for V2 |
| Cloud sync / account login | Keep V1 local-first for simplicity |
| Social sharing | Not aligned with V1 privacy-first tone |
| Wearable integration | Requires hardware partnerships |
| Recurring dream detection | Requires ML; V2 candidate |

---

## 9. Success Metrics

| Metric | Target |
|---|---|
| Onboarding completion rate | > 80% |
| Dreams logged per active user / month | ≥ 8 |
| Day-7 retention | > 40% |
| Crash-free session rate | > 99% |
| App store rating | ≥ 4.3 stars |

---

## 10. Milestones

| Phase | Deliverable | Target |
|---|---|---|
| 1 — Design | Wireframes, color system, component library via V0 | Week 1–2 |
| 2 — Core Build | Dream log entry + local storage + calendar view | Week 3–5 |
| 3 — Dashboard | Summary screen with charts and metrics | Week 6–7 |
| 4 — Polish | Animations, accessibility, edge cases, dark mode | Week 8 |
| 5 — Launch | TestFlight / Play Store beta | Week 9–10 |

---

*Document owner: Danielle Dacanay | Last updated: April 19, 2026*
