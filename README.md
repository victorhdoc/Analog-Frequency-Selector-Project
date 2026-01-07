# Analog Frequency Selector Project ⚡

**A purely analog control system developed for the Electronics Engineering course (Analog Electronics II) at UTFPR.**

## 📖 Overview

This project implements an autonomous signal processing system capable of making decisions based on the input frequency without using any microcontroller or digital code. The system relies entirely on the physics of semiconductors (transistors, diodes, and op-amps) to switch output channels.

### The Challenge
Design a circuit that monitors an input signal and behaves according to the following logic:

| Input Frequency ($f_{in}$) | System Behavior | Output Signal |
| :--- | :--- | :--- |
| **$f_{in} < 20 \text{ kHz}$** | Pass-Through Mode | Amplified & Filtered Input |
| **$f_{in} > 20 \text{ kHz}$** | Signal Injection Mode | Internally Generated 1 kHz Sine Wave |

---

## ⚙️ Circuit Topology & Architecture

The system is composed of four main analog blocks working in harmony.

### 1. Pre-Amplifier (Input Stage)
* **Topology:** Common Emitter with **Darlington Configuration** (using 2N5551 transistors).
* **Purpose:** To achieve high input impedance and amplify the weak input signal (150mV) to approximately 2V.
* **Key Feature:** The Darlington pair was implemented to compensate for component variations and maximize $h_{fe}$ (current gain).

### 2. Sallen-Key Filter (Conditioning)
* **Topology:** 2nd Order Low-Pass Filter.
* **Cutoff Frequency:** Designed for ~23.4 kHz.
* **Purpose:** To clean the amplified signal and attenuate high-frequency noise before the output stage.

### 3. Wien Bridge Oscillator (Signal Generation)
* **Frequency:** Fixed at ~1 kHz.
* **Purpose:** To provide a stable fallback signal when the input exceeds the frequency threshold.
* **Stability:** Stabilized using diode feedback to prevent saturation.

### 4. The Analog Decision Core (Selector)
This is the "brain" of the circuit. It works in three steps:
1.  **Sensing:** A parallel Sallen-Key filter reads the pre-amp output.
2.  **Rectification:** Diodes convert the AC signal into a DC voltage level proportional to the frequency.
3.  **Logic Switching:** A **Schmitt Trigger** (Comparator with hysteresis) detects if the DC level crosses the threshold. It drives a network of BJTs (Q1, Q2, Q3) that act as **Analog Gates**, physically blocking one path and opening the other.

---

## 📉 Results & Validation

The circuit was validated using an oscilloscope to verify the switching threshold.

### Case A: Input within range (15 kHz)
![entrada 15khz](https://github.com/user-attachments/assets/ed91f9b1-046e-4793-b79a-b13e85512758)

> **Observation:** The system allows the signal to pass. The output (Yellow) follows the input (Blue).

### Case B: Input above threshold (20 kHz)
![entrada 20khz](https://github.com/user-attachments/assets/1d2aac9a-337c-4298-91eb-30d9fe3d0660)

> **Observation:** The protection logic triggers. The input signal is blocked, and the circuit instantly switches the output to the local 1 kHz oscillator.

---

## 🛠️ Materials & Tools
* **Simulation:** Proteus ISIS / LTSpice
* **Op-Amps:** TL082
* **Transistors:** 2N5551 (NPN)
* **Diodes:** 1N4148
* **Passive Components:** Resistors and Capacitors (See BOM in docs)

## 👥 Authors & Credits
Project developed by the engineering team:
* **Victor Hugo Carvalho**
* Lucas Erlo Dambros
* Lucas O. Dahmer
* Sérgio Henrique M. dos Santos

**Instructor:** Alberto Vinicius de Oliveira (UTFPR - Toledo)

---

## 📂 Repository Structure
* `/docs`: Contains the full project report (PDF).
* `/schematics`: (Coming Soon) High-resolution circuit diagrams.
* `/simulation`: (Coming Soon) Simulation files.# Analog-Frequency-Selector-Project
