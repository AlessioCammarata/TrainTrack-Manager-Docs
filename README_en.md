<div align="center">
  <h1>TrainTrack Manager - Docs</h1>
  <p align="center">
  <a href="README.md">Italiano</a> | <b>English</b>
</div>

<p align="center">
  <img src="media/Preview.png" width = "45%" height="45%">
</p>

Integrated system for controlling, monitoring, and managing a model railway layout using **Arduino** and **Python**.

<p align="center">
  <video src="https://github.com/user-attachments/assets/e7bc4636-fc0d-448d-9878-869da95e0653"  controls muted autoplay loop>
    The browser does not support the video.
  </video>
</p>

## Download & Releases (Pre-release)

The latest version of the application is available as a **standalone executable for Windows 64-bit**.

* **Download**: [Latest Pre-release v0.9.0-beta](https://github.com/AlessioCammarata/TrainTrack-Manager-Docs/releases)
* **Installation**: 
    1. Download the file `TrainTrackManager_v0.9.0_Win64.zip` from the **Assets** section (do **NOT** download the "Source code" files, as they do not contain the compiled app).
    2. Extract the ZIP folder to your PC.
    3. Run `TrainTrackManager.exe`.
  >Important: Do not move the TrainTrackManager.exe file out of its original folder. The entire extracted directory structure must be kept intact, as the application relies on specific relative paths to access the /assets and /languages folders .
* **Important**: Keep the `/assets` and `/languages` folders in the same directory as the `.exe` file for the GUI to function correctly.
* **Preview Mode**: You can explore the GUI and manage the database even without an Arduino connected.
* **Antivirus Note**: Since the executable is not digitally signed, Windows SmartScreen or your Antivirus might flag it as a "False Positive". You can safely allow the execution.


## Overview

**TrainTrack Manager** is a smart railway ecosystem that combines:
- **Locomotive control**: Digital DCC control via **DCCpp**.
- **Switch/turnout management**: Manual turnout control and active electrical protections.
- **Position detection**: Real-time tracking through a network of **RFID (MFRC522)** sensors.
- **Desktop application**: Python GUI (Tkinter) with concurrent handling (thread/queue).
- **Video monitoring (optional)**: Video stream integration with OpenCV.

![Cover Image](media/cover-image.jpg)  
*TrainTrack Manager layout in full setup during a test session.*



## Project status (important)

Currently available:
- Full GUI control of **multiple locomotives at the same time**
- **Manual** control of all turnouts (switches)
- Active **RFID tag detection** and data exchange to track where a train is at any moment (application-side)
- Optional camera-based **second view** (OpenCV) for live monitoring

>**Work in progress:** the **automatic mode** is not complete yet.  
>In particular, the logic that **automatically triggers turnouts** based on detected position (RFID) and assigned route is still missing.



## Related repositories

- **Code (app + firmware):** `AlessioCammarata/TrainTrack-Manager` (Private)
- **Documentation (this repo):** `AlessioCammarata/TrainTrack-Manager-Docs` (Public)



## Hardware architecture (high-level)

The project follows a “two-layer” approach, separating power handling from sensor logic:

### 1) Power & locomotive control — Arduino Mega 2560
* DCC signal generation and handling via **DCCpp**.
* Commands sent to locomotive decoders through a **Motor Shield Rev3**.

![Motor Shield](media/MotorShield.jpg)

### 2) Tracking & sensors — Arduino Uno Rev3
* Network of **RFID MFRC522** sensors to uniquely identify locomotives when passing.
* Standard communication over the **SPI** bus.

![RFID Detector](media/RFIDdetector.jpg)

### Switch management & circuit protection
* **Opto-isolated relay module** to drive 18V turnouts, ensuring physical separation between power and Arduino logic.
* Use of diodes and polarized LEDs to mitigate inductive kickback from coils.

![Optoisolator Turnouts](media/OptoisolatorTurnouts.jpg)



## Software architecture

* **Python (GUI + logic):** OOP GUI built with **Tkinter**.
* **Concurrency:** `threading` and `queue` (FIFO) for asynchronous sensor reading without blocking the UI.
* **Serial communication:** `pyserial` for continuous PC ↔ Arduino communication.
* **Computer Vision:** Video stream integration via **OpenCV** for live monitoring.

![Logic Structure](media/logic-structure.png)  
*Logical dependency diagram between software modules.*



## Automation & safety

The control algorithm runs continuously to ensure layout safety:

1. **Acquisition**: RFID events are read from a FIFO queue.
2. **Analysis**: Computation of **critical points** (intersections and possible conflicts between assigned routes).
3. **Intervention (WIP)**: Automatic turnout handling and/or locomotive stop to prevent collisions (automatic turnout triggering is not complete yet).



## Track layout

![High Ground View](media/highground.jpg)  
*Top view of the TrainTrack Manager layout during automation tests.*



## Technical references

* **DCCpp**: Stack for DCC digital locomotive control.
* **MFRC522**: RFID sensor driver.
* **pySerial**: Python ↔ Arduino serial communication.



## Author

**Alessio Cammarata** — Project developed as final work for the Italian high school graduation exam (Esame di Stato), A.S. 2023/2024 (Computer Science & Telecommunications).



## License

This project is released under the **MIT** license. See `LICENSE` for details.

