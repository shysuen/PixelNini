# Pixel Avatar Generator

A dependency-free, single-file pixel avatar generator built with HTML Canvas. Open it directly in a browser to generate, edit, and export pixel avatars without installing packages or starting a server.

The editor uses a **32 x 32 logical pixel grid**. Each logical pixel occupies an 8 x 8 area in the exported image, producing a final PNG size of **256 x 256 pixels**.

## Features

- Generate reproducible pixel avatars from text seeds
- Draw with a pencil, erase pixels, fill regions, and pick colors
- Choose from 1, 2, or 3-pixel brush sizes
- Draw symmetrically with horizontal mirroring
- Show or hide the editing grid
- Undo and redo up to 60 history states
- Export and import editable JSON data
- Export a grid-free 256 x 256 PNG
- Use the editor with a mouse, touchscreen, or mobile device
- Keep all data local in the browser with no server uploads

## Quick Start

Locate [`pixel-avatar-generator.html`](./pixel-avatar-generator.html) in the project directory and open it with Chrome, Edge, or Firefox.

You can also open it from PowerShell:

```powershell
Start-Process .\pixel-avatar-generator.html
```

The project has no external dependencies. You do not need to run `npm install` or start a local web server.

## Usage

### 1. Generate an Avatar

1. Enter a name, identifier, or any text in the seed field.
2. Select **Generate Avatar**.
3. The same seed always produces the same avatar.
4. Select the `↻` button next to the seed field to create a new random seed and generate an avatar immediately.

### 2. Edit the Avatar

| Tool | Description |
| --- | --- |
| Pencil | Draw pixels with the selected color |
| Eraser | Restore pixels to transparency |
| Fill | Replace a connected area of the same color |
| Picker | Select an existing color from the canvas |

Use the color picker or palette to select a color. Use the brush-size menu to choose a 1, 2, or 3-pixel brush.

When **Mirror Drawing** is enabled, pixels drawn on one side are copied to the opposite side. This is useful for creating symmetrical faces. **Show Grid** only changes the editor preview and never appears in the exported PNG.

### 3. Undo and Redo

Use the **Undo** and **Redo** buttons or the following keyboard shortcuts:

| Action | Windows / Linux | macOS |
| --- | --- | --- |
| Undo | `Ctrl + Z` | `Command + Z` |
| Redo | `Ctrl + Y` or `Ctrl + Shift + Z` | `Command + Shift + Z` |

### 4. Save Editable Data

Select **Export Data** to download `pixel-avatar.json`. The file contains the seed, grid dimensions, and color value of every pixel, allowing you to continue editing later.

Select **Import Data** and choose a previously exported JSON file to restore an avatar. The current version only accepts data created with a 32 x 32 grid.

### 5. Export a PNG

Select **Download PNG** to save the avatar. The filename follows this format:

```text
pixel-avatar-seed.png
```

The exported image is always 256 x 256 pixels. The editing grid is excluded, and areas removed with the eraser or **Clear Canvas** remain transparent.

## Project Files

```text
.
|-- pixel-avatar-generator.html  # Page, styles, and application logic
|-- README.md                    # Chinese documentation
`-- README-en.md                 # English documentation
```

`pixel-avatar-generator.html` contains all HTML, CSS, and JavaScript required by the application. You only need this file when moving or sharing the tool.

## Customization

Avatar generation and canvas settings are defined near the beginning of the `<script>` block in the HTML file:

```javascript
const OUTPUT_SIZE = 256;
const GRID_SIZE = 32;
const CELL_SIZE = OUTPUT_SIZE / GRID_SIZE;
const MAX_HISTORY = 60;
```

- `OUTPUT_SIZE` controls the exported image width and height.
- `GRID_SIZE` controls the logical pixel-grid dimensions.
- `MAX_HISTORY` controls the maximum number of undo states.
- `PALETTE` contains the preset colors displayed in the editor.

When changing `GRID_SIZE`, make sure `OUTPUT_SIZE / GRID_SIZE` is an integer. JSON data created with a different grid size cannot be imported directly.

## Browser Compatibility

Use a recent version of Chrome, Edge, or Firefox. The browser must support Canvas, Pointer Events, FileReader, Blob, and `HTMLCanvasElement.toBlob()`.

If no file appears after selecting a download button, check whether the browser has blocked downloads from local pages.

