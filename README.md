# Photobooth Studio

Photobooth Studio is a browser-based photobooth application that uses your device’s camera, captures photo sequences, builds a printable photo strip, and can send the final strip by email.

## Features

- Camera access with device selection
- Live preview with optional mirror mode
- Countdown before each capture
- Automatic multi-shot capture flow for a full session
- Layout support for:
  - 2×6 — 3 photo
  - 2×6 — 4 photo
  - 4×6 — 6 photo
  - 4×6 — 8 photo
  - 2×3 (DS: 3 photos)
  - 2×3 (DS: 4 photos)
  - 4R Landscape - Right
  - 4R Landscape - Left
- Duplicate-by-row mode for 4×6 and 4x8 layouts
- Per-slot retake
- Template overlay support
- Save strip to device as PNG
- Print strip only
- Send strip by email through Google Apps Script

## How it works

1. Open the page.
2. Click **Start Camera**.
3. Choose the camera device if needed.
4. Select a layout.
5. Set the countdown duration.
6. Click **Capture** once.
7. The app counts down, captures the first photo, waits 1.5 seconds, then continues until the layout is filled.
8. The finished strip appears in the preview and can be saved, printed, or emailed.

## Layouts

### Standard strip layouts

- **2×6 — 3 photo**  
  600 × 1800 px
- **2×6 — 4 photo**  
  600 × 1800 px
- **4×6 — 6 photo**  
  1200 × 1800 px
- **4×6 — 8 photo**  
  1200 × 1800 px
- **2×3 (DS: 3 photos)**  
  1200 × 1800 px
- **2×3 (DS: 4 photos)**  
  1200 × 1800 px

### Landscape layouts

- **4R Landscape - Right**  
  1800 × 1200 px
- **4R Landscape - Left**  
  1800 × 1200 px

## Duplicate-by-row mode

When **Duplicate by row (4×6 only)** is enabled:

- `grid6` captures only **3 shots**
- `grid8` captures only **4 shots**
- Each captured shot is duplicated across the row slots
- This is useful when you want the same image repeated across a row instead of taking separate photos for each slot

## Controls

### Camera & capture
- **Start Camera** — requests camera permission and starts the preview
- **Refresh Cameras** — reloads available video devices
- **Capture** — starts the capture sequence or retakes the selected slot
- **New Session** — clears all captured photos
- **Clear Template** — removes the overlay template

### Layout controls
- **Strip layout** — chooses the strip design
- **Filter** — applies a preview/capture filter
- **Countdown seconds** — sets the delay before each shot
- **Template overlay** — uploads a PNG/JPG overlay artwork

### Toggles
- **Mirror preview** — mirrors the live preview
- **Auto print after final capture** — opens print view automatically after the strip is complete
- **Duplicate by row (4×6 only)** — enables row duplication mode for 4×6 layouts

## Saving, printing, and email

### Save to Device
Downloads the completed strip as a PNG file.

### Print Strip Only
Opens a print window with only the final strip image.

### Send via Email
Sends the final strip as a PNG attachment through Google Apps Script.

## Duplicate-by-row mode details

This mode applies only to `grid6` and `grid8`.

- `grid6` becomes a 3-shot session
- `grid8` becomes a 4-shot session
- The captured photo is reused across both slots in the same row

## File structure

Typical project files:

- `index.html` — main frontend UI and capture flow
- `photobooth_strip_guides.json` — layout guide coordinates
- `photobooth_strip_guides.txt` — layout guide notes

## Setup

### 1. Use a modern browser
Photobooth Studio relies on browser camera access. Use Chrome, Edge, or another modern browser with media permission support.

### 2. Allow camera permission
When prompted, allow the browser to use your camera.

### 3. Configure Google Apps Script
If you want email sending to work, update the Apps Script web app URL in the code so it matches your deployed script endpoint.

## Usage

### Starting a session
- Open the page
- Click **Start Camera**
- Select the correct camera if needed

### Capturing photos
- Choose the layout
- Set the countdown seconds
- Click **Capture** once
- The app automatically continues through the full session

### Retaking a photo
- Click **Retake** on a slot in the preview
- Press **Capture** again
- Only that slot will be replaced

### Saving and printing
- Click **Save to Device** to download the strip as a PNG
- Click **Print Strip Only** to open the print view

### Sending by email
- Enter the recipient email
- Click **Send via Email**

## Layout logic

The app builds each strip from layout geometry defined in the JavaScript configuration.

Important values include:

- `width` and `height` — canvas size for the layout
- `cols` and `rows` — number of grid slots
- `footerRatio` — reserved lower design area for standard strip layouts
- `allowDuplicateByRow` — enables row duplication for supported 4×6 layouts

Landscape layouts use their own geometry logic through `getLayoutGeometry(layout)`.

## Template overlay workflow

If you are creating a transparent artwork overlay, match the exact canvas size for the target layout:

- 2×6 layouts: **600 × 1800 px**
- 4×6 layouts: **1200 × 1800 px**
- 4R landscape layouts: **1800 × 1200 px**

Place the artwork around the photo slots defined by the layout geometry, then export it as a transparent PNG and upload it through **Template overlay**.

## Notes

- The app captures images to an internal canvas before rendering them into the strip.
- The preview shows slot positions and lets you retake individual photos.
- Filters affect both the live preview and the captured image.
- The export canvas is used for both saving and printing.

## Configuration reminder

The email feature depends on a deployed Google Apps Script web app. If the URL in the code is not set correctly, email sending will not work.
