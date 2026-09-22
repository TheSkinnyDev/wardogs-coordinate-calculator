# Wardogs Coordinate Calculator

A single-page calculator that converts two map coordinates into a straight-line range in metres and a compass heading from your position to the target.

Built with plain HTML, CSS, and JavaScript. No installation, dependencies, or backend required.

## Usage

1. Paste your coordinates into **Your position**.
2. Paste the destination into **Target position**.
3. The range and heading update automatically.

Use this coordinate format:

```text
x97.36, y109.56
```

### Example

**Your position:** `x97.36, y109.56`  
**Target position:** `x95.25, y108.02`

```text
RANGE 261 M
HEADING 234 SW
```

Range is rounded to the nearest metre. Heading is rounded to the nearest degree, measured clockwise from north: north is 0°, east is 90°, south is 180°, and west is 270°.

The compass label uses eight directions: N, NE, E, SE, S, SW, W, and NW.

## Features

- Calculates automatically as you type or paste.
- Always displays range in metres, including distances over 1,000 metres.
- Copies both result lines with **Copy result**.
- Reverses the starting point and destination with **Swap positions**.
- Accepts negative coordinates, decimal values, and uppercase or lowercase X/Y labels.
- Supports adjustable map scale and Y-axis orientation.
- Works offline and on mobile browsers.

## Map settings

The defaults are:

| Setting | Default |
| --- | --- |
| Scale | 100 metres per coordinate unit |
| East | Higher X values |
| North | Higher Y values |

Open **Map settings** to change the metres per coordinate unit or select **Lower Y values** if your map's Y-axis increases southward.

These are flat map coordinates, not latitude and longitude. Range is the straight-line distance; it does not account for terrain, elevation, or travel routes.

The distance calculation is:

```text
range_metres = sqrt((target_x - your_x)² + (target_y - your_y)²) × scale
```

If both positions are identical, the result is `RANGE 0 M` with no heading. Positive distances below half a metre display as `RANGE <1 M`.

## Run locally

Download `index.html` and open it in a web browser. If your downloaded file is named `Coordinate-Calculator.html`, rename it to `index.html` before uploading it to GitHub Pages.

## Publish with GitHub Pages

1. Create a public GitHub repository.
2. Upload `index.html` to the repository's root folder and commit it.
3. Open **Settings → Pages**.
4. Under **Build and deployment**, select **Deploy from a branch**.
5. Select the **main** branch and **/(root)** folder, then click **Save**.
6. Once deployment finishes, open the website link shown on the Pages settings screen.

The website address will follow this pattern:

```text
https://YOUR-USERNAME.github.io/YOUR-REPOSITORY/
```

To update the calculator, replace `index.html` in the repository and commit the changes. GitHub Pages will redeploy the page.

## Privacy

All calculations run locally in your browser. The calculator does not send coordinates to a server, use analytics, or require an account.
