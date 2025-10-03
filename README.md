#**Actively updating:** This repository is under active development 

Ultrasonic Distance Sensing System (MATLAB + Arduino)

> 🚧 **Actively updating:** This repository is under active development; additional plots, calibration results, and a demo video will be added as they’re ready.
> Live distance–time acquisition, calibration, error analysis, and velocity estimation using **HC-SR04**, **Arduino**, and **MATLAB App Designer**.

[![MATLAB](https://img.shields.io/badge/MATLAB-R2023b%2B-orange.svg)](#)
[![Arduino](https://img.shields.io/badge/Arduino-HC--SR04-blue.svg)](#)
[![Platform](https://img.shields.io/badge/OS-Windows%20%7C%20macOS%20%7C%20Linux-lightgrey.svg)](#)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](#license)

---

## Demo

- 🎥 **Video**: _add your link here (YouTube/Drive)_  
- 🖼️ **Screenshots/GIFs**: place in `docs/img/` and embed below.

<p align="center">
  <img src="docs/img/gui_overview.png" alt="MATLAB App Designer GUI" width="720"/>
</p>

---

## Table of Contents
- [Features](#features)
- [System Overview](#system-overview)
- [Bill of Materials](#bill-of-materials)
- [Wiring](#wiring)
- [Quick Start](#quick-start)
- [Run the App](#run-the-app)
- [Data Logging](#data-logging)
- [Calibration & Error Analysis](#calibration--error-analysis)
- [Velocity from Distance–Time](#velocity-from-distance–time)
- [Experiments](#experiments)
- [Results](#results)
- [Repo Structure](#repo-structure)
- [Team & Attribution](#team--attribution)
- [License](#license)

---

## Features
- **Live acquisition & plotting** of distance–time from **HC-SR04** via **MATLAB App Designer**
- **Start/Stop/Reload** controls; configurable **COM port** and **Trig/Echo** pins
- **Calibration** using **linear & quadratic fits** to reduce bias
- **Error metrics**: true, relative, and approximate error; **Good-data** LED/GUI flag
- **Velocity estimation** via **finite-difference** methods (forward & central)
- **Data logging** to CSV + one-click figure export (PNG) for reports

---

## System Overview

**Pipeline:** `HC-SR04 → Arduino (echo timing) → Serial → MATLAB (App Designer GUI) → Calibration/Error/Velocity → Plots + CSV`

<p align="center">
  <img src="docs/img/system_block_diagram.png" alt="System Block Diagram" width="780"/>
</p>

---

## Bill of Materials
- Arduino Uno (or compatible)
- HC-SR04 ultrasonic distance sensor
- Breadboard, jumper wires
- LED + series resistor (for “good-data” indicator)
- USB cable

---

## Wiring

| HC-SR04 Pin | Arduino Pin | Notes                  |
|-------------|-------------|------------------------|
| VCC         | 5V          | Sensor power           |
| GND         | GND         | Common ground          |
| TRIG        | **D7**      | Configurable in GUI    |
| ECHO        | **D6**      | Configurable in GUI    |

> You can change pins in the App settings before connecting.

---

## Quick Start

### Requirements
- **MATLAB R2023b+** with:
  - *MATLAB Support Package for Arduino Hardware*
  - *Ultrasonic Library*
- **Arduino IDE** (optional, for initial board test)

### Minimal MATLAB Snippet
```matlab
% App/Script snippet
a = arduino("COM7","Uno","Libraries","Ultrasonic");  % set your COM port
us = ultrasonic(a, "D7", "D6");                      % trig, echo
d = readDistance(us);                                % meters
