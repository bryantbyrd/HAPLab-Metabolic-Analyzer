# HAPLab Metabolic Analyzer

**Version 2.0.0** · released 2026-11-26

**A free, open-source web application for analyzing metabolic cart data in exercise physiology research.**

Built for researchers and clinicians working with the **Parvo TrueOne 2400** and compatible metabolic carts. Includes **Rodent Mode** for the **Columbus Instruments Oxymax** system.

> No installation. No server. No data leaves your browser. Open `index.html` and go.

> **Research and teaching tool — not a medical device.** Results depend on test quality and on the choices the user makes. They are not a diagnosis and must not be used as one.

## Live Demo

**[Open HAPLab Metabolic Analyzer](https://bryantbyrd.github.io/HAPLab-Metabolic-Analyzer/)**

No installation required — runs entirely in your browser. To try it without your own data, use the synthetic recordings in [`examples/`](examples/README.md).

---

## What's new in 2.0.0

- **Runs fully offline.** Chart.js and xlsx-js-style are included in the `vendor/` folder; the page makes no request to any other host.
- **Lactate thresholds follow *lactater* 1.0.0** (Log-log, OBLA, Bsln+, Dmax, ModDmax, Exp-Dmax, Log-Poly-ModDmax, Log-Exp-ModDmax, LTP1 / LTP2, LTratio), checked against the R package's own results. Lactate thresholds can differ from those of version 1.0.
- **Metabolic Response Map** — blood lactate, carbohydrate oxidation and fat oxidation on the same exercise stages, each on its own axis, with intensity-zone shading and optional reference lines.
- **Fat oxidation and metabolic flexibility** — Fatmax, crossover points and related markers.
- **Heart-rate quality checks** — dropouts and artefacts are flagged; unusable stages are reported as such instead of being averaged.
- **Excel export** of a multi-sheet workbook, **Moxy** muscle-oxygenation import, and an **AOD / MAOD calculator**.
- **Synthetic example recordings** in `examples/`.

See [`CHANGELOG.md`](CHANGELOG.md).

---

## Features

### File Support
- **Parvo TrueOne 2400** — raw breath-by-breath CSV export (auto-detected)
- **Pre-cleaned CSV** — formatted exports with inline lactate (`La`) column, stage labels, speed/grade columns
- **Columbus Instruments Oxymax** — rodent metabolic cart CSV (auto-detected, switches to Rodent Mode)
- **Moxy** muscle-oxygenation CSV (SmO₂ / THb), added to a loaded test
- Auto-detects format on upload; manual override available

### Metabolic Charts (Human Mode)
- V-slope (VCO₂ vs VO₂)
- RER vs Time
- VE, VE/VO₂, VE/VCO₂ vs Time
- FECO₂ and FEO₂ vs Time
- FAT and CHO Oxidation vs Time
- SmO₂ vs Time (with a Moxy file)
- Time or workload on the x-axis, zoom, and every chart expandable to a full-screen view with PNG export

### Ventilatory Threshold Identification (VT1/VT2)
- Draggable VT1 and VT2 threshold lines synced across all charts simultaneously
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
- Per-stage steady-state averages for HR, VO₂/kg, RER, CHO, FAT, %CHO, %FAT
- Adjustable steady-state averaging window per stage
- Training zone badge per stage
- Customizable column visibility

### Fat Oxidation & Metabolic Flexibility
- **Metabolic Response Map** — lactate (mmol/L), CHO oxidation (g/min) and fat oxidation (g/min) per stage on three independent axes; zone shading from the lactate thresholds, the ventilatory thresholds or the training-zone table
- Fatmax from a fitted curve, with the fitted curve available as an overlay
- Energy crossover and fat/CHO crossover
- Stage inspection: every value with its kind (measured, calculated, fitted, interpolated) and source

### Calculation Details & Data Cleaning
- Per-stage, per-column outlier management: Exclude / Impute / Manual entry
- Full audit trail of all modifications
- Heart-rate quality flags for dropouts and artefacts
- Stage window highlighted in the data table showing exactly which rows were included

### Stage Builder (Raw Data Viewer)
- View the full parsed dataset in a scrollable modal after upload
- **Define stages by clicking** — click a row to mark stage Start, click again (or another row) to mark End
- Auto-detects lactate from inline `La` column or from the Parvo Events section
- Auto-detects speed and grade from inline columns or Events section speed entries
- Pre-fills the stage table with start, end, workload, grade, and lactate automatically

### Lactate Analysis
- Per-stage lactate entry and curve fitting
- Lactate-threshold methods of the R package *lactater* 1.0.0: Log-log, OBLA, Bsln+, Dmax, ModDmax, Exp-Dmax, Log-Poly-ModDmax, Log-Exp-ModDmax, LTP1 / LTP2, LTratio
- LT1 and LT2 are chosen from those methods; every method's value is listed in a methods table
- A method that cannot be determined from the data is reported as such, with the reason

### Training Zones
- Zone tables from the ventilatory or the lactate thresholds, with selectable zone models

### Longitudinal Comparison Mode
- Load a second session for side-by-side or overlaid comparison
- **Substrate Utilization comparison sub-rows**: each stage shows primary row + comparison sub-row + absolute and % difference
- **Longitudinal Comparison Summary table**: all key metrics side by side with color-coded change column
- Toggle: show Absolute difference / % Change / Both
- Comparison thresholds can be shown on the primary session's charts
- Customizable row visibility for the Comparison Summary

### Session Management and Export
- Save session as JSON (includes all data, thresholds, stage definitions, outlier edits, peak overrides, audit trail)
- Load session from JSON — full restore including comparison sessions
- Unsaved changes indicator
- Excel workbook export (results, thresholds, lactate methods, stage calculations, full data), chart PNG export and figure captions

### AOD / MAOD Calculator
- Accumulated oxygen deficit from a sub-maximal calibration regression

---

## Rodent Mode (Columbus Instruments Oxymax)

Upload an Oxymax CSV file and the app automatically switches to Rodent Mode.

### Auto-Detected From File Header
- Subject ID, body mass (grams), experiment date
- Elapsed time computed from absolute timestamps
- VO₂ and VCO₂ converted from ml/hr to mL/kg/min using parsed body mass

### Rodent-Specific Charts
- RER, VO₂/kg, VO₂ and VCO₂ vs Time
- **VO₂/kg vs Speed** (primary rodent GXT view)
- CHO and FAT Oxidation vs Speed and vs Time
- **CHO/FAT Crossover chart** with Speed/Time toggle and a draggable marker
- **V-slope (VCO₂ vs VO₂)**
- **Excess CO₂ vs Time** — ExCO₂ = VCO₂ − VO₂

### Substrate Estimation
- CHO and FAT oxidation estimated via Frayn (1983) equations from VO₂ and VCO₂ when not directly measured
- All estimated values marked with † throughout charts and tables

### AT1/AT2 Threshold System
- Two draggable threshold lines (AT1 = moderate→heavy domain; AT2 = heavy→severe domain)
- Time is the single source of truth — dragging on any chart updates all charts
- Speed units toggle: m/min ↔ km/h

### Auto-Stage Generation
- Stages automatically generated from the treadmill speed column on upload

### HR/VE Features
- HR and VE charts, columns, and training zones hidden in Rodent Mode (not available from a chamber-based system)

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

1. Open the live demo, or open `index.html` from a downloaded copy
2. Drag and drop your CSV file onto the upload zone, or click to browse
3. The app auto-detects your file format and switches modes if needed
4. Confirm the proposed stages and enter lactate values (or use Stage Builder)
5. Drag VT1/VT2 (or AT1/AT2 in Rodent Mode) lines on any chart to set thresholds
6. Save your session as JSON to preserve all edits and reload later

### Running it offline

Download the release zip (or this repository), unzip it, and open `index.html`. No internet connection is needed. Keep these together in one folder:

```
index.html                  the app (HAPLAB.html is the same file under its earlier name)
vendor/                     Chart.js and xlsx-js-style (required)
examples/                   synthetic example recordings (optional)
THIRD-PARTY-NOTICES.md      licences of the included software
```

If `index.html` is moved without the `vendor` folder the app shows a message saying so and does not start. To put the app on another computer or a USB stick, copy the whole folder.

---

## Supported Metabolic Cart Formats

| Cart | Format | Auto-detected |
|------|--------|--------------|
| Parvo TrueOne 2400 | Raw breath-by-breath CSV | ✓ |
| Pre-cleaned CSV (with Stage/La columns) | Formatted CSV | ✓ |
| Columbus Instruments Oxymax | Oxymax CSV v1.x | ✓ (Rodent Mode) |

---

## Limitations

- Built for desktop browsers. The automated tests run in Chromium (Chrome / Edge); other browsers are not covered by them.
- Input formats are those listed above. Other carts' exports are not supported.
- Thresholds, Fatmax and crossover points are estimates from a single test. Different methods give different values; the app reports them separately and does not treat them as interchangeable.
- Substrate oxidation assumes a steady state and RER between 0.70 and 1.00; stages outside that range are flagged.
- The AOD / MAOD calculator and Rodent Mode are not yet covered by the automated tests of this release.
- There is no user account, cloud storage or multi-user database: a session is a file you keep.

## Privacy

Recordings from metabolic carts usually contain a name, age, height and body mass. The app never transmits them, but **session files and Excel exports contain them**, so treat those files as you treat the original recordings. The example files in this repository are synthetic.

---

## Technical Notes

- One HTML file plus two JavaScript libraries in `vendor/` — no build step, nothing to install
- [Chart.js](https://www.chartjs.org) 4.4.0 (MIT License) for all visualizations
- [xlsx-js-style](https://github.com/gitbrent/xlsx-js-style) 1.2.0 (Apache License 2.0) for Excel import and export
- Lactate-threshold methods adapted from [lactater](https://github.com/fmmattioni/lactater) 1.0.0 by Felipe Mattioni Maturana (MIT License)
- All computation runs locally in the browser — no data is transmitted
- Session files are JSON and human-readable
- Full notices: [`THIRD-PARTY-NOTICES.md`](THIRD-PARTY-NOTICES.md)

---

## References

- Achten, J., Gleeson, M., & Jeukendrup, A.E. (2002). Determination of the exercise intensity that elicits maximal fat oxidation. *Medicine & Science in Sports & Exercise*, 34(1), 92–97.
- Beaver, W.L., Wasserman, K., & Whipp, B.J. (1985). Improved detection of lactate threshold during exercise using a log-log transformation. *Journal of Applied Physiology*, 59(6), 1936–1940.
- Beaver, W.L., Wasserman, K., & Whipp, B.J. (1986). A new method for detecting anaerobic threshold by gas exchange. *Journal of Applied Physiology*, 60(6), 2020–2027.
- Bishop, D., Jenkins, D.G., & Mackinnon, L.T. (1998). The relationship between plasma lactate parameters, Wpeak and 1-h cycling performance in women. *Medicine & Science in Sports & Exercise*, 30(8), 1270–1275.
- Cheng, B., et al. (1992). A new approach for the determination of ventilatory and lactate thresholds. *International Journal of Sports Medicine*, 13(7), 518–522.
- Frayn, K.N. (1983). Calculation of substrate oxidation rates in vivo from gaseous exchange. *Journal of Applied Physiology*, 55(2), 628–634.
- Mattioni Maturana, F. *lactater: Tools for Analyzing Lactate Thresholds* (R package, version 1.0.0). https://github.com/fmmattioni/lactater

---

## License

MIT License — free to use, modify, and distribute. See [`LICENSE`](LICENSE). The included third-party software keeps its own licences.

---

## Citation

If you use HAPLab Metabolic Analyzer in published research, please cite:

> Byrd, B. (2026). *HAPLab Metabolic Analyzer* (Version 2.0.0) [Computer software]. https://doi.org/10.5281/zenodo.20533547

*The DOI above always points to the latest version. Please state the version you used for reproducibility.*

---

## Contact

Bryant Byrd, PhD Candidate  
Exercise Physiology, HAPLab  
Western Colorado University
