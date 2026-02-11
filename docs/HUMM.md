# HUMM — Product Strategy & Build Guide

## What Is Humm?

Humm is an iOS app that guides users through a science-backed humming technique to relieve sinus congestion and improve nasal breathing. The app uses real-time microphone input to provide ambient visual feedback through a shader-based experience, helping users hum at the correct pitch and strength without clinical-feeling meters or numbers.

Think of it as Apple Mindfulness meets a musical tuner — but the interface communicates entirely through a living, breathing visual form rather than data.

---

## The Science (Brief)

The paranasal sinuses produce high concentrations of nitric oxide (NO), a gas that is antifungal, antibacterial, and antiviral. When sinuses become blocked, NO gets trapped and can't circulate.

Research from the Karolinska Institute (Weitzberg & Lundberg, 2002) demonstrated that humming increases nasal nitric oxide output 15× compared to quiet breathing. The oscillating airflow acts as a pump, flushing trapped NO through the sinus openings (ostia) even when partially blocked. Low-frequency humming (~130 Hz) produces the greatest effect because it's close to the natural resonance frequency of the sinus cavities.

A published case report (Eby, 2006) described chronic rhinosinusitis symptoms eliminated in 4 days using sustained daily humming sessions.

**Key references:**
- Weitzberg & Lundberg, *Am J Respir Crit Care Med*, 2002 — [PubMed](https://pubmed.ncbi.nlm.nih.gov/12119224/)
- Eby, *Medical Hypotheses*, 2006 — [PubMed](https://pubmed.ncbi.nlm.nih.gov/16406689/)
- Maniscalco et al., *European Respiratory Journal*, 2003 — [ERJ](https://publications.ersnet.org/content/erj/22/2/323)

---

## Treatment Protocol

The app is structured around a two-phase protocol:

### Phase 1: Initial Dose
- **Duration:** 4 days
- **Daily goal:** ~1 hour of accumulated "good hum time"
- Purpose: Eliminate or significantly reduce sinus congestion

### Phase 2: Maintenance
- **Duration:** Ongoing
- **Daily goal:** ~10 minutes of accumulated "good hum time"
- Purpose: Maintain sinus health and prevent recurrence

"Good hum time" is defined as time spent humming within the acceptable pitch and amplitude range. The timer accumulates only during good hum time and pauses naturally when the user stops humming, breathes, or drifts out of range. There is no prescribed inhale/exhale cadence — users find their own rhythm.

---

## Design Principles

1. **Ambient over clinical.** The app communicates through visual form, not numbers or meters. Users should feel their way into the right zone, not stress about precision.

2. **Beauty sustains attention.** People will use this for up to an hour at a time. The visual experience must be genuinely captivating — something you'd want to watch, not tolerate.

3. **Simplicity and clarity.** Inspired by Apple Mindfulness. Every screen should feel obvious. Minimal UI, generous space, no clutter.

4. **Progressive disclosure.** The science is real and compelling, but surfaced in bite-sized, consumer-friendly pieces — never overwhelming.

5. **Low pressure.** The feedback model encourages without judging. Drifting out of range is a gentle visual fade, not a failure state.

---

## Information Architecture

### Tab Bar
- **Home** — Session launcher and progress tracking
- **Settings** — Notifications/reminders, recalibration, preferences

### Core Flow

```
Launch → Onboarding (first time only) → Home → Session → Home
```

### First Launch Flow

```
Launch → Education Screens (2-3) → Calibration Test Session → First Full Session → Home
```

---

## Key Screens

### Onboarding (First Launch Only)

A short sequence of 2-3 bite-sized educational screens explaining:
- What humming does (nitric oxide, sinus ventilation — simple language)
- The 4-day protocol (what to expect)
- How the visual feedback works

Followed by a **calibration test session** where the user practices humming and sees the shader respond in real time. This helps them find the right pitch and strength before committing to their first full session.

### Home Screen

**Phase 1 layout:**
- **Four circles** across the top of the screen, representing Days 1–4
- Each circle's border acts as a progress meter filling toward the 1-hour goal
- Center of each circle shows "Day 1", "Day 2", etc., changing to a checkmark when complete
- **Large start button** in the center of the screen
- Tab bar at bottom

**Phase 2 layout (post day 4):**
- The home screen transitions to maintenance mode
- Single daily circle showing progress toward 10-minute goal
- Visual tone should signal "you've done the hard part" — a lighter, calmer state

### Active Session Screen

Three elements only:
1. **The shader** — dominant, center of screen, the primary visual experience
2. **Progress indicator** — time accumulated toward daily goal
3. **Stop/done button**

The shader is the core of the experience and is described in detail below.

### Session End

Brief summary on exit showing good hum time accumulated in the session. Then return to home where the day circle reflects updated progress.

---

## The Shader: Cymatic Feedback Model

### Concept

The shader is inspired by **cymatics** — the phenomenon where sound frequencies create physical shapes in matter (sand, water, particles). The visual metaphor: your voice creates a living form. When you hum correctly, the form is beautiful, full, and organic. When you drift, it changes shape.

The shader should render as a **mesh gradient style** similar to the Apple Meditation app — rich, fluid, luminous. This serves both aesthetics (it's gorgeous to watch for long periods) and accessibility (feedback is encoded in shape and size, not color, which supports colorblind users).

### Feedback Encoding

**Two dimensions are encoded into the shader:**

#### Pitch (frequency) → Shape
- **Too low:** Form is overly round, blobby, undifferentiated
- **In the zone (~130 Hz):** Smooth, organic, balanced — a pleasing natural geometry
- **Too high:** Form fragments into spikier, more angular, complex geometry

This mirrors real cymatic physics where higher frequencies produce more complex patterns.

#### Strength (amplitude) → Size
- **Too soft:** Form shrinks, faint, doesn't fill the space
- **In the zone:** Full, expanded, flowing — fills the target area
- **Too strong:** Form overflows, becomes chaotic or over-energized

#### The Target Outline

A subtle outline on screen represents the ideal size and shape. The user's goal is to make the shader bloom to match this outline — the right size (strength) and the right smoothness (pitch). This gives spatial feedback without any numbers.

### Ideal State

When humming correctly, the shader is a **full, smooth, organically flowing mesh gradient form** that comfortably fills the target outline. It should feel alive — gently pulsing and shifting — but settled and harmonious. This is the state users learn to recognize and sustain.

---

## Technical Considerations

### Audio Input
- Real-time microphone access via AVAudioEngine
- Pitch detection (fundamental frequency tracking) — target zone around 130 Hz
- Amplitude measurement for strength feedback
- Processing should be efficient enough for long sessions without significant battery drain

### Shader
- Metal shader or SceneKit/SpriteKit for the mesh gradient visual
- Must respond to audio input in real time with smooth interpolation
- Performance must be solid for sessions up to 1 hour

### Background / Lock Screen
- Sessions may run for up to an hour; users will not hold their phone the entire time
- Consider support for continued session with screen locked
- Live Activity on lock screen showing session progress is a strong opportunity

### Platform
- iOS native (Swift/SwiftUI)
- iPhone only for v1

---

## Scope & Phasing

This document defines the v1 product. Individual features and screens will be designed in detail as they are built. The following is the rough build order:

1. **Audio engine** — pitch detection and amplitude measurement
2. **Shader** — cymatic-inspired mesh gradient responding to audio input
3. **Session screen** — shader + progress + stop button
4. **Home screen** — day circles, start button, phase 1/phase 2 states
5. **Onboarding** — education screens + calibration test session
6. **Settings** — notifications, recalibration
7. **Lock screen / background session support**

---

*This is a living document. It provides strategic context and product direction. Detailed specifications for individual features will be developed as design iteration progresses.*
