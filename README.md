# Posture Coach

Real-time posture detection in your browser — no install, no server, no account.

## What it does

- Detects your posture live via webcam using MediaPipe Pose
- Scores your posture 0–100 in real time
- Colour-codes your skeleton: green = good, amber = warning, red = bad
- Alerts you after 8 seconds of bad posture
- Tracks good vs bad posture time for the session

## Checks

| Check | What it detects |
|-------|----------------|
| Head level | Ear height difference (tilting left/right) |
| Shoulders even | One shoulder higher than the other |
| Not slouching | Shoulders rounding forward |
| Neck upright | Head drifting forward of shoulders |

## How to use

1. Download `index.html`
2. Open it in **Firefox** (camera works on local files without a server)
3. Allow camera access when prompted
4. Sit up straight, look forward → click **Calibrate**
5. Start working — the coach watches your posture and alerts you when needed

> **Chrome users:** serve the file with any local server, e.g. `python -m http.server 8080` then open `http://localhost:8080`

## How it works

```
Webcam → MediaPipe Pose (33 landmarks)
                ↓
    Calibration snapshot (baseline metrics)
                ↓
    Per-frame: compare current vs baseline
      • ear height diff   → head tilt
      • shoulder y diff   → unevenness
      • shoulder width    → slouch ratio
      • ear-shoulder x    → neck forward
                ↓
    Score (0-100) + colour-coded skeleton overlay
                ↓
    Alert after 8s consecutive bad posture
```

## Tech

- **MediaPipe Pose** (CDN) — 33-point skeleton, runs fully in-browser
- **Canvas 2D API** — skeleton drawing with glow effects
- **Vanilla JS / HTML / CSS** — zero dependencies, zero build step

## Privacy

Everything runs locally in your browser. No video is sent anywhere. No data is stored.
