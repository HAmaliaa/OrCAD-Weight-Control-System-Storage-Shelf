# Weight Control System for Storage Shelf - OrCAD Design

This repository contains the OrCAD schematic design, simulations, and documentation for an analog hardware system that monitors and controls the weight supported by a storage shelf using a resistive weight sensor.

##  Project Overview
The system monitors a resistive weight sensor to ensure that the shelf load stays within a specified safe operating range. It utilizes an analog window comparator topology to detect underload, normal, and overload conditions, signaling the status via specific LED indicators.

### Design Specifications & Parameters
Based on the project assignment requirements, the circuit is designed using the following parameters:

| Parameter | Value | Description |
| :--- | :--- | :--- |
| **Measurable Weight Range** | 7 ... 250 kg | Full sensor range ($W_{min} \dots W_{max}$) |
| **Allowed Weight Interval** | 40 ... 200 kg | Safe operating limits ($W_L \dots W_H$) |
| **Sensor Resistance Range** | 1 - 21 kΩ | Linear resistance variation ($R_{min} \dots R_{max}$) |
| **Supply Voltage ($V_{cc}$)** | 10 V | System power supply rail |
| **Underload LED** | Red | Active when weight < 2 kg |
| **Normal Condition LED** | Orange | Active when weight is between 2 kg and 50 kg |
| **Overload LED** | Yellow | Active when weight > 50 kg |

---

##  Functional Architecture

### 1. Resistance-to-Voltage Conversion
The resistive sensor's linear resistance changes proportionally to the weight ($R = f(W)$). A fixed-resistor voltage divider is designed to map the raw sensor resistance into a usable analog voltage range:
$$V_{sensor} \in [0V, V_{cc} - 2V] \implies [0V, 8V]$$
*   $R_{min} \implies 0\text{ V}$
*   $R_{max} \implies 8\text{ V}$

### 2. Comparator Stage (Window Detection)
Two independent analog comparators establish the threshold limits ($V_L$ and $V_H$) corresponding to the safe weight bounds ($W_L$ and $W_H$):
*   **Lower Threshold Comparator ($W_L$):** Detects underload conditions.
*   **Upper Threshold Comparator ($W_H$):** Detects overload conditions.

### 3. LED Signaling Stage
Driven by the comparator logic outputs, three current-limited branches control the LEDs to indicate real-time status:
*   **Underload:** Red LED ON
*   **Normal:** Orange LED ON
*   **Overload:** Yellow LED ON

---

##  Repository Structure
*   `/orcad-project/` - Contains the OrCAD Capture schematic (`.DSN`) and design files.
*   `/simulation/` - PSpice simulation profiles and transient/DC sweep results.
*   `/docs/` - Contains mathematical threshold calculations, component selection rationale, and the final technical report.

---

##  Testing & Validation
The design successfully satisfies all performance criteria:
*   [x] Linear voltage mapping across the full sensor range without op-amp saturation.
*   [x] Accurate threshold switching exactly at the boundary weight limits.
*   [x] Stable LED signaling with no flickering or unwanted oscillations near transition points.
