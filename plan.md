# Guitar Hero (web, minimal) — plan

## Goal
Single `index.html` (no build step) playable Guitar Hero clone in the browser.
Input: real Guitar Hero controller via Web Gamepad API, keyboard fallback.
Audio: fully synthesized via Web Audio — original composition, zero copyright risk.

## Song: "Shred of the Dragon" (original, TTFAF-inspired style)
- ~200 BPM, E harmonic minor, power-metal feel: fast 16th-note runs,
  gallop rhythm guitar, twin-lead-ish detuned saws, kick/snare/hats synthesized.
- Original melody/riffs only — evokes the genre (tempo, shred density, key)
  without copying any actual TTFAF melody.
- Structure (~70s): arpeggio intro → gallop riff → melodic verse →
  shred-burst solo → riff reprise → final shred + ending hit.
- Lead melody events ARE the chart — guaranteed audio/chart sync.
- Lanes derived from scale-degree rank (0-6 → 0-4) + octave delta, clamped.

## Rendering
- Canvas, 5 lanes, slight perspective (narrow at top → wide at hit line).
- GH colors: green/red/yellow/blue/orange. Notes scroll toward hit line.
- Timing master clock: `AudioContext.currentTime` (song rendered once into an
  AudioBuffer via OfflineAudioContext, then played — sample-accurate).

## Input
- Keyboard: frets `1-5` or `A S D F G`; strum `Enter`/`Space`/arrow keys.
- Gamepad: default profile (Xbox GH: frets = buttons [0,1,3,2,4] mapped to
  lanes, strum = dpad up/down 12/13) + interactive remap mode (`R` on title
  screen → press each fret + strum; saved to localStorage).
- Live debug overlay on title screen: gamepad id + pressed button indices,
  so unknown mappings are trivially fixable.
- Latency calibration: `[`/`]` adjusts audio offset ±10ms, persisted.

## Gameplay
- Strum + correct fret held when note crosses line = hit.
  Window: ±130ms (Perfect <60ms, Good <130ms). Overstrum = harmless.
- Score: 50 × multiplier (1x→4x every 10 streak). Track score, streak, hits/misses.
- Screens: TITLE → COUNTDOWN → PLAY → RESULTS (accuracy + grade). `Enter` restarts.

## Files
- `index.html` — everything (markup, CSS, JS inline).
- `plan.md` — this file.

## Verify
- `python3 -m http.server` → browser preview; syntax-check inline JS with `node --check`.
- Jared tests with the actual controller; debug overlay reveals its true mapping.
