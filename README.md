# Boarding Pass Scanner

Read the barcode on a flight boarding pass straight from a photo, entirely in your browser. Drop in a picture and it shows the passenger, route, flight, date, seat, cabin class and booking reference. Nothing is uploaded and there is no server.

**Live demo:** https://remkos2.github.io/boarding-pass-scanner/

## What it does

Boarding passes store their details in a 2D barcode (PDF417 on printed passes, Aztec on mobile passes), written in the IATA BCBP format. This tool decodes that barcode from a photo and turns it into readable fields:

- Passenger name
- Route (departure and arrival airports)
- Flight number and airline
- Date of travel
- Seat and cabin class
- Booking reference (PNR)
- Check-in status

PDF417, Aztec, QR and Data Matrix are all supported.

## Why it is different

- **Private by design.** Everything runs locally in your browser. The image never leaves your device and nothing is stored.
- **Fully offline.** The decoding engine is bundled inside the page, so it works with no internet connection. You can save the page and open it as a local file.
- **No install, no backend, no tracking.** It is a single static page.

## How to use it

**Online:** open the live demo, then drop in a photo, click to choose one, or paste an image with Ctrl+V.

**Offline on your own machine:** click `Code`, then `Download ZIP`, unzip it, and double-click `index.html`. It works the same way with no internet.

For the best result use a sharp, straight-on photo with the barcode filling the frame and no glare. A screenshot of a mobile pass works particularly well.

## Limitations

2D barcodes carry error correction, so the engine copes well with glare, blur and minor damage. A barcode that is physically cut off, with whole rows or columns missing from the photo, cannot be decoded, because the missing data cannot be reconstructed. There is no partial read: the barcode either resolves in full or not at all.

## Embedding it on a website

I built this to sit on my own website, which runs on Google Sites. Google Sites cannot host a multi-file app directly, so it loads the published page inside a frame. This is the embed I use, pointing at my own deployed copy:

```html
<iframe src="https://remkos2.github.io/boarding-pass-scanner/"
        style="width:100%;height:900px;border:0;"
        allow="clipboard-read; clipboard-write"></iframe>
```

If you want to do the same, deploy your own copy (GitHub Pages works well) and swap in your URL. Inside an embedded frame the file picker works normally, but Ctrl+V paste may be blocked by the host's sandbox.

## How it works under the hood

- The interface and the BCBP parser are plain HTML and JavaScript, with no framework.
- Decoding is handled by zxing-cpp compiled to WebAssembly (via zxing-wasm), bundled in `lib/` as text so the page never has to fetch anything.

## Repository structure

```
index.html                 the app
lib/zxing-reader.iife.js   decoding engine (zxing-wasm)
lib/zxing-wasm-binary.js   engine WebAssembly, embedded as base64 text
LICENSE                    MIT license for this project
THIRD-PARTY-NOTICES.md     attribution for the bundled engine
```

## Credits and license

This project is released under the MIT license (see `LICENSE`). Barcode decoding uses the open-source [zxing-wasm](https://github.com/Sec-ant/zxing-wasm) (MIT) by Ze-Zheng Wu, built on [zxing-cpp](https://github.com/zxing-cpp/zxing-cpp) (Apache-2.0). Full attribution is in `THIRD-PARTY-NOTICES.md`.

Built by Remko Stas.
