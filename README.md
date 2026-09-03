# VW-D16 Analogue Drum Machine

## Table of Contents

1. [Introduction](#1-introduction)
2. [Master Controls & Architecture](#2-master-controls--architecture)
3. [Drum Channels & Sound Shaping](#3-drum-channels--sound-shaping)
4. [The 16-Step Grid & Parameter Locks](#4-the-16-step-grid--parameter-locks)
5. [Technical Specifications](#5-technical-specifications)
6. [Credits & Copyright](#credits--copyright)

---

## 1. Introduction

Welcome to the **VW-D16 Analogue Drum Machine**, a 16-step pure synthesis rhythm generator. Serving as the dedicated percussion department of the Voltage & Wave ecosystem, the VW-D16 sits somewhere between a classic TR-style x0x drum machine and a modern performance groovebox.

Unlike sample-based players, the VW-D16 generates every transient, body, and noise burst in real time using the Web Audio API. It features four distinct analogue-modelled voices (Kick, Snare, Hi-Hat, and Clap), an advanced tactile interface, and "Elektron-style" per-step parameter locking — letting you alter the tuning, decay, and volume of a drum hit on a microscopic, step-by-step basis.

---

## 2. Master Controls & Architecture

The top panel governs global playback, preset generation, and live performance features.

<img width="2360" height="400" alt="vwd16-master-controls" src="https://github.com/user-attachments/assets/7a0e0fd1-d794-4de8-8508-5cd7f903ba89" />

### 2.1 Patterns

A single dropdown handles both preset loading and pattern generation:

| Selection | Function |
| :--- | :--- |
| `ROCK 1` · `ROCK 2` · `DISCO` · `BOSSA NOVA` · `ELECTRO` | Instantly loads a classic, genre-defining drum pattern across all four tracks. |
| `RANDOMISE ALL` | Intelligently populates the entire 16-step matrix using weighted probabilities (hi-hats are denser than claps, for instance). |
| `CLEAR ALL` | Wipes the grid on all four tracks. |

### 2.2 Clock

| Control | Function |
| :--- | :--- |
| **BPM** | A horizontal slider that sets the master tempo of the unit, from a sluggish 80 BPM to a driving 180 BPM. |

### 2.3 Performance & Transport

| Control | Function |
| :--- | :--- |
| **AUTO-FILL** | A momentary performance button. Holding it dynamically overrides the active sequence with an immediate 16th-note drum roll (snare/hat rush with four-on-the-floor kicks). Releasing it returns instantly to your programmed sequence. |
| **SYNC** | Instantly resets all track playheads to step 1 (or step 16, if a track is in reverse mode), keeping polyrhythmic sequences perfectly aligned. |
| **PLAY / STOP** | Toggles the global sequencer on and off. |

---

## 3. Drum Channels & Sound Shaping

The VW-D16 is divided into four independent synthesiser channels: **KICK** (red), **SNARE** (blue), **HI-HAT** (amber), and **CLAP** (green). Each channel follows the same layout — shown below for Kick — with its left-hand control block and its own row of the step grid.

<img width="2640" height="450" alt="vwd16-drum-channel" src="https://github.com/user-attachments/assets/defa64a5-5dbb-432d-bf77-60096f45e53d" />

### 3.1 Channel Routing & Triggers

| Control | Function |
| :--- | :--- |
| **MUTE** | Silences the individual track without stopping its sequencer playhead — the pattern keeps advancing silently underneath, so it drops back in perfectly in time when un-muted. |
| **RAND** | Generates a new randomised rhythm exclusively for that channel, based on its own track-specific density weighting. |
| **Play Mode** | `FWD` · `REV` · `PING` · `RAND` — sets that channel's step direction independently of the other three tracks. |

### 3.2 Analogue Synthesis Parameters

Each track has three dedicated horizontal faders that sculpt its raw oscillator and noise-buffer output:

| Control | Function |
| :--- | :--- |
| **TUNE** | Adjusts the fundamental pitch or filter cutoff of the drum voice. On **Kick**, this sets the target frequency of the low-end oscillator sweep. On **Snare**, it tunes the pitch of the triangle-oscillator body tone. On **Hi-Hat** and **Clap**, it shifts the bandpass filter frequency applied to the noise burst. |
| **DECAY** | Controls the duration of the amplitude envelope, transforming tight, clicking transients into booming tails or open hi-hats. |
| **LEVEL** | The master volume output for the individual track. |

---

## 4. The 16-Step Grid & Parameter Locks

The sequencer matrix relies on tactile, physical-style drum pads designed for instant feedback and deep parameter modulation.

### 4.1 Step Interactions

- **Audition & Toggle** — Clicking or tapping a step's drum pad toggles it on or off. Doing so immediately auditions the drum sound with its current parameters.
- **Visual Feedback** — A dedicated LED sits at the top of each column to indicate the active playback step, while the drum pads themselves depress and light up in the channel's colour when programmed.

### 4.2 Parameter Locking (P-Locks)

The VW-D16 lets you uncouple individual steps from a track's global parameters, enabling complex, evolving rhythms from a single drum voice — for example, a hi-hat pattern where every third hat is pitched down with a long decay.

**How to create a Parameter Lock:**

1. Press and hold a pad on the grid. This also toggles that step on or off, and the pad turns orange to indicate "Hold" mode.
2. While still holding the pad, move the `TUNE`, `DECAY`, or `LEVEL` slider on that track's left-hand control block.
3. A small amber Lock Indicator above the pad lights up, showing that this specific step now carries locked parameter data.
4. When the sequencer reaches this step, it uses your locked values instead of the track's global fader positions.

> **Note:** Releasing the pad snaps the left-hand sliders straight back to the track's global values — they're a live preview of the held step's data, not a separate editable state.

---

## 5. Technical Specifications

- **Sequencer Architecture:** 4 independent 16-step tracks, each with independent play direction (Forward, Reverse, Ping-Pong, Random).
- **Audio Engine:** Pure Web Audio API synthesis. Master bus processed through a `DynamicsCompressorNode` to prevent clipping during dense polyphonic playback and aggressive tuning overlap.
- **Drum Synthesis Models:**
  - **Kick:** Sine wave oscillator with a rapid exponential pitch envelope (transient click) into a linear decay.
  - **Snare:** Mixed triangle oscillator (body) and high-pass filtered white noise buffer (snap).
  - **Hi-Hat:** Bandpass-filtered white noise buffer.
  - **Clap:** Bandpass-filtered white noise, subjected to a multi-stage linear amplitude envelope to simulate a reverberating handclap.
- **Parameter Modulation:** Full array-based parameter locking for Tune, Decay, and Level across all 64 steps.
- **Interface:** Hardware-locked 1,280px widescreen chassis, optimised for touch displays with Pointer Event handling for multi-touch parameter locking.

---

## Credits & Copyright

**VW-D16 Analogue Drum Machine**
Created & Developed by **José Velázquez MA**
Published by **Voltage & Wave**
Website: [voltageandwave.co.uk](https://voltageandwave.co.uk/)

Copyright © 2026 José Velázquez MA / Voltage & Wave. All rights reserved.
