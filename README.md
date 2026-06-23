# HandPilot

Use your hand to control your mouse and fly a drone. Built with Python and Google MediaPipe, it tracks your hand in real time and turns your gestures into actions. No controller, no keyboard — just your hand.

## What It Does

- Tracks 21 points on your hand using your camera
- Maps your index fingertip to the mouse cursor
- Detects pinch gestures to trigger clicks
- Designed to also control a drone — same hand, same gestures

## Gestures

| Gesture | Action |
|---|---|
| ☝️ Index finger up | Move cursor |
| ☝️ Index + thumb pinch | Right click |
| ✌️ Index + middle up, thumb pinches middle | Left click |
| 🤙 Pinky up, hand high | Scroll up |
| 🤙 Pinky up, hand low | Scroll down |

## How It Works

Google MediaPipe detects 21 landmarks on your hand every frame.

```
4  ← thumb tip
8  ← index tip  (drives the cursor)
12 ← middle tip
20 ← pinky tip
0  ← wrist
```

Each frame:
1. Camera captures your hand
2. MediaPipe returns 21 landmarks
3. Code checks which fingers are up
4. Index tip maps to screen coordinates
5. Smoothing removes jitter
6. Mouse event fires

## Files

- `mouse_control.py` — run this
- `hand_tracker.py` — MediaPipe wrapper and gesture logic
- `requirements.txt` — dependencies

## Setup

```bash
git clone https://github.com/YOUR_USERNAME/handpilot.git
cd handpilot

python3 -m venv .venv
source .venv/bin/activate      # macOS / Linux
.venv\Scripts\activate         # Windows

pip install -r requirements.txt
python mouse_control.py
```

macOS only: System Settings → Privacy & Security → Accessibility → add Terminal → toggle ON.

## Tuning

Edit these at the top of `mouse_control.py`:

| Constant | Default | Effect |
|---|---|---|
| `SMOOTHING` | `6` | Higher = smoother but laggier |
| `PINCH_DIST` | `45` | How close fingers must be to click (px) |
| `FRAME_MARGIN` | `150` | Dead-zone border around camera frame |
| `CLICK_COOLDOWN` | `18` | Frames between allowed clicks |

## Roadmap

### Phase 1 — Hand Mouse ✅
- [x] Hand skeleton tracking via MediaPipe
- [x] Index fingertip controls the cursor
- [x] Pinch gestures for left and right click
- [x] Pinky gesture for scroll

### Phase 2 — Drone Camera 🔜
Replace the webcam with the drone's live camera. One line change:

```python
CAP_SOURCE = 0                           # webcam (now)
CAP_SOURCE = "udp://192.168.10.1:11111"  # DJI Tello
CAP_SOURCE = "rtsp://192.168.1.1/stream" # custom drone
```

### Phase 3 — Drone Flight Control 🔜
Map gestures to flight commands:

| Gesture | Drone command |
|---|---|
| Open palm, move up | Throttle up |
| Open palm, move down | Throttle down |
| Tilt hand left / right | Roll |
| Tilt hand forward / back | Pitch |
| Fist | Hover |
| Two fingers up | Emergency stop |

### Phase 4 — Autonomous Assist 🔜
- Obstacle detection using the drone camera and OpenCV
- Hand gesture overrides auto-hover
- Return-to-home gesture

## Tech Stack

- [MediaPipe](https://developers.google.com/mediapipe) — hand tracking
- [OpenCV](https://opencv.org/) — camera and visual overlay
- [pyautogui](https://pyautogui.readthedocs.io/) — mouse control
- [NumPy](https://numpy.org/) — coordinate mapping

## License

MIT
