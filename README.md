# Shred of the Dragon 🎸

A single-file Guitar Hero that runs in your browser. No build step, no
dependencies, no copyrighted music — the song is synthesized live with the
Web Audio API and the note chart is generated from the same melody, so
audio and chart can never drift apart.

## Play

```bash
python3 -m http.server 8321
# open http://localhost:8321
```

Then press **Enter** (or strum a connected Guitar Hero controller).

### Controls

| Input | Action |
| --- | --- |
| `Q W E R T` / `1-5` / `A S D F G` | frets (green → orange) |
| `Space` / `Enter` / arrows | strum |
| `P` | watch mode (plays itself) |
| `[` `]` | latency calibration ±10ms |

A Guitar Hero guitar over USB shows up as a standard gamepad
(Xbox 360 X-plorer mapping: frets = A/B/Y/X/LB, strum = d-pad up/down).
The title screen shows raw button indices if yours maps differently.

### URL params

- `?baby=1` — one note at a time, forgiving window
- `?hard=1` — full 16th-note shred, tight window
- `?kb=1` — keyboard only, ignore the gamepad
- `?auto=1` / `?play=1` — launch straight into watch mode

## The song

"Shred of the Dragon" — an original ~200 BPM E-harmonic-minor shred track
in the spirit of the classic: arpeggio intro, gallop riff, melodic verse,
16th-note solo, finale stabs. All oscillator + noise synthesis, rendered
offline into one buffer for sample-accurate timing.
