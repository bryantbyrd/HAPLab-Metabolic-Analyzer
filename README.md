# HAPLab Metabolic Analyzer

**Version 2.0.1** · released 2026-11-26

**A free, open-source web application for analyzing human metabolic cart data in exercise physiology research.**

Built for researchers and clinicians who run graded exercise tests on people with the **Parvo TrueOne 2400** metabolic cart.

> No installation. No server. No data leaves your browser. Open `index.html` and go.

> **Research and teaching tool — not a medical device.** Results depend on test quality and on the choices the user makes. They are not a diagnosis and must not be used as one.

> **AOD/MAOD analysis is under development and is not currently available for use.** It is unavailable in this public application and must not be used for research or physiological assessment.

## Live Demo

**[Open HAPLab Metabolic Analyzer](https://bryantbyrd.github.io/HAPLab-Metabolic-Analyzer/)**

No installation required — runs entirely in your browser. To try it without your own data, use the synthetic recordings in [`examples/`](examples/README.md).

---

## Acknowledgement: lactater

The lactate-threshold analysis in HAPLab includes a **JavaScript adaptation of the R package [lactater](https://github.com/fmmattioni/lactater), version 1.0.0, by Felipe Mattioni Maturana**, used under the MIT License.

- Copyright (c) 2020 Felipe Mattioni Maturana. The MIT licence text and copyright notice are reproduced in [`THIRD-PARTY-NOTICES.md`](THIRD-PARTY-NOTICES.md) and at the head of the lactate code inside `index.html`.
- The adaptation follows the R source of lactater 1.0.0 and is checked against results produced by the R package itself. Places where HAPLab departs from the package are marked `HAPLAB:` in the code.
- **Adapted from lactater:** Log-log; OBLA (2.0, 2.5, 3.0, 3.5 and 4.0 mmol/L); Bsln+ (baseline + 0.5, 1.0 and 1.5 mmol/L); Dmax, ModDmax, Exp-Dmax, Log-Poly-ModDmax and Log-Exp-ModDmax; LTP1 and LTP2. Curve fits: 3rd- and 4th-degree polynomial, B-spline, and exponential.
- **Not included:** LTratio; the individual-anaerobic-threshold methods (IAT, Keul, Simon, Stegmann); LTP1-Poly-ModDmax; bootstrap confidence intervals; and lactater's zone, training-load, reliability, MLSS, VLamax, performance-prediction, percentile and reporting functions.
- Any error in the adaptation is HAPLab's and not the original author's. If you report lactate thresholds from this app, please cite lactater as well (see [References](#references)).

---

## What's new in version 2

- **Runs fully offline.** Chart.js and xlsx-js-style are included in the `vendor/` folder; the page makes no request to any other host.
- **Lactate thresholds follow *lactater* 1.0.0** (see the acknowledgement above). Lactate thresholds can differ from those of version 1.0.
- **Metabolic Response Map** — blood lactate, carbohydrate oxidation and fat oxidation on the same exercise stages, each on its own axis, with intensity-zone shading and optional reference lines.
- **Fat oxidation and metabolic flexibility** — Fatmax, crossover points and related markers.
- **Heart-rate quality checks** — dropouts and artefacts are flagged; unusable stages are reported as such instead of being averaged.
- **Excel export** of a multi-sheet workbook and **Moxy** muscle-oxygenation import.
- **Synthetic example recordings** in `examples/`.

Version 2.0.1 switches off the AOD/MAOD calculator that version 2.0.0 showed, because it is still being developed, and corrects this README (version 2.0.0 listed LTratio among the lactate methods; it is not implemented). See [`CHANGELOG.md`](CHANGELOG.md).

---

## Features

### File Support
- **Parvo TrueOne 2400** — raw breath-by-breath CSV export (auto-detected)
- **Pre-cleaned CSV** — formatted exports with inline lactate (`La`) column, stage labels, speed/grade columns
- **Moxy** muscle-oxygenation CSV (SmO₂ / THb), added to a loaded test
- Auto-detects format on upload; manual override available

### Metabolic Charts
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
- Per-stage lactate entry and curve fitting (3rd- or 4th-degree polynomial, B-spline, exponential)
- Lactate-threshold methods adapted from *lactater* 1.0.0: Log-log; OBLA 2.0–4.0 mmol/L; Bsln+ 0.5 / 1.0 / 1.5 mmol/L; Dmax, ModDmax, Exp-Dmax, Log-Poly-ModDmax, Log-Exp-ModDmax; LTP1 and LTP2
- LT1 and LT2 are chosen from those methods; every method's value is listed in a methods table
- A method that cannot be determined from the data is reported as such, with the reason
- LTratio and the IAT-family methods of lactater are not implemented

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

### AOD / MAOD Analysis
AOD/MAOD analysis is under development and is not currently available for use. It is unavailable in this public application and must not be used for research or physiological assessment.

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
3. The app auto-detects your file format
4. Confirm the proposed stages and enter lactate values (or use Stage Builder)
5. Drag the VT1/VT2 lines on any chart to set thresholds
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

---

## Limitations

- **AOD/MAOD analysis is under development and is not currently available for use.** It is unavailable in this public application and must not be used for research or physiological assessment.
- For human exercise tests. Built for desktop browsers; the automated tests run in Chromium (Chrome / Edge), and other browsers are not covered by them.
- Input formats are those listed above. Other carts' exports are not supported.
- Thresholds, Fatmax and crossover points are estimates from a single test. Different methods give different values; the app reports them separately and does not treat them as interchangeable.
- Not every lactater method is implemented (see the acknowledgement above).
- Substrate oxidation assumes a steady state and RER between 0.70 and 1.00; stages outside that range are flagged.
- There is no user account, cloud storage or multi-user database: a session is a file you keep.

## Privacy

Recordings from metabolic carts usually contain a name, age, height and body mass. The app never transmits them, but **session files and Excel exports contain them**, so treat those files as you treat the original recordings. The example files in this repository are synthetic.

---

## Technical Notes

- One HTML file plus two JavaScript libraries in `vendor/` — no build step, nothing to install
- [Chart.js](https://www.chartjs.org) 4.4.0 (MIT License) for all visualizations
- [xlsx-js-style](https://github.com/gitbrent/xlsx-js-style) 1.2.0 (Apache License 2.0) for Excel import and export
- Lactate-threshold methods: a JavaScript adaptation of [lactater](https://github.com/fmmattioni/lactater) 1.0.0 by Felipe Mattioni Maturana (MIT License)
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
- Mattioni Maturana, F. (2026). *lactater: Tools for Analyzing Lactate Thresholds* (R package, version 1.0.0). https://github.com/fmmattioni/lactater

---

## License

MIT License — free to use, modify, and distribute. See [`LICENSE`](LICENSE). The included third-party software keeps its own licences: Chart.js (MIT), xlsx-js-style (Apache License 2.0) and lactater (MIT, Copyright (c) 2020 Felipe Mattioni Maturana).

---

## Citation

If you use HAPLab Metabolic Analyzer in published research, please cite:

> Byrd, B. (2026). *HAPLab Metabolic Analyzer* (Version 2.0.1) [Computer software]. https://doi.org/10.5281/zenodo.20533547

*The DOI above always points to the latest version. Please state the version you used for reproducibility.*

---

## Contact

Bryant Byrd, PhD Candidate  
Exercise Physiology, HAPLab  
Western Colorado University
