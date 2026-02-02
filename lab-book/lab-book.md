# Lab Book: Auditory Alpha Bridge

**Hardware:** Neurosity Crown

## Day 3: Sunday, Feb 1st, 2026
### **Objective**
Develop + validate an automated threshold characterization protocol to establish baseline and peak alpha power values for individual calibration of the neurofeedback system.

### **Protocol Design:**

4 alternating cycles (eyes open → eyes closed → eyes open → eyes closed)
20 seconds per condition (80 seconds total)
Voice-guided prompts using macOS text-to-speech for autonomous operation
Automatic analysis calculating baseline, peak, threshold (2.5x baseline), and contrast ratio

Neurosity Crown (Device IDs: 353 and 63F)
Custom Python script with CSV logging
Sampling: 256 Hz, 8 channels (CP3, C3, F5, PO3, PO4, F6, C4, CP4)

Target Measurement:
Parieto-occipital channels (PO3, PO4 - indices 3 & 4)
Alpha band (8-12 Hz) power extraction via SDK

### **Background:**
Previous session successfully established basic alpha reactivity detection (eyes open → eyes closed with auditory beep). However, each session required manual calibration, and we lacked quantitative baseline/threshold data. We needed a standardized protocol to:

Collect reliable baseline alpha values (eyes open)
Measure peak alpha values (eyes closed)
Calculate optimal detection thresholds
Assess signal consistency (standard deviation)

Test 1 - Crown 353:

Eyes Open (baseline): 3.9 ± 2.1
Eyes Closed (peak): 4.5 ± 1.9
Contrast ratio: 1.2x ⚠️
Status: Poor signal quality

Test 2 - Crown 63F (Initial):

Eyes Open (baseline): 3.1 ± 1.9
Eyes Closed (peak): 3.7 ± 1.9
Contrast ratio: 1.2x ⚠️
Status: Poor signal quality

Troubleshooting.. Added all-channel monitoring to identify source of alpha activity. During eyes-closed periods, observed:

F5 (index 2): 58.3-97.7 (frontal left)
F6 (index 5): 55.8-85.7 (frontal right)
PO3 (index 3): 1.2-8.3 (parietal-occipital left)
PO4 (index 4): 2.3-6.5 (parietal-occipital right)

Expected vs. Observed:

Expected: Strong alpha in PO3/PO4 (occipital visual cortex)
Observed: Strong alpha in F5/F6 (frontal regions)
Contrast: Frontal channels showed ~20-30x increase; occipital channels showed only ~2-3x increase


probably due to bad positioning / parieto-occipital electrodes (PO3/PO4) not making proper contact with target region over visual cortex.
Not using frontal elotrodes, as frontal alpha might just be mu rhythm (motor cortex, 8-13 Hz) / may include facial muscle artifacts / does not reflect genuine occipital alpha from visual cortex idle state

### **Key Learnings:

Protocol works well: Voice guidance, timing, and automatic analysis all functioned correctly
Electrode placement critical: Even with good SDK/software, poor hardware positioning invalidates measurements
All-channel diagnostics essential: Without viewing all channels, we would have assumed the measurement was simply "weak" rather than identifying it as a positioning error
Scientific integrity: Measuring the correct neural source is more important than measuring the strongest signal

### **amused that my voice has a London accent :) 




---

## Day 2: Sunday, Jan 25, 2026
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
