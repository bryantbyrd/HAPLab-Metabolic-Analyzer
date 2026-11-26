# vendor/

The two JavaScript libraries HAPLab Analyzer needs. The HTML file loads them from here with relative
paths, so **this folder must stay in the same folder as the HTML file**.

| Folder | Library | File | Licence | sha256 of the file |
|---|---|---|---|---|
| `chart.js-4.4.0/` | Chart.js 4.4.0 | `chart.umd.js` | MIT (`LICENSE.md`) | `321e3a3fa98da4aaa957d10be57cbb514de0989eed8f9d726b5d05902cd01904` |
| `xlsx-js-style-1.2.0/` | xlsx-js-style 1.2.0 | `xlsx.bundle.js` | Apache-2.0 (`LICENSE`) | `1c7abf2993ff2cd61e508f9268e9acda0098c9796f3925d2ba0d2579072653e2` |

Both files are the unmodified browser builds published in the npm packages `chart.js@4.4.0`
(`dist/chart.umd.js`) and `xlsx-js-style@1.2.0` (`dist/xlsx.bundle.js`). Do not edit them. To check a
copy, compare its sha256 with the table (PowerShell: `Get-FileHash <file> -Algorithm SHA256`).

To update a library, replace the folder with the new version's published build and licence, change
the two `<script src="vendor/...">` lines in the HTML file and the names in its start-up check, update
this table and `THIRD-PARTY-NOTICES.md`, and run the tests.
