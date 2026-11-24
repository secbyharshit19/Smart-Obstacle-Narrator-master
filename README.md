# 👁️ SMART OBSTACLE NARRATOR | AI-Powered Assistive Vision

### Real-Time Obstacle Detection, Spatial Reasoning & Voice Alerts for Visual Accessibility

<p align="center">
  An AI-powered assistive vision prototype exploring how computer vision and spoken feedback can help blind people and people with visual impairments better understand their surroundings.
</p>

<p align="center">
  <a href="https://smart-obstacle-narrator-1.streamlit.app/">
    🚀 <b>Live Demo</b>
  </a>
  &nbsp;|&nbsp;
  <a href="https://github.com/Harshit-Soni-1905/Smart-Obstacle-Narrator">
    📂 <b>Repository</b>
  </a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python">
  <img src="https://img.shields.io/badge/PyTorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white" alt="PyTorch">
  <img src="https://img.shields.io/badge/YOLO11-111F68?style=for-the-badge&logo=ultralytics&logoColor=white" alt="YOLO11">
  <img src="https://img.shields.io/badge/OpenCV-5C3EE8?style=for-the-badge&logo=opencv&logoColor=white" alt="OpenCV">
  <img src="https://img.shields.io/badge/ByteTrack-Object_Tracking-2F855A?style=for-the-badge" alt="ByteTrack">
  <img src="https://img.shields.io/badge/Streamlit-FF4B4B?style=for-the-badge&logo=streamlit&logoColor=white" alt="Streamlit">
  <img src="https://img.shields.io/badge/WebRTC-333333?style=for-the-badge&logo=webrtc&logoColor=white" alt="WebRTC">
  <img src="https://img.shields.io/badge/pytest-0A9EDC?style=for-the-badge&logo=pytest&logoColor=white" alt="pytest">
</p>

---

## 🌍 The Mission: Exploring More Accessible Mobility

For people who are blind or have visual impairments, understanding nearby obstacles and navigating unfamiliar environments can present significant challenges. Assistive technologies can provide additional information about the surrounding environment through non-visual feedback.

**Smart Obstacle Narrator explores how computer vision and real-time audio narration could help make environmental information more accessible.**

The prototype processes camera frames to detect common objects, estimate their approximate proximity and image-relative direction, and prioritize selected warnings. Instead of requiring the user to interpret every visual detection, the system communicates selected information through concise spoken alerts.

The project aims to explore an additional source of environmental awareness—not replace existing mobility aids or established navigation practices.

> **Accessibility goal:** Investigate how real-time AI perception and spoken feedback can help people with visual impairments access useful information about their surroundings.

## 📌 Overview

Detecting an object is only one part of understanding a scene. For assistive applications, the system must also consider where an object appears, how close it seems, whether it intersects an estimated walking corridor, and whether announcing it is useful at that moment.

Smart Obstacle Narrator combines:

- **Object detection** to identify common objects in a camera feed.
- **Persistent tracking** to associate objects across video frames.
- **Spatial reasoning** to estimate image-relative direction and approximate proximity.
- **Hazard prioritization** to rank potential warnings using spatial and object-related signals.
- **Event-driven narration** to reduce repetitive announcements.
- **Text-to-speech** to communicate selected alerts through audio.

The project provides both a desktop application and a browser-based demonstration.

### The Problem

- People with visual impairments may benefit from additional information about nearby objects and potential obstacles.
- Object detectors produce visual labels and bounding boxes, which are not directly accessible through audio alone.
- Announcing every object repeatedly can make audio feedback overwhelming.
- Camera-based distance estimates are uncertain and can be affected by lighting, camera placement, and occlusion.

### The Approach

The system converts visual detections into contextual, prioritized alerts:

```text
Camera Input
     ↓
YOLO11 Object Detection
     ↓
ByteTrack Object Tracking
     ↓
Relative Proximity & Direction Estimation
     ↓
Walking-Corridor Reasoning
     ↓
Potential Hazard Prioritization
     ↓
Event Filtering & Cooldowns
     ↓
Concise Spoken Alerts
```

The goal is to explore whether this pipeline can provide useful supplementary environmental feedback for assistive mobility applications.

---

## 🎯 Project Objectives

The project investigates how AI-powered computer vision can contribute to more accessible environmental awareness.

Its objectives are to:

- Detect common objects in a live camera feed.
- Estimate approximate relative proximity and image-relative direction.
- Track objects across frames to maintain temporal context.
- Identify objects that overlap with a projected walking corridor.
- Prioritize potential hazards instead of announcing every detection equally.
- Reduce repetitive audio alerts through cooldowns and event deduplication.
- Deliver spoken feedback through desktop and browser interfaces.
- Monitor processing latency and frame rate.
- Provide a platform for further research into accessible computer vision systems.

---

## 🏗️ Architecture

```text
                Camera / Video Frame
                         │
                         ▼
                 YOLO11 Detector
                         │
                         ▼
                    ByteTrack
                 Object Tracking
                         │
                         ▼
               Spatial Estimation
                ┌────────┴────────┐
                ▼                 ▼
          Direction Mapping  Relative Depth
                │                 │
                └────────┬────────┘
                         ▼
              Walking-Corridor Model
                         │
                         ▼
                Hazard Prioritizer
                         │
                         ▼
                 Event Narrator
              (Cooldowns & Filtering)
                         │
                         ▼
                 Spoken Feedback
                ┌────────┴────────┐
                ▼                 ▼
            Desktop TTS       Browser TTS
```

### Core Processing Stages

**1. Object Detection**

YOLO11 identifies objects in incoming camera frames and returns bounding boxes, class labels, and confidence scores.

**2. Persistent Tracking**

ByteTrack associates detections across frames and maintains track IDs where available. This helps distinguish continuing objects from newly appearing ones.

**3. Spatial Estimation**

The system estimates image-relative direction and approximate proximity using bounding-box geometry and perspective cues. These are heuristic estimates, not calibrated physical measurements.

**4. Walking-Corridor Reasoning**

A perspective-projected corridor approximates the expected walking region in the image. Overlap with this region contributes to potential hazard prioritization.

**5. Hazard Prioritization**

The system combines available spatial and object information to rank potential hazards. These rankings do not guarantee that an object will cause a collision.

**6. Event-Driven Narration**

The event system handles new objects, proximity escalation, urgency escalation, and periodic reminders. Cooldowns and deduplication help reduce repeated announcements.

**7. Audio Feedback**

Selected alerts are communicated using native desktop speech or browser-based speech synthesis.

---

## ✨ Features

| Feature | Description |
|---|---|
| **AI Object Detection** | YOLO11-based detection of common objects |
| **Multi-Object Tracking** | ByteTrack association across frames |
| **Relative Proximity Estimation** | Approximate NEAR, MEDIUM, and FAR categories |
| **Directional Reasoning** | Image-relative LEFT, AHEAD, and RIGHT zones |
| **Walking-Corridor Analysis** | Perspective-based estimation of potential path overlap |
| **Hazard Prioritization** | Urgency scoring using proximity, direction, class, and corridor intersection |
| **Event-Driven Alerts** | New-object alerts, escalation events, and periodic reminders |
| **Speech Cooldowns** | Helps reduce repetitive announcements |
| **Desktop Voice Output** | Native Windows SAPI5 speech through pyttsx3 |
| **Browser Voice Output** | Client-side Web Speech API |
| **WebRTC Webcam Demo** | Browser-based video streaming with session-isolated processing |
| **Performance Monitoring** | FPS, inference latency, total latency, and active-track metrics |
| **Automated Testing** | Regression and integration tests for core behavior |

---

## 🧠 Why This Matters for Visual Accessibility

Traditional object detection produces information such as labels and bounding boxes. For a person who cannot easily access that visual output, spoken descriptions can offer another way to receive selected environmental information.

Smart Obstacle Narrator explores three ideas:

| Accessibility consideration | Project approach |
|---|---|
| **Non-visual feedback** | Communicates selected detections through spoken alerts |
| **Contextual information** | Adds approximate direction and proximity categories |
| **Reduced audio clutter** | Uses prioritization, event handling, and cooldowns to limit repetitive announcements |

For example, the system may generate an alert describing an object as being ahead or to one side, with an approximate proximity category.

These are examples of the intended feedback style, not guarantees that the system will identify every obstacle or provide accurate navigation instructions.

**The intended benefit is supplementary environmental awareness for people with visual impairments.** Whether the system is useful, understandable, and safe in real-world mobility settings requires dedicated testing with users and accessibility professionals.

---

## 🌐 Live Demo

<p align="center">
  <a href="https://smart-obstacle-narrator-1.streamlit.app/">
    🚀 <b>Launch Smart Obstacle Narrator</b>
  </a>
</p>

The hosted demonstration provides browser-based video processing, annotated detections, telemetry, captions, and spoken alerts.

### How to Try It

1. Open the live demo.
2. Grant camera permission when prompted.
3. Start the webcam stream.
4. Point the camera at common objects in a well-lit environment.
5. Observe the annotated detections and telemetry.
6. Enable voice alerts and use **Test Voice** to check browser speech.
7. Observe how alerts change as objects move through the scene.

### Web Demo Architecture

- **Video input:** Browser webcam access through WebRTC.
- **Processing:** The hosted application processes incoming frames using the vision pipeline.
- **Audio:** Browser speech synthesis reads alert text through the Web Speech API.
- **Session isolation:** Each connection receives its own processing pipeline and tracking state.

**Privacy note:** In the hosted configuration, camera frames are transmitted to the server for inference. Do not assume frames remain exclusively on the visitor's device. The application is designed not to store or log user video or audio, but users should review the implementation and hosting behavior before using sensitive footage.

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Programming Language | Python |
| Deep Learning | PyTorch |
| Object Detection | Ultralytics YOLO11 |
| Object Tracking | ByteTrack |
| Image Processing | OpenCV |
| Spatial Reasoning | Bounding-box geometry and perspective heuristics |
| Desktop Speech | pyttsx3 / Windows SAPI5 |
| Web Framework | Streamlit |
| Video Streaming | streamlit-webrtc / WebRTC |
| Browser Speech | Web Speech API |
| Configuration | YAML and environment variables |
| Testing | pytest |
| Version Control | Git and GitHub |
| Deployment | Streamlit Community Cloud |

---

## 💻 Run Locally

### Prerequisites

- Python 3.12 or a compatible Python version supported by the dependencies.
- A webcam for live camera operation.
- Windows 10/11 for native SAPI5 speech.
- An NVIDIA GPU with compatible CUDA support is recommended for faster inference. CPU inference may also be possible.

### 1. Clone the Repository

```bash
git clone https://github.com/Harshit-Soni-1905/Smart-Obstacle-Narrator.git
cd Smart-Obstacle-Narrator
```

### 2. Create a Virtual Environment

**Windows:**

```powershell
python -m venv .venv
.venv\Scripts\activate
```

**Linux/macOS:**

```bash
python -m venv .venv
source .venv/bin/activate
```

### 3. Install Dependencies

Install PyTorch using the instructions appropriate for your operating system and hardware. Refer to [`docs/environment.md`](docs/environment.md) for environment guidance.

Install the project and development dependencies:

```bash
pip install -e ".[dev]"
```

For the web demo, install its additional dependencies if necessary:

```bash
pip install -r requirements-demo.txt
```

### 4. Run the Desktop Application

```bash
python -m narrator
```

The default model is `yolo11s.pt`.

To override the model:

**Windows PowerShell:**

```powershell
$env:NARRATOR_MODEL = "yolo11n.pt"
python -m narrator
```

**Linux/macOS:**

```bash
NARRATOR_MODEL=yolo11n.pt python -m narrator
```

Model weights may be downloaded automatically when required and are not committed to the repository.

### 5. Run the Web Demo

```bash
streamlit run app.py
```

Open `http://localhost:8501`, grant camera permission, and start the video stream.

---

## ⌨️ Desktop Controls

| Key | Action |
|---|---|
| `q` / `Esc` | Quit the application |
| `m` | Toggle voice alerts |
| `c` | Toggle the collision-risk overlay |
| `Space` | Pause or resume processing |

---

## ⚙️ Configuration

| File | Purpose |
|---|---|
| `config/default.yaml` | Default detector, speaker, event, corridor, ground, and depth settings |
| `src/narrator/config.py` | Typed configuration handling and environment overrides |
| `pyproject.toml` | Package metadata, dependencies, and pytest configuration |
| `requirements.txt` | Streamlit Community Cloud dependencies |
| `requirements-demo.txt` | Web-demo dependency manifest |
| `packages.txt` | System packages required by the hosted demo |

### Environment Variables

| Variable | Purpose |
|---|---|
| `NARRATOR_MODEL` | Overrides the YOLO model filename |
| `NARRATOR_DEVICE` | Selects the inference device, such as `cuda`, `cpu`, or `auto` |

---

## 🧪 Testing & Verification

Run the full test suite:

```bash
pytest -v
```

Run specific areas:

```bash
# Tracking, event narration, and performance monitoring
pytest tests/test_tracking_and_events.py -v

# WebRTC processing and browser speech bridge
pytest tests/test_web_demo.py -v

# Ground-aware obstacle reasoning
pytest tests/test_ground_aware_reasoning.py -v

# Baseline detection
pytest tests/test_baseline_detection.py -v
```

**Reported verification:** 270 tests passed in a recent full-suite run. Re-run the suite after making changes to confirm the current result.

---

## 📁 Project Structure

```text
Smart-Obstacle-Narrator/
├── app.py
├── config/
│   └── default.yaml
├── demo/
│   ├── __init__.py
│   ├── processor.py
│   └── web_speaker.py
├── docs/
│   ├── architecture.md
│   ├── environment.md
│   └── safety_disclaimer.md
├── models/
│   └── .gitkeep
├── packages.txt
├── pyproject.toml
├── requirements.txt
├── requirements-demo.txt
├── src/
│   └── narrator/
│       ├── __init__.py
│       ├── __main__.py
│       ├── config.py
│       ├── depth.py
│       ├── detector.py
│       ├── diagnostics.py
│       ├── direction.py
│       ├── distance.py
│       ├── events.py
│       ├── ground_plane.py
│       ├── health.py
│       ├── metrics.py
│       ├── phrasing.py
│       ├── pipeline.py
│       ├── prioritizer.py
│       └── speaker.py
├── tests/
│   ├── fixtures/
│   │   └── bus.jpg
│   ├── test_baseline_detection.py
│   ├── test_collision_risk_and_tracking.py
│   ├── test_config.py
│   ├── test_depth_and_phrasing.py
│   ├── test_ground_aware_reasoning.py
│   ├── test_ground_region.py
│   ├── test_health_and_reliability.py
│   ├── test_narrator.py
│   ├── test_relative_depth_and_spatial.py
│   ├── test_tracking_and_events.py
│   ├── test_vocabulary_and_hazards.py
│   └── test_web_demo.py
├── .gitignore
├── LICENSE
└── README.md
```

---

## ⚠️ Known Limitations

- **Missed detections:** Transparent surfaces, thin objects, low-contrast obstacles, and ground-level hazards may not be detected.
- **False positives:** Harmless objects may be reported as potential hazards.
- **Uncalibrated distance:** Monocular estimates may differ substantially from actual physical distances.
- **Image-relative direction:** Direction labels depend on camera position and do not represent precise three-dimensional bearings.
- **Limited field of view:** A single camera cannot observe every side, rear, overhead, or occluded hazard.
- **Processing latency:** Delays between object appearance and spoken alerts may affect responsiveness, especially on CPU-only hosting.
- **Environmental sensitivity:** Low light, rain, fog, glare, and crowded scenes can reduce performance.
- **Audio dependency:** Spoken alerts may not help in noisy environments or for people unable to hear announcements.
- **No certified safety guarantees:** The prototype has not been validated as a primary mobility or collision-avoidance aid.

For further details, see [`docs/safety_disclaimer.md`](docs/safety_disclaimer.md).

---

## 🎓 Key Learnings

This project explores practical concepts across computer vision, AI, and software engineering:

- Integrating YOLO-based detection with multi-object tracking.
- Designing a modular perception-to-narration pipeline.
- Estimating relative proximity and direction from image geometry.
- Implementing perspective-based walking-corridor reasoning.
- Prioritizing events and managing speech cooldowns.
- Measuring FPS, inference latency, and total processing latency.
- Building a browser-based video application with WebRTC and Streamlit.
- Testing tracking, event handling, spatial reasoning, and web integration.
- Exploring accessible feedback interfaces for assistive technology research.

---

## 📜 License

This project is licensed under the MIT License. See [`LICENSE`](LICENSE) for details.

**Third-party dependency notice:** Ultralytics YOLO is licensed under AGPL-3.0. Review the [Ultralytics licensing information](https://www.ultralytics.com/license) for applicable terms, especially for commercial use.

---

## 👨‍💻 Author

**Harshit Soni**

B.Tech — Computer Science & Engineering

Interested in Artificial Intelligence, Machine Learning, Computer Vision, and accessible AI systems.

- GitHub: [Harshit-Soni-1905](https://github.com/Harshit-Soni-1905)

---

<p align="center">
  Built with Python • PyTorch • YOLO11 • OpenCV • ByteTrack • Streamlit
</p>
