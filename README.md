# Photobooth Studio

Photobooth Studio is a browser-based photobooth application that uses the device camera, captures a guided photo sequence, builds a printable photo strip, and can optionally send the final strip through Google Apps Script.

## Features

* Camera access with device selection
* Countdown before each capture
* Continuous capture flow for a full session
* Layout support for:

  * 2×6 — 3 photo
  * 2×6 — 4 photo
  * 4×6 — 6 photo
  * 4×6 — 8 photo
* Duplicate-by-row mode for 4×6 layouts
* Preview strip with automatic slot filling
* Retake per slot
* Template overlay support
* Save strip to device
* Print strip only
* Email strips to users

## How it works

1. Start the camera.
2. Choose the layout.
3. Press **Capture** once.
4. The app performs the countdown, captures the first photo, waits 1.5 seconds, then continues until the layout is filled.
5. The finished strip appears in the preview and can be saved, printed, or emailed.

## Duplicate-by-row mode

When **Duplicate by row (4×6 only)** is enabled:

* The app captures only **3 shots** for `grid6` or **4 shots** for `grid8`.
* Each captured shot is duplicated across the two slots in that row.
* This is useful when you want the same image repeated across a row instead of taking separate images for each slot.

## Strip guide sizes

### Canvas sizes

* `3 strips`: 600 × 1800 px
* `4 strips`: 600 × 1800 px
* `3x2 strips`: 1200 × 1800 px
* `4x2 strips`: 1200 × 1800 px

### Gap thickness

* Vertical gap between rows: **21 px**
* Horizontal gap between columns on 4×6 layouts: **24 px**
* Footer/design area height: **396 px**
* Footer starts at: **y = 1404 px**

## Files

Typical project files:

* `Index.html` — frontend user interface and capture flow
* `photobooth_strip_guides.json` — exact layout coordinates for each strip design
* `photobooth_strip_guides.txt` — human-readable guide

## Setup

### 1. Use a modern browser

PhotoBooth Studio relies on camera access through browser media permissions. Use Chrome, Edge, or another modern browser with camera support.

### 2. Enable camera permission

Allow the browser to use the camera when prompted.

### 3. Configure Google Apps Script

If you want email sending to work, make sure the Apps Script web app URL in the code matches your deployed script URL.

## Usage

### Starting a session

* Open the page.
* Click **Start Camera**.
* Select the correct camera if needed.

### Capturing photos

* Choose the layout.
* Set the countdown seconds.
* Click **Capture** once.
* The app will automatically continue through the full session.

### Retaking a photo

* Click **Retake** on a slot in the preview.
* Press **Capture** again.
* Only that slot will be replaced.

### Saving and printing

* Click **Save to Device** to download the strip as a PNG.
* Click **Print Strip Only** to open the print view.

### Sending by email

* Enter the recipient email.
* Click **Send via Email**.

## Editing layout spacing and placement

If you want to change spacing or location of the strips, edit the layout guide logic in `buildSlots(layout)`.

The key values are:

* `marginX` — left and right inset
* `marginY` — top inset
* `gapX` — horizontal gap between columns
* `gapY` — vertical gap between rows
* `footerRatio` — reserved lower design area

The exact strip coordinates are also listed in `photobooth_strip_guides.json`.

## Transparent strip design workflow

If you are creating a transparent artwork overlay, match the exact canvas size for the layout:

* 2×6 layouts: 600 × 1800 px
* 4×6 layouts: 1200 × 1800 px

Place your artwork around the slot coordinates in the guide file, and keep transparency in the exported overlay image.
