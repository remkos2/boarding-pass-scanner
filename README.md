# Flight Ticket Barcode Scanner

A fully local, offline boarding-pass scanner. No internet, no installs, no data leaves your computer.

## How to use

1. Double-click **`index.html`** and it opens in your browser.
2. Drag in a photo of a boarding pass, click to choose one, or paste with Ctrl+V.
3. The decoded details appear: passenger, route, flight, date, seat, cabin, booking reference (PNR), and check-in status.

Works on both your computers since it lives in OneDrive.

## What it reads

Boarding passes store their data in a 2D barcode: **PDF417** on paper printouts and **Aztec** on mobile passes. Both encode the IATA "BCBP" string, which this tool decodes and parses. QR and Data Matrix are also attempted as a fallback.

Decoding uses the **zxing-cpp** engine compiled to WebAssembly, the same high-accuracy engine used by professional tools, bundled locally so it runs fully offline.

## Tips for a good scan

- Crop the photo to mostly the barcode, shot straight-on.
- Avoid glare and blur; more pixels on the barcode is better.
- A clean screenshot of a mobile pass works best of all.

Note on partial barcodes: 2D barcodes carry error correction, so the engine tolerates some dirt, glare, or minor damage. But a barcode that is physically cut off (missing whole rows/columns) usually cannot be decoded, because the missing data can't be reconstructed.

## Putting it online (Google Sites)

The whole tool is self-contained, so it runs from any public web address with no backend.

1. Create a **public GitHub repo** and upload this folder's contents (`index.html` + the
   `lib/` folder, structure intact).
2. Repo → **Settings → Pages** → deploy from branch `main`, folder `/ (root)`. After a
   minute you get `https://<username>.github.io/<repo>/`.
3. In Google Sites: **Insert → Embed → Embed code**, then paste:
   ```html
   <iframe src="https://<username>.github.io/<repo>/"
           style="width:100%;height:900px;border:0;"
           allow="clipboard-read; clipboard-write"></iframe>
   ```
   Place it, resize, Publish.

Inside the Google Sites frame the file picker works; Ctrl+V paste may be blocked by
Google's sandbox (a Google limitation, not the tool).

## Files

- `index.html`: the scanner (open this, or double-click it locally).
- `lib/zxing-reader.iife.js`: the decoding engine (zxing-cpp), kept local.
- `lib/zxing-wasm-binary.js`: the engine's WebAssembly module embedded as text, so the page never needs to download or fetch anything.
- `LICENSE` and `THIRD-PARTY-NOTICES.md`: your MIT license plus attribution for the bundled engine.
