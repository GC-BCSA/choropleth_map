# KBC ChoroplethMap

**Live tool:** *(deploy choropleth-map.html to your host and link here)*

A browser-based US choropleth mapping tool. Plot up to 6 data layers at the state or county level with full color scale controls, pan, and zoom. No installation required — open the file and go.

---

## Quick Start

1. Click **+ ADD LAYER** in the sidebar
2. Select **STATE** or **COUNTY** from the Level dropdown
3. Paste your data into the text area (see [Data Format](#data-format) below)
4. Adjust the color scheme, scale type, and range as needed
5. Click **PLOT DATA**
6. Zoom and pan the map to your area of interest
7. Click **EXPORT PNG** to download a high-resolution image

---

## Header Controls

All header controls are uniform width and height. From left to right:

<table>
<tr>
<td><kbd style="background:#21409A;color:#fff;padding:6px 16px;border-radius:5px;font-family:monospace;font-size:12px;border:none;display:inline-block">US 48+AK/HI</kbd></td>
<td>Map view showing the contiguous 48 states with Alaska and Hawaii insets. Projection is fixed to Albers USA.</td>
</tr>
<tr>
<td><kbd style="background:#1A204C;color:rgba(255,255,255,0.6);padding:6px 16px;border-radius:5px;font-family:monospace;font-size:12px;border:1px solid rgba(255,255,255,0.3);display:inline-block">LOWER 48</kbd></td>
<td>Contiguous 48 states only. Alaska and Hawaii are excluded. Projection is selectable.</td>
</tr>
<tr>
<td><kbd style="background:#1A204C;color:rgba(255,255,255,0.6);padding:6px 16px;border-radius:5px;font-family:monospace;font-size:12px;border:1px solid rgba(255,255,255,0.3);display:inline-block">WORLD</kbd></td>
<td>World view with country borders and US state overlays. Projection is selectable.</td>
</tr>
<tr>
<td><kbd style="background:#21409A;color:#fff;padding:6px 16px;border-radius:5px;font-family:monospace;font-size:12px;border:none;display:inline-block">PLOT DATA</kbd></td>
<td>Parses all entered data, resolves state/county identifiers to FIPS codes, and renders the choropleth fills on the map. Run this after entering or changing data.</td>
</tr>
<tr>
<td><kbd style="background:rgba(255,255,255,0.1);color:#fff;padding:6px 16px;border-radius:5px;font-family:monospace;font-size:12px;border:1px solid rgba(255,255,255,0.25);display:inline-block">&#9635; WATER</kbd></td>
<td>Checkbox toggle. When checked, the ocean/water background is visible on the map and included in exports. Uncheck for a transparent background in the exported PNG.</td>
</tr>
<tr>
<td><kbd style="background:rgba(255,255,255,0.1);color:#fff;padding:6px 16px;border-radius:5px;font-family:monospace;font-size:12px;border:1px solid rgba(255,255,255,0.25);display:inline-block">&#9635; LEGEND</kbd></td>
<td>Checkbox toggle. Shows or hides the legend overlay in the lower-left corner of the map. The legend displays a gradient bar with min/max values for each visible layer.</td>
</tr>
<tr>
<td><kbd style="background:rgba(255,255,255,0.1);color:#fff;padding:6px 16px;border-radius:5px;font-family:monospace;font-size:12px;border:1px solid rgba(255,255,255,0.25);display:inline-block">RESET</kbd></td>
<td>Resets pan and zoom back to the default fitted view for the current map selection.</td>
</tr>
<tr>
<td><kbd style="background:rgba(52,211,153,0.1);color:#34d399;padding:6px 16px;border-radius:5px;font-family:monospace;font-size:12px;border:1px solid #34d399;display:inline-block">EXPORT PNG</kbd></td>
<td>Exports the current map view as a PNG. The shortest side is always 2000px. The current pan/zoom position is captured as-is.</td>
</tr>
</table>

---

## Map Views

| View | Projection | Description |
|---|---|---|
| US 48+AK/HI | Albers USA (fixed) | All 50 states. Alaska and Hawaii rendered as insets in the lower left. |
| Lower 48 | Selectable | Contiguous states only. Zoom in without the AK/HI insets. |
| World | Selectable | Full world with country borders and US state detail overlaid. |

**Pan:** click and drag anywhere on the map.  
**Zoom:** scroll wheel. Scale range is 0.5× to 200×.  
**Reset:** click RESET in the header to return to the default fit.

---

## Projections

Available projections vary by map view. The dropdown appears in the sidebar below the layer list when Lower 48 or World is active. It is hidden for US 48+AK/HI, which is always Albers USA.

| Projection | Available For |
|---|---|
| Albers USA | US 48+AK/HI only |
| Albers | Lower 48 |
| Lambert Conformal | Lower 48, World |
| Conic Equidistant | Lower 48, World |
| Mercator | Lower 48, World |
| Transverse Mercator | Lower 48, World |
| Equal Earth | Lower 48, World |
| Natural Earth | Lower 48, World |
| Azimuthal Equal-Area | Lower 48, World |
| Orthographic | Lower 48, World |
| Stereographic | Lower 48, World |

---

## Layer Panel

Up to **6 layers**. Each layer is always fully expanded in the sidebar. Scroll the sidebar to see all layers.

### Layer Card Fields

| Field | Description |
|---|---|
| **Name** | Editable text at the top of the card. Click to rename. |
| **Level** | `STATE` or `COUNTY`. Controls how the data input is parsed and which geography is filled. |
| **Scale** | `Linear`, `Quantile`, or `Quantize`. Controls how values are mapped to the color ramp. |
| **Scheme** | Color ramp preset. See [Color Schemes](#color-schemes) below. Select `Custom` to define your own low and high colors. |
| **Low / High** | Visible only when Scheme is set to `Custom`. Color picker and hex input for each end of the ramp. |
| **Ramp** | Preview of the current color gradient from low to high. |
| **Range** | Manual domain override. Leave both fields blank for auto (min/max of entered values). Set one or both to clamp or extend the scale. |
| **Opacity** | Fill opacity for the layer, 10–100%. |
| **Data** | Paste or type your data. See [Data Format](#data-format) below. |
| **HIDE / SHOW** | Toggles visibility of the layer on the map without deleting the data. |
| **DEL** | Permanently removes the layer. |
| **Status** | Shows matched/failed counts after PLOT DATA is run. |

---

## Data Format

Each line is one record. The value is always the **last comma-separated token**. Lines beginning with `#` or `//` are skipped.

### State Level

```
state_name_or_abbreviation, value
fips, value
```

**Examples:**
```
West Virginia, 45
CA, 88
54, 12
New York, 210
```

Accepted state identifiers:
- Full name: `West Virginia`, `California`
- 2-letter abbreviation: `WV`, `CA`
- 2-digit FIPS (with or without leading zero): `54`, `06`

### County Level

```
county, state, value
fips, value
```

**Examples:**
```
Kanawha, WV, 850
Wood County, West Virginia, 410
54039, 1200
Los Angeles, CA, 3800
Jefferson, Alabama, 520
```

Accepted county identifiers:
- County name + state abbreviation: `Kanawha, WV`
- County name (with or without "County") + full state name: `Wood County, West Virginia`
- 5-digit FIPS: `54039`

The "County", "Parish", "Borough", and similar suffixes are optional and stripped automatically during matching.

---

## Color Schemes

| Scheme | Description |
|---|---|
| Blues | White → dark blue. Sequential, good for single-variable density. |
| Oranges | White → dark orange. |
| Greens | White → dark green. |
| Reds | White → dark red. |
| Purples | White → dark purple. |
| Teal | Light cyan → dark teal (BuGn). |
| Magma | Yellow → black. Perceptually uniform diverging. |
| Viridis | Yellow → dark violet. Perceptually uniform, colorblind-friendly. |
| Red→Green | Red → yellow → green. Diverging; good for positive/negative. |
| Red→Blue | Red → white → blue. Diverging; good for above/below average. |
| Custom | Define your own low and high colors via color picker or hex input. |

### Scale Types

| Type | Behavior |
|---|---|
| Linear | Values mapped proportionally across the color range. Best when data is evenly distributed. |
| Quantile | Breaks data into equal-count buckets (7 classes). Best for skewed distributions — each color represents the same number of features. |
| Quantize | Breaks the domain into equal-width buckets (7 classes). Good for uniform interval classification. |

---

## Legend

When **LEGEND** is checked, an overlay in the lower-left corner of the map shows a gradient bar for each visible layer that has data. The bar spans from the effective domain minimum to maximum, with values labeled at each end. The legend updates automatically when layers are added, hidden, or re-plotted.

---

## Tooltip

Hovering over any filled region displays a tooltip with:
- Layer name (colored to match the layer's high color)
- Geography name (state name or county name)
- The data value for that feature

---

## Sidebar Footer

<table style="border-spacing:6px">
<tr>
  <td><kbd style="background:#21409A;color:#fff;padding:6px 20px;border-radius:5px;font-family:monospace;font-size:12px;border:none;display:inline-block">+ ADD LAYER</kbd></td>
  <td>Adds a new layer card. Maximum 6 layers total.</td>
</tr>
<tr>
  <td><kbd style="background:transparent;color:#c0392b;padding:6px 16px;border-radius:5px;font-family:monospace;font-size:12px;border:1px solid #c0392b;display:inline-block">CLEAR ALL</kbd></td>
  <td>Removes all layers after confirmation. Cannot be undone.</td>
</tr>
</table>

---

## Export

Clicking **EXPORT PNG** captures the current map viewport — including the current pan/zoom position — and saves it as a PNG file. The shorter dimension is always scaled to **2000px**, so a landscape viewport exports at roughly 2000×1200px or wider depending on window proportions.

The **WATER** checkbox controls whether the ocean background color is included in the export. Unchecked produces a transparent/white background suitable for overlaying on other documents.

The **LEGEND** overlay is included in the export if it is visible at time of export.

---

## Technical Notes

- All data processing happens in the browser. No data is sent to any server.
- Geographic boundaries use [`us-atlas`](https://github.com/topojson/us-atlas) (counties-10m) and [`world-atlas`](https://github.com/topojson/world-atlas) via jsDelivr CDN.
- State and county resolution is done entirely client-side via FIPS lookups built from the TopoJSON topology at load time.
- Rendering uses [D3.js v7](https://d3js.org/) and [TopoJSON](https://github.com/topojson/topojson).
- The tool is a single self-contained HTML file with no build step required.
