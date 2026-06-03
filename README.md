# HAPLab Metabolic Analyzer

**A web-based data reduction and reporting tool for exercise physiology testing.**

Built for the Parvo TrueOne 2400 metabolic cart, the HAPLab Metabolic Analyzer integrates metabolic cart data with blood lactate measurements to streamline physiologist-determined threshold identification, training zone calculation, and longitudinal performance comparison. Runs entirely in the browser with no installation required.

---

## 🌐 Live Tool

Access the tool directly at:
**[bryantbyrd.github.io/HAPLab-Metabolic-Analyzer](https://bryantbyrd.github.io/HAPLab-Metabolic-Analyzer)**

No login, no download, no setup. Open and use.

---

## Features

### Data Import
- Drag-and-drop or click-to-upload CSV files exported directly from the Parvo TrueOne 2400 metabolic cart software
- Automatic column detection and format validation
- Editable patient/subject information fields

### Interactive Metabolic Charts
- VO₂, VCO₂, RER, heart rate, and ventilation plotted across exercise stages
- The physiologist visually inspects the data and manually places threshold markers (blue line for VT1, red line for VT2) by dragging them to the appropriate position
- All downstream calculations (threshold summary, training zones, substrate tables) update in real time as the lines are moved

### Lactate Analysis
- Manual entry of blood lactate values collected at each exercise stage
- Polynomial regression curve fitting with R² display
- Dmax and modified Dmax curves are plotted to assist the physiologist in identifying LT1 and LT2
- Overlay of VT1/VT2 and LT1/LT2 markers on lactate curves (toggleable)

### Threshold Summary
- Full metabolic profile at VT1 and VT2: VO₂, heart rate, speed/power, RER, VE, and more
- Side-by-side VT vs. LT comparison table

### Training Zones
- Five-zone model derived from VT1, VT2, and peak heart rate
- CHO and FAT oxidation rates averaged within each zone from metabolic cart data

### Substrate Utilization
- Stage-by-stage carbohydrate and fat oxidation table

### Longitudinal Comparison
- Load a second test session alongside the primary session
- Side-by-side comparison of all key metrics
- Green/red highlighting for improvement or decline relative to the comparison session

### Session Management
- Save the full session state (data + thresholds + lactate values) as a `.json` file
- Reload any saved session at any time to continue or revisit analysis

---

## How to Use

1. **Export** your test data as a CSV from the Parvo TrueOne 2400 software
2. **Open** the tool at the link above
3. **Upload** the CSV file using the drag-and-drop zone
4. **Fill in** patient/subject information
5. **Identify** VT1 and VT2 by inspecting the charts and dragging the threshold lines to the appropriate positions
6. **Enter** blood lactate values if available
7. **Review** the threshold summary, training zones, and substrate tables
8. **Save** the session as a `.json` file to revisit later, or load a second session for longitudinal comparison

---

## Data Privacy

All data processing happens **entirely in your browser**. No data is uploaded to any server. Files never leave your computer.

---

## Compatibility

| Browser | Supported |
|---|---|
| Chrome / Edge | ✅ Recommended |
| Firefox | ✅ |
| Safari | ✅ |

No internet connection is required after the page loads. The tool can be saved and run as a local file.

---

## For Developers

The entire application is a single self-contained `index.html` file with no frameworks, no build step, and no dependencies. To run locally:

```bash
git clone https://github.com/bryantbyrd/HAPLab-Metabolic-Analyzer.git
cd HAPLab-Metabolic-Analyzer
open index.html   # or double-click the file in Explorer
```

---

## Citation

A permanent DOI and formal citation are coming soon via [Zenodo](https://zenodo.org). This page will be updated once the archive is live.

In the meantime, a `CITATION.cff` file is included in this repository. GitHub displays it automatically as a **"Cite this repository"** button on the repo page, making it easy for others to copy a formatted reference.

---

## Contact

**Bryant Byrd**
Western Colorado University, High Altitude Performance Lab
GitHub: [@bryantbyrd](https://github.com/bryantbyrd)
