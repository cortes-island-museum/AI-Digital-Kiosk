# How to edit cortes_categories.csv

This file has one row per **category** (Parks & Trails, Camping & Tenting,
Post Offices, etc.) plus one row for the "About Cortes Island" welcome
screen. Open it in Excel, Numbers, or Google Sheets like any spreadsheet.
**This is the live data source for category descriptions and category
photos** — the app reads this file every time it starts, the same way it
already reads `cortes_island_points_of_interest.csv` for individual
places. This is the "place for descriptions" that didn't exist before —
now it does.

## Columns

- **category** — the category's name, exactly as it should appear on its
  button. The 13 existing names are listed below, plus "About Cortes
  Island" for the welcome screen. **A name that isn't on that list
  creates a new category** (see "Adding a new category" below).
- **description** — the paragraph(s) shown at the top of that category's
  overview screen (or, for "About Cortes Island", on the welcome/info
  screen). For more than one paragraph, leave a blank line between them
  (in Excel/Sheets, press Option+Return / Alt+Enter inside the cell for a
  line break, then a second one for a blank line).
- **photo_file** — the exact file name of the photo shown at the top of
  that category's screen (e.g. `c-campgrounds.jpg`), which must already
  exist in the `assets/photos` folder. If you add a new photo, drop the
  file into `assets/photos` first, then type its exact file name here.
  Leave blank to keep the plain icon instead of a photo.
- **icon_file** — *(optional)* the file name of the small icon on the
  category's button, e.g. `farm.png`. The file goes in the `assets/icons`
  folder. Leave blank to keep the current icon (a new category without an
  icon gets a simple four-square icon).
- **pin_color** — *(optional)* the default pin colour on this category's
  map, used for any place whose own `pin_color` is blank in the
  points-of-interest CSV. Same colour names as there (red, blue, dark,
  green, darkgreen, orange, yellow, purple, pink, teal, lightblue, brown,
  black, grey).

## Button order

The category buttons appear in the **same order as the rows in this
file**. To move a category up or down the list, move its row.

## Adding a new category

1. Add a new row at the position where you want the button to appear.
   Type the new name in `category`, plus a `description` and
   `photo_file` like any other row.
2. *(Optional)* put an icon in `assets/icons` and type its file name in
   `icon_file`. For the best result use a **transparent PNG (or SVG),
   square, about 96×96 px, with a dark single-colour symbol**. The app
   turns it white automatically when the button is selected.
3. *(Optional)* pick a `pin_color` for its map pins.
4. In `cortes_island_points_of_interest.csv`, add the places for this
   category and type the **same name, spelled exactly the same** in their
   `category` column.
5. Reload the app. The new button appears in the right-hand column, and
   the other buttons get a little smaller if needed to fit.

There's room for up to 18 categories, so the buttons stay big enough to
tap comfortably.

To **remove** a new category, delete its row. The 13 built-in categories
stay in the column even if their row is deleted.

## The existing category names

About Cortes Island, Parks & Trails, Camping & Tenting,
Docks & Boat Launches, Beaches & Water Access, Accommodation, Eating,
Groceries & Stores, Arts & Culture, Playgrounds, Community, Post Offices,
Services, Public Toilets

(Plus any new categories you've added. These must match exactly the names used in
`cortes_island_points_of_interest.csv` — see
`HOW_TO_EDIT_POI_CSV.md` — plus "About Cortes Island" for the welcome
screen.)

## Getting your changes into the app

**The app reads this file directly, every time it starts** — same as the
points-of-interest CSV. Save your changes to `cortes_categories.csv`
(keep the file name exactly as-is, in the same folder as
`cortes_kiosk_prototype.html`), then reload or relaunch the app and your
edits are live. Always open the app through `launch_kiosk.bat` /
`test_on_mac.command`, never by double-clicking the HTML file directly —
same reason as the points-of-interest CSV (see
`HOW_TO_EDIT_POI_CSV.md`).

**If you typo an existing category name:** the app will treat it as a
new category, and you'll see an extra button with that misspelled name.
Just fix the spelling in the CSV and reload. Check the browser's developer console (Chrome/Edge: right-click
the page → Inspect → Console tab) if something doesn't seem to have
taken effect — it lists any new categories it added.

**If a category has no row here** (or the file fails to load), it just
falls back to a generic placeholder description and the plain icon — the
app won't crash or show anything broken.

## About photos — one less thing to worry about now

Previously, a photo you dropped into `assets/photos` (for a place or for
a category) wouldn't actually show up in the app unless Claude also
added its exact file name to a hidden internal list and rebuilt the
file — that was the bug behind photos showing a placeholder with the
right name printed on it. That's fixed: the app now just tries to load
whatever file name you typed (guessing `.jpg`/`.jpeg`/`.png`/`.webp` if
you left the extension off), and only shows a placeholder if the file
genuinely isn't there. Dropping the file into `assets/photos` and typing
its name in the CSV is the whole process now, for both this file and
`cortes_island_points_of_interest.csv`.
