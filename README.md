<h1>
  <img src="images/logo.png" alt="Eu-152 logo" width="48">
  Eu-152 — Cross-platform Gamma Spectroscopy App
</h1>

Eu-152 is a no-frills desktop and mobile application for gamma spectroscopy. One consistent UI and one analysis pipeline from pulses to a calibrated spectrum. 
No Python. No web UI. Just a standard executable JAR you can double-click and use.

- Runs on Windows, Linux, and macOS  
- Works on Raspberry Pi  
- Backward-compatible build for Windows XP SP3 (Java 8)
- Runs on Android with USB Audio Codec support
  
![Java](https://img.shields.io/badge/Java-8+-blue)
![Platform](https://img.shields.io/badge/platform-cross--platform-lightgrey)

---

## Table of contents

- [Overview](#overview)
- [Supported inputs](#supported-inputs)
- [Why Eu-152](#why-eu-152)
- [Downloads](#downloads)
- [How to run](#how-to-run)
- [Quick start: USB audio](#quick-start-usb-audio)
- [Features in detail](#features-in-detail)
- [Current status and roadmap](#current-status-and-roadmap)
- [Screenshots](#screenshots)
- [Contact and feedback](#contact-and-feedback)
- [License](#license)

---

## Overview

Eu-152 provides a consistent workflow whether you acquire via EPICS, a simple serial protocol, or plain USB audio. Create ROIs, run auto-peak to seed candidates, refine them, calibrate using known lines (for example Eu-152), and export your results.

It is written entirely in Java: if your system runs Java, it runs Eu-152.

---

## Supported inputs

1) **EPICS Channel Access**  
   - Example: connect a Canberra 556AIM in your NIM crate and expose it via EPICS.  
     I strongly suggest you to read the Nuclear Physics Lab "NPL" blog about this: [Amateur Camberra spectroscopy](http://www.nuclearphysicslab.com/npl/npl-home/spectroscopy/software_and_hardware/diy-canberra-system/)

2) **Simple SH-Protocol v2 over serial**  
   - Example: Atom Spectra devices.  
   - SH menu in Eu-152 lets you **Start**, **Stop**, **Reset**, and configure serial ports.

3) **Plain USB audio (PCM) devices**  
   - Example: Theremino, Gamma Spectacular, and high-resolution USB codec devices such as "Cubino" and experimental boards.

4) **Open Gamma Protocol** (text-based serial)  
   - Works with devices like the **Open Gamma Detector** on Raspberry Pi Pico.  
   - Supports commands like `set mode energy`, `set out spectrum`, and `reset spectrum`.

---

## Why Eu-152

- Same workflow across lab gear (EPICS), bench serial devices, and sound cards at home  
- Portable JAR, zero complex installation  
- Practical defaults with full manual control when needed  
- Focus on the job, not on themed UIs or arbitrary constraints  

---

## Downloads

- Stable and also backward-compatible build for all kind of systems (Java 8):  
  from here, on GitHub or from my Google Drive:  
  [Download Link Eu-152](https://drive.google.com/file/d/1mcc90R8HlZffilprH9flhV1MmWTFNG62/view?usp=sharing)

- OpenJDK for WindowsXP legacy Java installer:  
  [Download OpenJDK 1.8 Windows legacy](https://drive.google.com/file/d/1sPy953caLw_NI2v_q8BpZ12EZcA1DtF-/view?usp=sharing)

---

## How to run

**On Linux and Raspberry Pi:**
```bash
java -jar Eu152.jar
```

**On Windows and macOS:**
- Double-click `Eu152.jar`

If it does not open, install OpenJDK 1.8.  
Sometimes even on Windows, you may need to use:
```
java -jar Eu152.jar
```

---

## Quick start: USB audio

1. Pick device, sample rate, and channel (L/Mono or R)  
2. Set input level as high as possible without clipping  
3. Set LLD around 4–6% of full scale to suppress baseline noise
4. The other parameters are usually good as per default. In case them are not:  
  a. Choose smoothing taps close to pulse width shown in preview  
  b. If activity piles up near channel 0, enable band-pass filter and raise LLD  
  c. Use Height for clean pulses; Area is more stable with noisy shapes  
  d. Use the two oscilloscopes in the settings panel to tune things live

---

## Features in detail

### USB codec acquisition path

- Trigger with LLD  
- Baseline estimation  
- Optional band-pass prefilter  
- Smoothing  
- Pulse height and area measurement  
- Pile-up and saturation rejection  
- CPS calculation  
- Histogramming to 1024 bins  

### Common analysis tools (all inputs)

- ROI management with totals and net counts  
- Auto-peak to seed candidates  
- FWHM calculator  
- Energy calibration (linear or quadratic)  
- Save/load energy calibration as a separate file  
- PNG export  
- Portable CSV format for loading and saving spectra  
- Multipage printing with clean ROI table on second page  

### Open Gamma Protocol (serial text protocol)

- Recognizes serial output from Open Gamma Detector (Pico firmware)  
- Commands supported: `set mode energy`, `set out spectrum`, `reset spectrum`  
- Two output modes supported:  
  - `SPECTRUM`: single-line full histogram  
  - `EVENTS`: bin stream, accumulable into a histogram  
- Automatic ASCII parsing and visual feedback

### SH Protocol serial improvements

- SH menu with `Port Setup`, `Start`, `Stop`, and `Reset`  
- Supports ASCII log display and device control from GUI  
- Useful for Atom Spectra or Arduino-like boards

### Interactive vertical marker

- A movable vertical red cursor in the spectrum view  
- Shows live energy and channel  
- Usable via keyboard arrows or mouse wheel  
- Great for identifying lines and refining ROIs

### Auto-peak finder dialog

- Opens a live configuration popup  
- Parameters:  
  - Sensitivity  
  - Min width (in channels)  
  - Max width (in channels)  
- Updates the results in real time  
- Includes OK and Exit buttons with cancel behavior

### Save/Load in NPES JSON format

- Stores:  
  - Spectrum histogram  
  - ROIs  
  - Calibration  
  - Peak fits  
  - Display settings  
- Files are JSON and portable across versions  
- Use the main Save/Load buttons in the app

---

## Current status and roadmap

**Current:**

- Acquisition via EPICS, SH serial, and USB audio  
- ROI creation, auto-peak, calibration  
- CSV, PNG, and NPES JSON export/import  
- SH and Open Gamma serial protocols  
- Multipage printing with clean layout  
- Cross-platform builds

**Planned:**

- More hobby protocol support  
- Further DPI-aware layout improvements  
- UX and documentation polish based on feedback  
- Auto-versioning integration  
- Public GitHub releases and changelog structure

---

## Screenshots

![](images/Eu152_1.png)  
![](images/Eu152_2.png)  
![](images/Eu152_3.png)  
![](images/Eu152_4.png)  
![](images/Eu152_5.png)  

---

## Contact and feedback

If you test Eu-152 with your setup (EPICS, SH serial, or USB audio), please share:

- Notes on your configuration  
- Hardware description  
- Screenshots or saved spectra files  
- Parameters that worked well for your hardware  

Your feedback helps set smarter defaults and prioritize improvements.

Mail to: [l.i.papadopol@gmail.com](mailto:l.i.papadopol@gmail.com)

---

## License

At the moment this is a closed source project cause will become - probably - my thesis project.  
I'll set it open source when the thesis will be published.

