# Peel Paint Party

Peel Paint Party is a web app for designing hand-painted gifts, starting with a
standard 8 ft × 2 ft (96 × 24 in) pong table. You lay out photos, colors, and
text on a true-to-scale template, then turn the whole design into black-and-white
outlines you can trace and paint by hand. The painting is the fun, meaningful part
of a handmade gift; the hours of prep before it (finding images, tracing onto tissue
paper, projecting, outlining) are the chore. Peel Paint Party automates the setup,
not the craft. All photo processing happens in your browser, so your photos never
leave your device.

## Current features

- **Six section layouts (Styles 1–6)**, each remembering its own colors, photos, and text
- **Freeform photo placement**: put photos anywhere on the table, resize, rotate, and layer them
- **Section background colors** from a 12-color palette, plus a custom color picker
- **Photos with background removal** that clear plain backdrops so the section color shows through
- **Zoom, rotate, and reposition** photos inside each section
- **Text in sections and over the cup circles**, with five fonts (Titan One, Bungee,
  Rubik Mono One, Permanent Marker, Bricolage Grotesque)
- **Adjustable line thickness and color** for the section lines (lines stay black in outline view)
- **Reshape sections** by dragging their corner points; neighboring sections move with them
- **Remove sections** you don't want (like the small inner circle in Style 6), and restore them anytime
- **Cup circle color** picker, or dashed guide circles if you pick no color
- **"Turn all photos into outlines"** button that converts everything into
  black-and-white paintable outlines

## How to run it

The whole app is a single HTML file with no build step and no install.

1. Download or clone this repository.
2. Double-click `index.html` to open it in any modern browser (Chrome, Safari,
   Firefox, or Edge).

An internet connection is only needed to load the Google Fonts.

## Next steps

- **Tiled PDF print export**: print the outline design at true size across letter
  pages, with alignment marks and page numbers so the pages can be taped together
- **Paint-by-number color labels**: number each colored region, with a color key
- **More object types**: coolers and cornhole boards
