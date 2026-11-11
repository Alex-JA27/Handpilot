# HandPilot 🖐️

Control your mouse using just your hand gestures. Built with Python, Google MediaPipe, and OpenCV, HandPilot tracks your hand in real time and translates finger movements into mouse actions.

No physical mouse needed — just your webcam and your hand.

## What It Does

- Tracks 21 hand landmarks in real time using your webcam
- Maps your index fingertip to the mouse cursor
- Detects pinch gestures to trigger left and right clicks
- Enables hands-free scrolling using pinky gestures
- Applies motion smoothing for stable cursor movement
- Uses click cooldowns to prevent accidental repeated clicks

## Gestures

| Gesture | Action |
|---|---|
| ☝️ Index finger up | Move cursor |
| ☝️ Index + thumb pinch | Right click |
| ✌️ Index + middle up, thumb pinches middle | Left click |
| 🤙 Pinky up, hand high | Scroll up |
| 🤙 Pinky up, hand low | Scroll down |

## How It Works

HandPilot uses Google MediaPipe to detect and track 21 landmarks on your hand every frame.

### Key Hand Landmarks

```text
4  ← Thumb tip
8  ← Index fingertip (controls cursor)
12 ← Middle fingertip
20 ← Pinky fingertip
0  ← Wrist
```

### Processing Pipeline

1. Webcam captures live video input
2. MediaPipe detects 21 hand landmarks
3. Gesture recognition identifies finger positions
4. Index fingertip coordinates map to screen coordinates
5. Motion smoothing reduces cursor jitter
6. PyAutoGUI executes the corresponding mouse action

## Project Structure

```text
HandPilot/
├── mouse_control.py    # Main application
├── hand_tracker.py     # MediaPipe wrapper and gesture logic
├── requirements.txt    # Python dependencies
└── README.md           # Project documentation
```

## Installation & Setup

### 1. Clone the Repository

```bash
git clone https://github.com/Alex-JA27/Handpilot.git
cd Handpilot
```

### 2. Create a Virtual Environment

**macOS / Linux:**

```bash
python3 -m venv .venv
source .venv/bin/activate
```

**Windows:**

```bash
python -m venv .venv
.venv\Scripts\activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

### 4. Run HandPilot

```bash
python mouse_control.py
```

### macOS Accessibility Permissions

On macOS, PyAutoGUI requires Accessibility permissions to control the mouse.

1. Open System Settings
2. Navigate to Privacy & Security
3. Select Accessibility
4. Add Terminal (or your Python IDE)
5. Enable Accessibility permissions

## Configuration & Tuning

You can adjust the following constants at the top of `mouse_control.py` to customize performance.

| Constant | Default | Description |
|---|---|---|
| `SMOOTHING` | `6` | Higher values produce smoother but slower cursor movement |
| `PINCH_DIST` | `45` | Maximum fingertip distance required to register a click (px) |
| `FRAME_MARGIN` | `150` | Camera frame margin used for coordinate mapping |
| `CLICK_COOLDOWN` | `18` | Minimum number of frames between clicks |

## Technologies Used

| Technology | Purpose |
|---|---|
| Python | Core application and gesture processing |
| MediaPipe | Real-time hand landmark detection |
| OpenCV | Webcam capture and visual feedback |
| PyAutoGUI | Mouse movement, clicking, and scrolling |
| NumPy | Coordinate mapping and numerical processing |

## Features

- [x] Real-time hand detection and tracking
- [x] 21-point hand landmark detection
- [x] Index fingertip cursor control
- [x] Left-click gesture recognition
- [x] Right-click gesture recognition
- [x] Gesture-based scrolling
- [x] Cursor motion smoothing
- [x] Click cooldown management

## Future Improvements

- [ ] Customizable hand gesture mappings
- [ ] Adjustable sensitivity through a user interface
- [ ] Additional gestures for keyboard shortcuts
- [ ] Improved gesture recognition under varying lighting conditions
- [ ] Multi-hand gesture support

## Project Goal

HandPilot explores how computer vision and gesture recognition can create more intuitive ways for humans to interact with computers.

By combining real-time hand tracking, coordinate mapping, and gesture classification, the project demonstrates how natural hand movements can replace traditional mouse inputs.

## Author

**Alex Alvarado**

[GitHub](https://github.com/Alex-JA27)
