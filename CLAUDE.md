# Peel Paint Party — Project Brief for Claude Code

This file tells Claude Code what this project is, what has been decided, and what has already been built. Read it fully before making changes.

## Who I am and how to work with me

I'm Katie, a University of Arkansas student building this for my class Digital Infrastructure and Innovation, on a team of two. I'm a beginner at coding and git. I want to learn the plumbing, not just get working code, so:

- Explain each file you create and why it exists, in plain language.
- Explain any git command before running it.
- Commit small and often with clear messages. Commit history is part of my graded evidence.
- Never commit API keys. Keys go in `.env`, and `.env` must be in `.gitignore`.

## The product

Peel Paint Party is a web app for designing hand-painted gifts like pong tables, coolers, and cornhole boards. Users lay out photos, colors, and text on a true-to-scale template, then turn the design into black-and-white outlines to trace and paint.

The core insight: the painting is the fun, meaningful part of a handmade gift. The week of prep before it (finding images, tracing onto tissue paper, projecting, outlining) is the chore. The app automates the setup, not the craft. The person still chooses the design and paints it by hand.

Audiences: students making gifts (formal, birthdays), paint-and-sip and girls'-night groups, parents doing family projects like Father's Day.

Long-term vision (not in this build): order a print-on-demand, peel-and-stick, temporary-tattoo-style stencil, cut to exact dimensions, shipped rolled in a tube, possibly with paint-by-number color labels. Estimated price $60–70 per pong table kit. For comparison, a DIY build runs about $150 in materials, and a commissioned custom table costs $200–400.

## Class deliverable scope (due December 4, 2026)

Smallest viable version: one object, the standard pong table, done well.

- In scope: photo upload, background removal, line-art conversion, true-dimension pong table canvas, arranging designs, outline view, and eventually a tiled print-at-home PDF.
- Out of scope for the class: coolers, cornhole boards, print-on-demand, payments, shipping, a searchable art library.

Success criteria:

1. At least 7 of 10 test photos produce paintable line art.
2. Printed stencils measure within ⅛ inch of real table dimensions.
3. Design-to-transfer takes far less time than tissue-paper tracing.
4. At least 3 of 5 testers finish a full design without help in under 30 minutes.
5. At least 3 of 5 testers say they'd pay $60–70 for a printed kit.

Timeline:

- Oct 12–16: scope plan
- Oct 19–30: build the halves
- Nov 2–6: connect them
- Nov 9–13: PDF export and real-board test
- Nov 16–20: user testing
- Nov 23–27: Thanksgiving buffer
- Nov 30–Dec 4: polish and present

## Ethics and legal decisions (do not change without asking me)

- Uploads stay private. Never build a searchable gallery of user uploads. User photos are processed in the browser and never leave the device.
- Neutral print-service model. We act like a print shop. Terms of service put rights responsibility on the uploader.
- Never market the app as a way to use Pinterest or other people's art. Encourage personal photos (pets, places, people).
- Any built-in art library must be art we own or have written permission to use.

## What's already built

The current prototype is a single self-contained file, `index.html` (HTML, CSS, and vanilla JS, no build step). It works in any browser.

### Canvas

- The pong table is 96 × 24 inches (8 ft × 2 ft), drawn on a green "cutting mat" background with foot rulers along the top and left edges.
- All geometry is stored in inches. A pixels-per-inch value (`ppi`) is recomputed whenever the window resizes.
- Cup circles: 10-cup triangles at each end. Rows of 4, 3, 2, 1 with radius 1.85 in. Row x-centers start at 2.6 in from each end, stepping 3.2 in toward the middle. Row y-offsets from center (y = 12):
  - 4-row: ±1.85, ±5.55
  - 3-row: 0, ±3.7
  - 2-row: ±1.85
  - 1-row: 0

  The right end mirrors the left (x → 96 − x). A "Show cups" toggle controls visibility.

### Layouts

A picker in the panel offers Style 1–6 plus Freeform. Each layout remembers its own colors, photos, and text when you switch away and back.

### Section geometry

All polygons use (x, y) in inches, origin at the top-left. Sections are numbered in list order.

**Style 1 (7 sections):**

1. (0,0) (24,12) (0,24)
2. (0,0) (48,0) (24,12)
3. (0,24) (24,12) (48,24)
4. (48,0) (72,12) (48,24) (24,12) — the center diamond
5. (48,0) (96,0) (72,12)
6. (48,24) (72,12) (96,24)
7. (96,0) (72,12) (96,24)

**Style 2 (10 sections):**

1. (0,0) (28,12) (0,24)
2. (0,0) (28,0) (28,12)
3. (0,24) (28,12) (28,24)
4. (28,0) (48,12) (28,24)
5. (28,0) (68,0) (48,12)
6. (28,24) (48,12) (68,24)
7. (68,0) (68,24) (48,12)
8. (68,0) (96,0) (68,12)
9. (68,24) (68,12) (96,24)
10. (96,0) (68,12) (96,24)

**Style 3 (11 sections):**

1. (0,0) (24,12) (0,24)
2. (0,0) (24,0) (24,12)
3. (0,24) (24,12) (24,24)
4. (24,0) (48,0) (24,12)
5. (24,24) (24,12) (48,24)
6. (24,12) (48,0) (72,12) (48,24) — the center diamond
7. (48,0) (72,0) (72,12)
8. (48,24) (72,12) (72,24)
9. (72,0) (96,0) (72,12)
10. (72,24) (72,12) (96,24)
11. (96,0) (72,12) (96,24)

**Style 4 (18 sections):** same as Style 3, except the center diamond is split into 8 vertical stripes.

- Sections 1–5: same as Style 3's sections 1–5.
- Sections 6–9 (left half-diamond, x 24→48): stripes at x = 24|30|36|42|48. Edges: top y = 12 − (x − 24)/2, bottom y = 12 + (x − 24)/2.
- Sections 10–13 (right half-diamond, x 48→72): stripes at x = 48|54|60|66|72. Edges: top y = (x − 48)/2, bottom y = 24 − (x − 48)/2.
- Sections 14–18: same as Style 3's sections 7–11.

**Style 5 (17 sections):**

1. (0,2.5) (28,12) (0,20.8)
2. (0,0) (14.2,0) (14.2,7.3) (0,2.5)
3. (14.2,0) (28,0) (28,12) (14.2,7.3)
4. (0,20.8) (13.2,16.65) (28,24) (0,24)
5. (13.2,16.65) (28,12) (28,24)
6. (28,0) (48,0) (48,2.4) (32.8,12) (28,12)
7. (48,0) (57.9,0) (57.9,8.57) (48,2.4)
8. (57.9,0) (67.4,0) (67.4,12) (63.4,12) (57.9,8.57)
9. (32.8,12) (48,2.4) (63.4,12) (48,20.8) — the center diamond
10. (28,12) (32.8,12) (38.6,15.36) (38.6,24) (28,24)
11. (38.6,15.36) (48,20.8) (48,24) (38.6,24)
12. (48,20.8) (63.4,12) (67.4,12) (67.4,24) (48,24)
13. (67.4,3.1) (81.8,7.07) (67.4,12)
14. (67.4,0) (96,0) (96,2.2) (81.8,7.07) (67.4,3.1)
15. (67.4,12) (80.6,16.06) (80.6,24) (67.4,24)
16. (80.6,16.06) (96,20.8) (96,24) (80.6,24)
17. (67.4,12) (96,2.2) (96,20.8)

**Style 6 (9 sections):** Style 1 plus a bullseye. Sections are stacked, so later sections draw on top of earlier ones.

- Sections 1–7: same as Style 1.
- Section 8: circle at (48,12), radius 9.8.
- Section 9: circle at (48,12), radius 4.9.
- Label positions are custom: section 4 at (31.5,12), section 8 at (48,4.6).

### Features of each section (in the Style layouts)

- Click to select. Selecting shows the section panel. A dashed blue outline marks the selected section.
- Background color: a 12-swatch palette taken from Katie's hand-painted table, plus a custom color picker and a "no color" option. Palette: `#A99BF0 #4FC3F7 #1E5BD8 #F8A23B #FAD54A #E2CFA8 #BDBDBD #D32F2F #F4A7C6 #3BB273 #161616 #FFFFFF`.
- Photo: add one by clicking "Add photo" or by dragging a file onto the section. The photo fills the section and is clipped to its shape. Controls:
  - Drag to reposition. Panning is clamped so the photo never leaves a gap.
  - Zoom from 0.3× to 3×.
  - Rotation slider plus a "Turn 90°" button.
  - "Remove plain background" with a sensitivity slider, so the section color shows around a graphic.
  - Line detail slider for the outline view.
  - Replace and Remove buttons.
- Text: multi-line text with a choice of 5 fonts, size, rotation, and color. Drag to move the text. If a section has both a photo and text, a "Dragging moves: Photo / Text" switch picks which one moves.
- Line thickness slider (0.1–1.5 in, default 0.45) for the black section lines.

### Cup circles

- "Fill circles with color" (palette swatches). When off, the circles show as dashed blue guides.
- Text over each end, in separate left and right boxes. It's automatically rotated to face the player at that end: left end `rotate(90)`, right end `rotate(-90)`. The text is centered 7.4 in from each end.
- Font, size, and text color controls.

### Freeform layout and extra photos

- Photos can be placed anywhere: drag to move, use the corner handle to resize, plus width and rotation sliders and Turn 90°. Also remove background, line detail, bring forward/send back, center, and delete. Arrow keys nudge (Shift for bigger steps), and Delete removes.
- In the Style layouts, these photos act as "extra photos on top."

### Outline view

A "Turn all photos into outlines" button and a Color / Outlines toggle in the header. In outline view:

- Photos become black line art.
- Section colors become white.
- Cup circles become black rings.
- All text becomes hollow letters with a white fill and black stroke.

### Image processing (all in the browser, no server)

- Photos are downscaled to a maximum of 1100 px on the long side.
- Background removal: flood-fill from all border pixels. Pixels within an RGB distance tolerance of the average corner color, and connected to the border, become transparent. This works on plain or light backdrops. A real AI model (remove.bg API or the open-source BRIA RMBG) is the planned upgrade.
- Line art: grayscale (transparent counts as white), then a 3×3 box blur, then Sobel edge magnitude. Threshold = `20 + (100 − detail) × 2`. Edge pixels are black, opaque non-edge pixels are white (so upper layers hide lower ones), and transparent pixels stay transparent. A known weakness: two colors with similar brightness may not produce an edge.

### Design system

- Theme: cutting mat green (`#2D5A4B`) with a grid, a "painter's tape" blue accent (`#5A9BE0`) on a torn-tape logo, and primer white for the table (`#FDFDFB`).
- Fonts: Bricolage Grotesque for the UI and Permanent Marker for the logo. Lettering fonts: Titan One (bubble, the closest to Katie's hand lettering), Bungee, Rubik Mono One, Permanent Marker, and Bricolage Grotesque.
- Supports both light and dark mode, and is responsive (the panel stacks under the canvas on narrow screens).

## Next steps (in priority order)

1. Tiled PDF export: print the outline design at true size across letter pages (about 39 pages for the full table), with alignment marks and page numbers so the pages can be taped together.
2. Paint-by-number labels: number each colored region in the outline export, with a color key.
3. Better background removal and line art: swap in an AI model. Keep keys in `.env`.
4. Save and load designs so work isn't lost on refresh.
5. More objects: cornhole boards, then coolers (side panels and lid; the wrap and stretch around rounded corners needs physical testing).
6. Later: print-on-demand ordering.

## Testing and evidence

- Test with real photos: pets, houses, logos, people.
- Save dated screenshots and screen recordings of key milestones. Commit history serves as the dated record of who built what.
- Log significant AI use (what was asked, what came back, what was kept) in the team journal.
