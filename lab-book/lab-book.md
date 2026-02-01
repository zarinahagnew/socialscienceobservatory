# Lab Book: Auditory Alpha Bridge

**Hardware:** Neurosity Crown

---

## Entry 2: Sunday, Jan 25, 2026
### **Objective**
Establishing a stable real-time data bridge and signal localization.

### **Activity**
* **Systematic Debugging:** Troubleshot the `brainwaves_power_by_band` subscription method.
* **Callback Refinement:** Refined the callback function to target specific electrodes rather than a global average.

### **Findings**
* **Syntax Resolution:** Determined that the specific SDK version on the local machine required a positional string for the band ("alpha") and a specific callback reference.
* **Localization:** Refined the data stream to monitor **PO3** and **PO4** (Parietal-Occipital). These sensors sit directly over the visual cortex, making them the most sensitive to the **"Alpha Block"** phenomenon (where Alpha waves surge the moment visual processing ceases).



### **Technical Success**
* **Closed-Loop Achieved:** Successfully triggered a system beep (`\a`) via Python when $PO3/PO4$ average power exceeded $15.0\text{ }\mu\text{V}^2$.
* **LED Telemetry:** Confirmed "Solid White" status as the operational "Ready" state for this firmware version.

---

## Day 1: Sunday, Jan 18, 2026
### **Objective**
Baseline characterization + initial environment setup.

### **Activity**
* **Neural Signature:** Conducted initial recording to establish a signature for the Alpha band ($8\text{--}12\text{ Hz}$).
* **Data Analysis:** Analyzed raw CSV data to differentiate between "Eyes Open" (Baseline) and "Eyes Closed" (Target State) power levels.

### **Findings**
* **Baseline Power:** $\approx 3.0\text{ }\mu\text{V}^2$.
* **Peak Alpha Power:** Identified a significant surge at $10\text{ Hz}$ reaching $\approx 441.0\text{ }\mu\text{V}^2$ during eyes-closed trials.
* **Threshold Selection:** Established a conservative trigger threshold of $15.0\text{ }\mu\text{V}^2$ to minimize false positives from muscle artifacts.

### **Technical Blockers**
* **Authentication:** Encountered errors and Python 3.9.6 deprecation warnings from Google-auth libraries.
* **SDK Logic:** Resolved login syntax by transitioning from positional arguments to dictionary-based authentication.

---

## Summary of Current State
* **The "Bridge" is functional:** Python $\leftrightarrow$ Neurosity Cloud $\leftrightarrow$ Crown Hardware.
* **Signal Quality:** High. The $10\text{ Hz}$ signature is robust and easily distinguishable from background noise.
* **End Goal:** Transition from binary auditory feedback (beep) to continuous **sonification** (modulated audio tracks) to study the effects of real-time biofeedback on sustained Alpha states.
