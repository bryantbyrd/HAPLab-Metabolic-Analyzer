# Changelog

## 2.0.2 (2026-11-26)

* The documentation, interface labels, help sections and instructional text have been refined for
  clarity and consistency.
* No analytical calculations or functionality have changed.

## 2.0.1 (2026-11-26)

* The AOD / MAOD calculator is switched off. AOD/MAOD analysis is under development and is not
  currently available for use; it must not be used for research, physiological assessment or
  exercise prescription. Its navigation button is gone and the calculator cannot be opened.
* This public version analyses human exercise tests only. Rodent Mode (Columbus Instruments Oxymax),
  which versions 1.0 and 2.0.0 offered, is switched off: an Oxymax file or a session saved in Rodent
  Mode is refused with a message and nothing is loaded.
* Documentation corrected: the README and third-party notices of 2.0.0 listed LTratio among the
  lactate-threshold methods. It is not implemented. The lists now match the app, and the README
  acknowledges prominently that the lactate-threshold code is a JavaScript adaptation of
  *lactater* 1.0.0 by Felipe Mattioni Maturana (MIT License).
* The README describes the analyzer for human exercise tests.
* Fixed: in a narrow browser window the header's title and subtitle overlapped the session-status
  bar and some header buttons were out of reach. The header now grows and its buttons wrap.
* No calculation changed: ventilatory and lactate thresholds, Moxy, the Metabolic Response Map,
  comparisons, sessions and exports give the same results as in 2.0.0.

## 2.0.0 (2026-11-26)

* Runs fully offline: Chart.js 4.4.0 and xlsx-js-style 1.2.0 are included in `vendor/`; the page makes
  no request to any other host.
* Lactate-threshold methods now follow *lactater* 1.0.0 and are checked against the R package.
  Lactate thresholds can differ from those of version 1.0.
* New: Metabolic Response Map (blood lactate, carbohydrate oxidation and fat oxidation on one chart).
* New: fat oxidation and metabolic-flexibility analysis (Fatmax, crossover points).
* New: heart-rate quality checks for dropouts and artefacts.
* New: Excel workbook export, Moxy muscle-oxygenation import, AOD / MAOD calculator (switched off
  again in 2.0.1).
* New: synthetic example recordings in `examples/`.
* The file-format guide and the built-in sample file no longer show a real person's details.

## 1.0 (2026-06-03)

First public release.
