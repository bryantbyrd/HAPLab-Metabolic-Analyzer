# Third-party software in HAPLab Metabolic Analyzer

HAPLab Analyzer is a single HTML file plus two JavaScript libraries that it loads from the `vendor/`
folder. It also contains a JavaScript adaptation of the lactate-threshold methods of the R package
*lactater*. Their licences and notices are reproduced or referenced here and must stay with every copy
of the app.

## Chart.js 4.4.0

* Used for: every chart.
* File: `vendor/chart.js-4.4.0/chart.umd.js`, the unmodified `dist/chart.umd.js` of the npm package
  `chart.js@4.4.0` (sha256 `321e3a3fa98da4aaa957d10be57cbb514de0989eed8f9d726b5d05902cd01904`).
* Licence: MIT. Copyright (c) 2014-2022 Chart.js Contributors.
  Full text: `vendor/chart.js-4.4.0/LICENSE.md`.
* The build bundles `@kurkle/color` (MIT, (c) 2023 Jukka Kurkela); its notice is inside the file.
* Home page: https://www.chartjs.org

## xlsx-js-style 1.2.0

* Used for: Excel import and export.
* File: `vendor/xlsx-js-style-1.2.0/xlsx.bundle.js`, the unmodified `dist/xlsx.bundle.js` of the npm
  package `xlsx-js-style@1.2.0` (sha256 `1c7abf2993ff2cd61e508f9268e9acda0098c9796f3925d2ba0d2579072653e2`).
* Licence: Apache License, Version 2.0. Copyright (C) 2012-present SheetJS LLC; styling additions by
  the xlsx-js-style contributors. Full text: `vendor/xlsx-js-style-1.2.0/LICENSE`.
* The file was not modified. It embeds SheetJS Community Edition 0.18.5 (its own banner reads
  "xlsx-js-style 1.2.0-beta @ 2022-04-05"). The file carries no licence text itself, so the
  `LICENSE` file is kept beside it.
* Home page: https://github.com/gitbrent/xlsx-js-style

## lactater 1.0.0 (adapted, inside the HTML file)

* HAPLab contains a **JavaScript adaptation** of the R source of *lactater* v1.0.0
  ("lactater: Tools for Analyzing Lactate Thresholds") by **Felipe Mattioni Maturana**
  (https://github.com/fmmattioni/lactater). Differences from the R package are marked "HAPLAB:" in
  the code. Any error in the adaptation is HAPLab's and not the original author's.
* Adapted and used for: the lactate-threshold methods Log-log; OBLA (2.0, 2.5, 3.0, 3.5, 4.0 mmol/L);
  Bsln+ (baseline + 0.5, 1.0, 1.5 mmol/L); Dmax, ModDmax, Exp-Dmax, Log-Poly-ModDmax,
  Log-Exp-ModDmax; LTP1 and LTP2; with the curve fits 3rd- and 4th-degree polynomial, B-spline and
  exponential.
* Not adapted (not available in HAPLab): LTratio; IAT, Keul, Simon, Stegmann; LTP1-Poly-ModDmax;
  bootstrap confidence intervals; and the package's zone, training-load, reliability, MLSS, VLamax,
  performance-prediction, percentile and reporting functions. (The notices of version 2.0.0 listed
  LTratio as used; that was an error.)
* Licence: MIT. The copyright notice and permission notice below are also reproduced at the head of
  the lactate code inside the HTML file.

```
Copyright (c) 2020 Felipe Mattioni Maturana

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

## Methods and concepts (no code taken)

The app implements published methods from their descriptions, among them: Frayn (1983) for substrate
oxidation; Beaver, Wasserman & Whipp (1986) for the V-slope method; Achten et al. (2002) for Fatmax.
The Metabolic Response Map is HAPLab's own figure; its concept follows San-Millán's metabolic map.
