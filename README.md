[日本語](README_JP.md)/English

# Fontmiru

A browser-based font inspection tool. Load a font file and check its typesetting, OpenType features, variable axes, glyph repertoire and internal tables.

Fontmiru is built with Japanese fonts in mind: you can also check how fonts behave in **vertical text** and how **proportional metrics for Japanese (`palt` / `vpal` and friends)** take effect. All parsing happens inside the browser — your font files never leave your device.

 ![Screenshot](screenshot.png) 


## Live Demo

[https://toktaro.github.io/Fontmiru/](https://toktaro.github.io/Fontmiru/)

## Features

### Preview

- **Horizontal / Vertical**: Switch writing mode with one click. In vertical mode you can also check `vert` glyphs and the orientation of Latin text (`text-orientation`)
- **OpenType Feature Toggles**: Lists every feature the font contains and lets you set each one to Default / ON / OFF. Japanese-related features (`palt` `vpal` `pkna` `kern` `vkrn` `halt` `vhal` `chws` and more) are listed first
- **Compare with Default**: Shows the text with and without your feature settings side by side
- **1em Grid**: Changes in advance widths caused by proportional metrics become visible against the grid
- **Layout Controls**: Size, line height and letter spacing via sliders or numeric input, plus start / center / end alignment
- **Sample Text**: Presets for punctuation, kana, mixed Japanese/Latin text and more, and you can save your own edited text as "My Samples"
- **Font Mixing**: Using the selected font as the base, assign a different font to each character class — Kanji / Hiragana / Katakana / Punctuation & Symbols / Latin / Digits (e.g. a kana font combined with kanji from another font). A size ratio can be set per class

### Variable Fonts

- **Axis Controls**: Parses `fvar` and provides a slider and numeric input for each axis
- **Named Instances**: Apply an instance from the list, or view all instances side by side
- **Animation**: Sweep any axis back and forth automatically to watch it change

### Glyph List

- **Character Repertoire**: Parses `cmap` and shows every encoded glyph in a grid (glyph names come from the `post` table)
- **Filter & Search**: By Unicode block, character, `U+XXXX` or glyph name
- **Export**: Copy the characters to the clipboard, or save them as a per-block `.txt` or a `.csv` with BOM
- **Glyph Metrics**: Double-click a glyph to see its advance, side bearings (LSB / RSB, and TSB / BSB for vertical), vertical origin (`VORG`) and bounding box, with annotated diagrams

### Font Info & Tables

- **Font Info**: Key `name` table entries and metrics (`OS/2` / `head` / `hhea` / `vhea`) at a glance
- **Credits & License**: Manufacturer, designer (with URLs), Vendor ID, copyright, trademark, license text and URL, and embedding permissions (fsType) in one place
- **Table List**: Parsed values for the major tables (`head` `hhea` `vhea` `maxp` `post` `OS/2` `name` `cmap` `fvar` `GDEF` `GSUB` `GPOS`); unsupported tables show a hex dump of their first bytes
- **GDEF Version**: Shows the raw majorVersion / minorVersion, which is handy for checking what your font editor exported
- **Spec Links**: The ⓘ next to each table opens the Microsoft OpenType specification (or Apple's TrueType Reference Manual for AAT tables)

### Convenience

- **Favorites**: Star (☆) a font you use often, and next time you can open it with a single click from the Favorites list in the sidebar. If you load a different file with the same name, you can update the saved copy
- **Themes**: Follow the OS setting, or choose Light / Dark
- **Collapsible Sidebar**: Click a section heading to fold it; the open/closed state is remembered
- **Fully Local**: Everything runs in the browser; no font file is ever uploaded to a server

## Usage

### Basic Workflow

1. Open `index.html` in your browser (or visit the Live Demo)
2. Drop font files onto the left panel, or click to choose them (multiple files supported)
3. In "プレビュー" (Preview), check the typesetting and switch writing mode, OpenType features, variable axes and so on
4. Browse the repertoire in "グリフ一覧" (Glyph List), and open font info and tables with the ⓘ button

### Trying Font Mixing

1. Load the base font (e.g. a kana font) and the font you want to combine with it (e.g. a kanji font)
2. Select the base font in the font list
3. Turn on "混植" (Font Mixing) in the sidebar and choose a font and size ratio for each character class

### About Favorites

Browsers cannot reopen a file from its location on disk, so a favorited font is saved as a copy inside the browser (IndexedDB). Favorites are stored separately for each browser and each URL you use. Removing a favorite also deletes its saved copy.

## Technical Specifications

- **Requirements**: Modern browsers (Chrome and Safari recommended; also works in Firefox and Edge)
- **Dependencies**: None (no external libraries or CDNs)
- **File Format**: Single HTML file (CSS & JavaScript embedded)

### Supported Formats

| Format | Display | Analysis (axes, features, glyphs, tables) |
|--------|---------|------|
| TTF / OTF | Yes | Yes |
| TTC / OTC | Yes (all faces expanded) | Yes |
| WOFF | Yes | Yes |
| WOFF2 | Yes | No (display only) |

### Known Limitations

- The glyph list only shows glyphs that have a character code assigned (glyphs without one, such as `vert` alternates, cannot be displayed)
- How proportional metrics and kerning are rendered depends on the browser's text shaping
- Glyph metrics are the values of the default instance (variable font deltas are not applied). For CFF-outline fonts, the bounding box is an approximation measured by the browser
- Font mixing switches fonts character by character, so kerning between characters from different fonts, and OpenType features that depend on neighboring characters, do not apply. Size ratios scale from the baseline
- `cmap` formats 4 and 12 are supported

## License

This project is licensed under the [MIT License](LICENSE.md).

Free to use for both personal and commercial purposes. If you modify and publish it, sharing your source would be appreciated — though it is not required.

This tool is still in testing (Beta), and the accuracy of what it displays and reports is not guaranteed. No warranty is provided for any damage arising from its use.

Please handle any font files you load in accordance with each font's own license.

(c) 2026- toktaro
