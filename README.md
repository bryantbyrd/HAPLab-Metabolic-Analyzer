# HAPLab Metabolic Analyzer

**A free, open-source, single-file web application for analyzing metabolic cart data in exercise physiology research.**

Built for researchers and clinicians working with the **Parvo TrueOne 2400** and compatible metabolic carts. Now includes **Rodent Mode** for the **Columbus Instruments Oxymax** system.

> No installation. No server. No data leaves your browser. Open `index.html` and go.

> ## Live Demo

**[Open HAPLab Metabolic Analyzer](https://bryantbyrd.github.io/HAPLab-Metabolic-Analyzer/)**

No installation required — runs entirely in your browser.

---

## Features

### File Support
- **Parvo TrueOne 2400** — raw breath-by-breath CSV export (auto-detected)
- **Pre-cleaned CSV** — formatted exports with inline lactate (`La`) column, stage labels, speed/grade columns
- **Columbus Instruments Oxymax** — rodent metabolic cart CSV (auto-detected, switches to Rodent Mode)
- Auto-detects format on upload; manual override available

### Metabolic Charts (Human Mode)
- VO₂/kg vs Time
- RER vs Time
- VE, VE/VO₂, VE/VCO₂ vs Time
- PetO₂, PetCO₂ vs Time
- CHO and FAT Oxidation vs Time
- %CHO and %FAT vs Time
- VO₂/kg vs HR (V-slope for human data)
- All charts expandable to full-screen modal

### Ventilatory Threshold Identification (VT1/VT2)
- Draggable VT1 (blue) and VT2 (red) threshold lines synced across all charts simultaneously
- Linear interpolation or nearest measured value toggle
- Full calculation transparency — click any threshold value to see which data points were used and the exact formula
- Submaximal test mode with user-entered known VO₂max and HRmax for percentage calculations

### Threshold Summary Table
- VT1 and VT2: Time, HR, VO₂/kg, % VO₂max, % HRmax, RER, Lactate
- Peak row with test/known max values displayed side by side
- Transparency indicators (≈ interpolated, = nearest) on every cell — clickable for full derivation detail

### Results Summary Panel
- Clean single-session metric table: Peak values, VT1/VT2 metrics, Training Zones
- Customizable row visibility (show/hide any metric)
- Peak value overrides: manually replace Peak VO₂/kg, Peak HR, Peak RER, Peak VE with known values — cascade automatically into all percentage calculations
- Same transparency indicators and click-to-explain popups as Threshold Summary

### Substrate Utilization Table
- Per-stage averages for HR, VO₂/kg, RER, CHO (g/hr), FAT (g/hr), %CHO, %FAT, VE/VO₂, VE/VCO₂
- Averaging method toggle: All breaths / Final 3 min / Final 2 min / Final 60 s / Final 30 s / Nearest value
- Training zone badge per stage (Z1–Z5) based on HR
- Customizable column visibility

### Calculation Details & Data Cleaning
- Per-stage, per-column outlier management: Exclude / Impute / Manual entry
- Full audit trail of all modifications
- Snap-to-point boundary dragging for stage windows
- Column-specific outlier exclusion with visual highlighting in the raw data viewer
- Stage window highlighted in the data table showing exactly which rows were included

### Stage Builder (Raw Data Viewer)
- View the full parsed dataset in a scrollable modal after upload
- **Define stages by clicking** — click a row to mark stage Start, click again (or another row) to mark End
- Auto-detects lactate from inline `La` column or from the Parvo Events section (`x.xx mmol` format)
- Auto-detects speed and grade from inline columns or Events section speed entries
- Pre-fills stage table with tStart, tEnd, workload, grade, and lactate automatically
- Previously defined stages shown with persistent color-coded highlights and stage labels (S1, S2, …) so you always know where the last stage ended
- Single-row stage support (click start row twice)
- Warning when entered tEnd extends beyond the last actual data point in the stage

### Lactate Analysis
- Per-stage lactate entry with polynomial (2nd/3rd degree) regression
- LT1 (Traditional Dmax), LT2 (Modified Dmax) auto-detection with draggable lines
- LT1/LT2 lines default to off on load; toggle on when needed
- Lactate threshold transparency: same click-to-explain popups as ventilatory thresholds
- Polynomial interpolation or nearest measured value toggle for lactate at threshold

### Longitudinal Comparison Mode
- Load a second session JSON for side-by-side comparison
- **Substrate Utilization comparison sub-rows**: each stage shows primary row + comparison sub-row + absolute and % difference
- Stage matching by number with manual re-mapping option for mismatched protocols
- **Longitudinal Comparison Summary table**: all key metrics side by side with color-coded change column
- Toggle: show Absolute difference / % Change / Both
- Calculation detail popups on Change column values — shows primary value, comparison value, formula, and result
- Peak value location popups (ⓘ) on both sessions showing time, co-occurring HR, RER, VE at peak
- Prior threshold overlay: toggle to show comparison session's VT1/VT2 as ghost lines on primary session charts
- Customizable row visibility for the Comparison Summary

### Session Management
- Save session as JSON (includes all data, thresholds, stage definitions, outlier edits, peak overrides, audit trail)
- Load session from JSON — full restore including comparison sessions
- Unsaved changes indicator

---

## Rodent Mode (Columbus Instruments Oxymax)

Upload an Oxymax CSV file and the app automatically switches to Rodent Mode.

### Auto-Detected From File Header
- Subject ID, body mass (grams), experiment date
- Elapsed time computed from absolute timestamps (15-second intervals → fractional minutes)
- VO₂ and VCO₂ converted from ml/hr to mL/kg/min using parsed body mass

### Rodent-Specific Charts
- RER vs Time
- VO₂/kg vs Time
- **VO₂/kg vs Speed** (primary rodent GXT view)
- CHO Oxidation vs Speed and vs Time (g/hr)
- FAT Oxidation vs Speed and vs Time (g/hr)
- %CHO and %FAT vs Time
- **CHO/FAT Crossover chart** with Speed/Time toggle — auto-detects Fatmax crossover point with draggable marker
- VO₂ and VCO₂ vs Time (absolute mL/min)
- **V-slope (VCO₂ vs VO₂)** — primary non-ventilatory threshold detection chart
- **Excess CO₂ vs Time** — ExCO₂ = VCO₂ − VO₂; inflects upward at the metabolic threshold

### Substrate Estimation
- CHO and FAT oxidation estimated via Frayn (1983) equations from VO₂ and VCO₂ when not directly measured
- All estimated values marked with † footnote throughout charts and tables

### AT1/AT2 Threshold System
- Two draggable threshold lines (AT1 = moderate→heavy domain; AT2 = heavy→severe domain)
- Time is the single source of truth — dragging on any chart (speed, VO₂, time) updates all charts simultaneously using hidden time mapping
- All 13 rodent charts sync on drag; summary values update on release
- Speed units toggle: m/min ↔ km/h

### Auto-Stage Generation
- Stages automatically generated from TREADMILL SPEED column on upload
- Speed = 0 becomes Baseline/Rest stage
- Dismissible notice confirms auto-generation; review and adjust in stage table

### HR/VE Features
- HR and VE charts, columns, and training zones hidden in Rodent Mode (not available from chamber-based system)
- Missing-column warnings suppressed for expected absent fields

---

## Frayn Equation Fallback

When CHO/FAT columns are absent, the app estimates substrate oxidation using:

```
CHO (g/min) = 4.585 × VCO₂ − 3.226 × VO₂
FAT (g/min) = 1.695 × VO₂ − 1.701 × VCO₂
```

(VO₂ and VCO₂ in L/min; Frayn 1983)

All estimated values are clearly labeled with a † indicator throughout the interface.

---

## Calculation Transparency

Every computed value in the app — threshold metrics, stage averages, substrate oxidation rates, percentage calculations — has a clickable indicator revealing exactly how it was derived:

- `≈` — value was linearly interpolated between two data points (shows both points and formula)
- `○` — nearest measured value was used (shows which row)
- `ⓘ` — peak/lookup value (shows time of occurrence and co-occurring variables)
- `✎` — user-entered override

---

## Usage

1. Open `index.html` in any modern browser (Chrome, Edge, Firefox, Safari)
2. Drag and drop your CSV file onto the upload zone, or click to browse
3. The app auto-detects your file format and switches modes if needed
4. Enter subject information, stage times, and lactate values (or use Stage Builder)
5. Drag VT1/VT2 (or AT1/AT2 in Rodent Mode) lines on any chart to set thresholds
6. Save your session as JSON to preserve all edits and reload later

---

## Supported Metabolic Cart Formats

| Cart | Format | Auto-detected |
|------|--------|--------------|
| Parvo TrueOne 2400 | Raw breath-by-breath CSV | ✓ |
| Pre-cleaned CSV (with Stage/La columns) | Formatted CSV | ✓ |
| Columbus Instruments Oxymax | Oxymax CSV v1.x | ✓ (Rodent Mode) |

---

## Technical Notes

- Single HTML file — no build step, no dependencies to install
- Chart.js (CDN) for all visualizations
- All computation runs locally in the browser — no data is transmitted
- Session files are JSON and human-readable

---

## References

- Frayn, K.N. (1983). Calculation of substrate oxidation rates in vivo from gaseous exchange. *Journal of Applied Physiology*, 55(2), 628–634.
- Beaver, W.L., Wasserman, K., & Whipp, B.J. (1986). A new method for detecting anaerobic threshold by gas exchange. *Journal of Applied Physiology*, 60(6), 2020–2027.
- Cheng, B., et al. (1992). A new approach for the determination of ventilatory and lactate thresholds. *International Journal of Sports Medicine*, 13(7), 518–522.
- Bishop, D., et al. (1998). The validity of a repeated sprint ability test. *Journal of Science and Medicine in Sport*, 1(3), 133–148.

---

## License

MIT License — free to use, modify, and distribute.

---

## Citation

If you use HAPLab Metabolic Analyzer in published research, please cite:

> Byrd, B. (2025). *HAPLab Metabolic Analyzer* [Computer software]. https://github.com/bryantbyrd/HAPLab-Metabolic-Analyzer

*Note: If citing for a specific publication, please include the version or commit hash for reproducibility.*

---

## Contact

Bryant Byrd, PhD Candidate  
Exercise Physiology, HAPLab  
Western Colorado University
