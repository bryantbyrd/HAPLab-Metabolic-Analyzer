# Changelog

## 2.0.0 — 2026-11-26

* Runs fully offline: Chart.js 4.4.0 and xlsx-js-style 1.2.0 are included in `vendor/`; the page makes
  no request to any other host.
* Lactate-threshold methods now follow *lactater* 1.0.0 and are checked against the R package.
  Lactate thresholds can differ from those of version 1.0.
* New: Metabolic Response Map (blood lactate, carbohydrate oxidation and fat oxidation on one chart).
* New: fat oxidation and metabolic-flexibility analysis (Fatmax, crossover points).
* New: heart-rate quality checks for dropouts and artefacts.
* New: Excel workbook export, Moxy muscle-oxygenation import, AOD / MAOD calculator.
* New: synthetic example recordings in `examples/`.
* The file-format guide and the built-in sample file no longer show a real person's details.

## 1.0 — 2026-06-03

First public release.
