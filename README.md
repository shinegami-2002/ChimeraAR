# Chimera AR — Mixed Reality Painting for Meta Quest 3

![Unity](https://img.shields.io/badge/Unity-6-000000?logo=unity&logoColor=white)
![C#](https://img.shields.io/badge/C%23-239120?logo=csharp&logoColor=white)
![Meta Quest](https://img.shields.io/badge/Meta_Quest_3-1877F2?logo=meta&logoColor=white)
![OpenXR](https://img.shields.io/badge/OpenXR-Spatial_Computing-FF6F00)

A mixed-reality painting application for Meta Quest 3 that lets you paint directly onto real-world surfaces using AR passthrough. Scan your room, pick materials and colors, and create art on your walls, floors, and furniture in real time.

## Demo

https://github.com/user-attachments/assets/demo.mp4

> *30-second preview — full demo available on request*

---

## Features

- **Room Scanning** — Uses Meta's Mixed Reality Utility Kit (MRUK) to scan and detect real-world surfaces (walls, floors, furniture)
- **Surface Painting** — Raycast-based painting system that stamps decals onto detected surfaces with accurate normal alignment
- **Material Gallery** — Cycle through preset materials and painting textures (colors, images, patterns)
- **Continuous & Stamp Modes** — Toggle between single-click stamp placement and continuous painting with trigger hold
- **Adjustable Tile Sizes** — 4 sizes (5cm, 10cm, 20cm, 40cm) for fine detail or broad strokes
- **Undo & Clear** — Undo last paint stroke or clear entire canvas
- **Haptic Feedback** — Controller vibration feedback on paint, button clicks, and mode switches
- **Wrist Menu** — Toggle-able wrist-mounted UI palette for quick access to tools
- **Audio Feedback** — Sound effects for painting actions and UI interactions

---

## Tech Stack

| Component | Technology |
|-----------|-----------|
| **Engine** | Unity 6 |
| **Language** | C# |
| **XR Platform** | Meta Quest 3 |
| **XR SDK** | Meta XR SDK, OpenXR, XR Interaction Toolkit |
| **Spatial** | Meta Mixed Reality Utility Kit (MRUK), OVRScene |
| **Rendering** | Universal Render Pipeline (URP), custom materials |
| **Input** | OVRInput (controller tracking, hand triggers, haptics) |

---

## Architecture

```
                    Meta Quest 3
                         |
            +------------+------------+
            |                         |
      Room Scanning              Painting System
      (RoomScanManager)          (ChimeraPainter)
            |                         |
    OVRScene.RequestSpaceSetup   Raycast → Surface Detection
            |                         |
    MRUK.LoadSceneFromDevice     Decal Spawning + Normal Alignment
                                      |
                              +-------+-------+
                              |       |       |
                          Materials  Sizes   Modes
                          Gallery   Toggle  (Stamp/Continuous)
```

### Core Scripts

| Script | Responsibility |
|--------|---------------|
| `ChimeraPainter.cs` | Main painting logic — raycasting, decal placement, material selection, size toggling, undo/clear, haptic feedback |
| `RoomScanManager.cs` | Triggers Meta Quest room scanning via `OVRScene.RequestSpaceSetup()`, reloads scene data on app resume |
| `MaterialButton.cs` | UI component for color/material selection buttons |
| `MenuToggle.cs` | Wrist-mounted menu toggle via left controller button |

---

## Controls

| Controller | Button | Action |
|-----------|--------|--------|
| **Right** | Index Trigger | Paint / Select UI |
| **Right** | Hand Trigger | Undo last stroke |
| **Left** | Index Trigger | Toggle continuous/stamp mode |
| **Left** | A Button | Clear all paint |
| **Left** | Start/Y Button | Toggle wrist menu |

---

## Getting Started

### Prerequisites

- Unity 6 (or later)
- Meta Quest 3 headset
- Meta XR SDK and MRUK packages installed via Unity Package Manager

### Build & Deploy

```bash
# Clone the repo
git clone https://github.com/shinegami-2002/ChimeraAR.git

# Open in Unity 6
# File → Build Settings → Android → Meta Quest 3
# Build and Run
```

### APK

A pre-built APK is included at `Chimera_AR.apk` — sideload via:

```bash
adb install Chimera_AR.apk
```

---

## License

MIT
