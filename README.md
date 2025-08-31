# Military Symbol Explorer

This project provides a simple, stand‑alone web application for exploring and downloading MIL‑STD‑2525 / APP‑6 military symbols.  It loads the official **Joint Military Symbology Markup Language (JMSML)** data set on the fly, lets you search and filter thousands of symbols, preview them in a grid and batch‑download selected symbols as SVG files.

## Features

- **Comprehensive data set** – When the page loads it fetches every `LegacySymbol` definition from the `joint‑military‑symbology‑xml` repository.  This covers all MIL‑STD‑2525D / APP‑6D symbol sets (land units, equipment, installations, air/sea/space platforms, control measures, fires areas, weather overlays, etc.), resulting in over 2 000 unique symbols.
- **Live search and filtering** – A search box filters symbols by name or category, and a category drop‑down lets you narrow results to a specific symbol set.  Use the optional **View selected** toggle to show only the cards you’ve chosen.
- **Multi‑selection with persistent state** – Clicking on a card toggles its selection.  Selected cards are highlighted and counted; you can also select all visible symbols or clear the selection.
- **Preview and batch download** – Each card shows a preview rendered via the [milsymbol](https://github.com/spatialillusions/milsymbol) library.  Clicking **Download Selected** packages all selected symbols into a ZIP archive containing individual SVG files.
- **Graceful handling of missing icons** – The renderer attempts multiple SIDC conversions (numeric and letter formats) for each symbol.  If the underlying library can’t draw a particular code, the application displays a neutral placeholder instead of a spurious question‑mark icon.
- **Modern light‑mode interface** – The UI is built with plain HTML, CSS and vanilla JavaScript.  The header is sticky, controls are grouped logically, and checkboxes show clear tick marks when selected.

## Usage

1. Clone or download this repository.
2. Open `index.html` in any modern browser.  The page will immediately begin downloading symbol definitions (requires internet access).
3. Use the search field and category filter in the top bar to find specific symbols.  The summary line below the search bar shows the number of matching symbols and how many you’ve selected.
4. Click on a symbol card to select or deselect it.  Selected cards are outlined in blue and display a tick mark in their corner.
5. To download your selection as a ZIP file of SVGs, click **Download Selected**.  The file names correspond to the symbols’ SIDC codes.

## Technical Notes

- The application relies on the [Joint Military Symbology XML](https://github.com/Esri/joint-military-symbology-xml) project for symbol definitions and on the [milsymbol](https://github.com/spatialillusions/milsymbol) library for rendering.  Both are loaded at runtime via CDN.  Because the data is fetched directly from GitHub, the page must be served with network connectivity.  It will not function offline.
- Some control‑measure symbols share the same base glyph according to the standard (e.g. many fires areas use a hook‑shaped icon).  This is intentional; differences between these symbols are conveyed by their names and modifiers rather than by distinct shapes.
- A small number of symbols are not yet supported by milsymbol.  In those cases the application displays a grey placeholder in the card and skips the file when downloading.

## Development

This repository contains only two files (`index.html` and this `README.md`) and has no build step.  To modify the behaviour or appearance:

- Edit `index.html` to adjust styles, change the user interface, or customise the symbol‑loading logic.  The script section defines functions for loading JMSML files, filtering/searching, rendering the grid and handling downloads.
- If you need to extend the symbol set or change how names are generated, modify the `loadJMSML()` function.  It parses each instance XML file, builds a mapping of IDs to labels, and constructs a `symbolData` array of `{ name, sidc, category }` objects.

## License

This project itself is provided under the MIT License.  Note that the JMSML data and milsymbol library have their own licenses; please consult their respective repositories for details.

