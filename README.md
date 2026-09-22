# Wardogs Coordinate Calculator

A simple map calculator that gives you the straight-line distance and compass heading from your position to a target. Paste two coordinates to get a result you can quickly read or copy:

```text
RANGE 261 M
HEADING 234 SW
```

All calculations run in your browser. No account is needed, and your coordinates are not sent anywhere.

## How to use it

1. Paste your current coordinates into **Your position**.
2. Paste the destination coordinates into **Target position**.
3. Read the result, which updates automatically as you type or paste.

Enter each position in this format:

```text
x97.36, y109.56
```

Spaces, uppercase or lowercase X/Y labels, negative numbers, and decimal values are supported.

- **Copy result** copies both the range and heading lines.
- **Swap positions** reverses the starting point and destination.
- **Map settings** lets you adjust the coordinate scale and the direction of the Y-axis.

## Reading the result

| Output | Meaning |
| --- | --- |
| `RANGE 261 M` | The target is approximately 261 metres away in a straight line. |
| `HEADING 234 SW` | Head toward 234° clockwise from north, broadly southwest. |

Distances are always shown in metres, even above 1,000 metres, and are rounded to the nearest whole metre. Headings are rounded to the nearest whole degree.

The compass label is the nearest of eight directions:

| Direction | Label | Centre heading |
| --- | --- | --- |
| North | N | 0° |
| Northeast | NE | 45° |
| East | E | 90° |
| Southeast | SE | 135° |
| South | S | 180° |
| Southwest | SW | 225° |
| West | W | 270° |
| Northwest | NW | 315° |

Each compass label covers a 45° sector centred on its listed heading. For example, a heading of 234° falls within the southwest sector.

If both coordinates are identical, the calculator displays `RANGE 0 M` and `HEADING —`, because there is no direction to travel. A positive distance below half a metre displays as `RANGE <1 M`.

## Map scale and orientation

By default, the calculator assumes:

- **One coordinate unit equals 100 metres.**
- **X increases eastward.**
- **Y increases northward.**

Under **Map settings**, change **Metres per coordinate unit** if your map uses a different scale. For example, a value of `100` means a change from `x97` to `x98` represents 100 metres.

If Y values increase as you move south on your map, set **North is toward** to **Lower Y values**. This changes the heading calculation without changing the distance.

## How the calculations work

### 1. Find the displacement

Subtract your position from the target position:

```text
Δx = target_x − your_x
Δy = target_y − your_y
```

Using the example:

```text
Your position:   x97.36, y109.56
Target position: x95.25, y108.02

Δx = 95.25 − 97.36 = −2.11
Δy = 108.02 − 109.56 = −1.54
```

With the default orientation, this places the target west and south of you.

### 2. Calculate the range

The calculator uses the Pythagorean theorem to find the straight-line distance, then multiplies by the map scale:

```text
range_metres = √(Δx² + Δy²) × metres_per_unit
```

For the example:

```text
range_metres = √((−2.11)² + (−1.54)²) × 100
             = √6.8237 × 100
             ≈ 261.22 metres
```

Rounded to the nearest metre, the result is **261 M**.

### 3. Calculate the heading

The calculator treats the horizontal displacement as eastward movement and adjusts the vertical displacement to represent northward movement:

```text
east  = Δx
north = Δy      when higher Y means north
north = −Δy    when lower Y means north
```

It then uses `atan2` to find the clockwise angle from north:

```text
heading_degrees = (atan2(east, north) × 180 / π + 360) % 360
```

Here, `% 360` wraps the angle into the range from 0° up to, but not including, 360°. The argument order `atan2(east, north)` makes north the zero-degree reference.

For the example, the angle is approximately **233.88°**, displayed as **234**. The nearest compass direction is **SW**, producing:

```text
RANGE 261 M
HEADING 234 SW
```

The compass label is calculated from the unrounded angle. If rounding the numeric heading produces 360°, it is displayed as 0°.

## What the range represents

This calculator is designed for flat X/Y map coordinates with the same scale on both axes. It does not calculate geographic distances from latitude and longitude.

The range is the direct distance between the two points. It does not account for terrain, elevation, obstacles, roads, or the route you may need to travel. Accuracy depends on the coordinates and map scale you provide.


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
