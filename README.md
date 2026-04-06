# TrainTrack Manager - Docs

<p align="center">
  <img src="media/Preview.png" width="60%">
</p>

### Integrated system for controlling, monitoring, and managing a model railway layout using **Arduino** and **Python**.

---

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
---

## Overview

**TrainTrack Manager** is a smart railway ecosystem that combines:
- **Locomotive control**: Digital DCC control via **DCCpp**.
- **Switch/turnout management**: Manual turnout control and active electrical protections.
- **Position detection**: Real-time tracking through a network of **RFID (MFRC522)** sensors.
- **Desktop application**: Python GUI (Tkinter) with concurrent handling (thread/queue).
- **Video monitoring (optional)**: Video stream integration with OpenCV.

![Cover Image](media/cover-image.jpg)  
*TrainTrack Manager layout in full setup during a test session.*

---

## Project status (important)

Currently available:
- Full GUI control of **multiple locomotives at the same time**
- **Manual** control of all turnouts (switches)
- Active **RFID tag detection** and data exchange to track where a train is at any moment (application-side)
- Optional camera-based **second view** (OpenCV) for live monitoring

>**Work in progress:** the **automatic mode** is not complete yet.  
>In particular, the logic that **automatically triggers turnouts** based on detected position (RFID) and assigned route is still missing.

---

## Related repositories

- **Code (app + firmware):** `AlessioCammarata/TrainTrack-Manager` (Private)
- **Documentation (this repo):** `AlessioCammarata/TrainTrack-Manager-Docs` (Public)

---

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

---

## Software architecture

* **Python (GUI + logic):** OOP GUI built with **Tkinter**.
* **Concurrency:** `threading` and `queue` (FIFO) for asynchronous sensor reading without blocking the UI.
* **Serial communication:** `pyserial` for continuous PC ↔ Arduino communication.
* **Computer Vision:** Video stream integration via **OpenCV** for live monitoring.

![Logic Structure](media/logic-structure.png)  
*Logical dependency diagram between software modules.*

---

## Automation & safety

The control algorithm runs continuously to ensure layout safety:

1. **Acquisition**: RFID events are read from a FIFO queue.
2. **Analysis**: Computation of **critical points** (intersections and possible conflicts between assigned routes).
3. **Intervention (WIP)**: Automatic turnout handling and/or locomotive stop to prevent collisions (automatic turnout triggering is not complete yet).

---

## Track layout

![High Ground View](media/highground.jpg)  
*Top view of the TrainTrack Manager layout during automation tests.*

---

## Technical references

* **DCCpp**: Stack for DCC digital locomotive control.
* **MFRC522**: RFID sensor driver.
* **pySerial**: Python ↔ Arduino serial communication.

---

## Author

**Alessio Cammarata** — Project developed as final work for the Italian high school graduation exam (Esame di Stato), A.S. 2023/2024 (Computer Science & Telecommunications).

---

## License

This project is released under the **MIT** license. See `LICENSE` for details.

---

# 🇮🇹 Versione Italiana

### Sistema integrato per il controllo, il monitoraggio e la gestione di un plastico ferroviario tramite **Arduino** e **Python**.

---

## Download e Release (Pre-release)

L'ultima versione dell'applicazione è disponibile come **eseguibile standalone per Windows 64-bit**.

* **Download**: [Pagina delle Release](https://github.com/AlessioCammarata/TrainTrack-Manager-Docs/releases)
* **Installazione**: 
    1. Scarica il file `TrainTrackManager_v0.9.0_Win64.zip` dalla sezione **Assets** (NON scaricare i file "Source code").
    2. Estrai la cartella sul tuo PC.
    3. Avvia `TrainTrackManager.exe`.
  
>Importante: Non spostare il file TrainTrackManager.exe al di fuori della cartella estratta. La struttura delle cartelle deve rimanere esattamente così com'è; l'eseguibile ha bisogno di trovare le sottocartelle /assets e /languages nella loro posizione originale per funzionare .
* **Nota**: Mantieni le cartelle `/assets` e `/languages` nella stessa directory dell'eseguibile per il corretto funzionamento dell'interfaccia.
* **Preview Mode**: È possibile esplorare la GUI e il database anche senza Arduino collegato.
---

## Panoramica

**TrainTrack Manager** è un ecosistema domotico che combina:
- **Controllo locomotive**: Gestione digitale DCC tramite libreria **DCCpp**.
- **Gestione scambi**: Comando manuale dei deviatoi e protezioni elettriche attive.
- **Rilevamento posizione**: Tracking in tempo reale tramite rete di sensori **RFID (MFRC522)**.
- **Applicazione desktop**: Interfaccia grafica in Python (Tkinter) con gestione concorrente (thread/queue).
- **Monitoraggio video (opzionale)**: Integrazione flussi video con OpenCV.

![Cover Image](media/cover-image.jpg)  
*Il plastico ferroviario TrainTrack Manager in assetto completo durante una sessione di test.*

---

## Stato del progetto (importante)

Attualmente sono disponibili:
- Controllo completo da GUI di **più locomotive contemporaneamente**
- Comando **manuale** di tutti gli scambi (deviatoi)
- **Rilevazione tag RFID** attiva e scambio dati per capire dove si trova un treno in ogni momento (lato applicazione)
- **Second view** con videocamera (OpenCV) opzionale per il monitoraggio live

🚧 **In sviluppo:** la modalità **automatica** non è ancora completa.  
In particolare manca la logica che attiva **automaticamente i deviatoi** in base alla posizione rilevata (RFID) e al percorso assegnato.

---

## Repository collegati

- **Codice (app + firmware):** `AlessioCammarata/TrainTrack-Manager` (Privato)
- **Documentazione (questa repo):** `AlessioCammarata/TrainTrack-Manager-Docs` (Pubblico)

---

## Architettura Hardware (high-level)

Il progetto adotta un approccio a “doppio livello” separando la potenza dalla logica dei sensori:

### 1) Controllo Potenza & Locomotive — Arduino Mega 2560
* Generazione e gestione del segnale DCC tramite libreria **DCCpp**.
* Invio comandi ai decoder delle locomotive attraverso **Motor Shield Rev3**.

![Motor Shield](media/MotorShield.jpg)

### 2) Tracking & Sensori — Arduino Uno Rev3
* Rete di sensori **RFID MFRC522** per identificare univocamente le locomotive al passaggio.
* Comunicazione standard su bus **SPI**.

![RFID Detector](media/RFIDdetector.jpg)

### Gestione scambi e protezione circuitale
* Modulo **relè optoisolato** per comandare i deviatoi a 18V, garantendo la separazione fisica tra potenza e logica di Arduino.
* Utilizzo di diodi e LED polarizzati per mitigare i ritorni induttivi dalle bobine.

![Optoisolator Turnouts](media/OptoisolatorTurnouts.jpg)

---

## Architettura Software

* **Python (GUI + logica):** Interfaccia grafica OOP sviluppata in **Tkinter**.
* **Concorrenza:** Gestione tramite `threading` e `queue` (logica FIFO) per la lettura asincrona dei sensori senza bloccare la UI.
* **Comunicazione seriale:** Libreria `pyserial` per il dialogo costante PC ↔ Arduino.
* **Computer Vision:** Integrazione flussi video via **OpenCV** per il monitoraggio live.

![Logic Structure](media/logic-structure.png)  
*Diagramma delle dipendenze logiche tra i moduli del programma.*

---

## Automazione e Sicurezza

L’algoritmo di controllo lavora in ciclo continuo per garantire la sicurezza del plastico:

1. **Acquisizione**: Lettura degli eventi RFID dalla coda FIFO.
2. **Analisi**: Calcolo dei **punti critici** (intersezioni e potenziali conflitti tra i percorsi assegnati).
3. **Intervento (WIP)**: Gestione automatica dei deviatoi e/o arresto della locomotiva per prevenire collisioni (attivazione automatica deviatoi non ancora completa).

---

## Layout del Circuito

![High Ground View](media/highground.jpg)  
*Vista zenitale del plastico ferroviario TrainTrack Manager durante i test di automazione.*

---

## Riferimenti tecnici

* **DCCpp**: Stack per il controllo digitale DCC delle locomotive.
* **MFRC522**: Driver per sensori RFID.
* **pySerial**: Comunicazione seriale Python ↔ Arduino.

---

## Autore

**Alessio Cammarata** — Progetto realizzato come elaborato per l'Esame di Stato A.S. 2023/2024 (Informatica e Telecomunicazioni).

---

## Licenza

Questo progetto è rilasciato sotto licenza **MIT**. Consulta il file `LICENSE` per maggiori dettagli.