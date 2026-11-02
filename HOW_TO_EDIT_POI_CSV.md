# How to edit cortes_island_points_of_interest.csv

This file has one row per point of interest (trail, beach, campsite, shop,
etc.) currently in the kiosk. Open it in Excel, Numbers, or Google Sheets
like any spreadsheet. **This is the live data source** — the app reads
this exact file every time it starts, so editing it is how you maintain
the kiosk's points of interest yourself going forward.

## Columns

- **category** — must exactly match one of the 13 category names below
  (spelling and spacing matter). This decides which sidebar section the
  place shows up under. (There's also a special `Welcome` category, used
  only for the two Discover-screen landmark cards — see its own section
  below.)
- **name** — the place's name, as it should appear in the app.
- **latitude / longitude** — the map coordinates. Easiest way to get these:
  right-click the spot on Google Maps and click the coordinates that pop up
  at the top of the menu — it copies them for you.
- **description** — the main text shown on the place's detail screen. If
  you want more than one paragraph, leave a blank line between paragraphs
  (in Excel/Sheets, press Option+Return / Alt+Enter inside the cell for a
  line break).
- **more_details** — optional extra text that's tucked behind a "read
  more" toggle, if you want it. Leave blank if not needed.
- **hours** and **contact** — optional; leave blank if not applicable.
- **photo_file** — the exact file name of the photo for this place (e.g.
  `green-mountain-GMT02400.jpg`), which must already exist in the
  `assets/photos` folder. If you add a new photo, drop the file into
  `assets/photos` first, then type its exact file name here.
- **pin_color** — which color pin marks this spot on the map. Choose one of:
  `red`, `blue`, `dark` (dark teal), `green`, `darkgreen`, `orange`,
  `yellow`, `purple`, `pink`, `teal`, `lightblue`, `brown`, `black`,
  `grey`. Capitals and spaces don't matter (`Light Blue` works). Leave
  blank, or type a color not on this list, and the pin is `dark`.
- **id** — an internal reference code. Leave existing ones alone; for a
  brand-new row you can leave this blank and it'll be generated
  automatically from the name.
- **keywords** — *(added 28 Sept 2026, used only by the Search button)*
  extra words a visitor might type to find this place, separated by
  commas, e.g. `beach, kids, swimming, picnic`. The place's name and
  category are already searchable, so there's no need to repeat them —
  add activities (hiking, biking, kayak), who it suits (kids, family),
  amenities (toilet, wifi, atm) and other names people use for it
  (e.g. `burger barn`). Capitals, apostrophes and word endings don't
  matter ("hiking" also finds "hike"). Leave blank if you like — the
  place just won't come up for anything beyond its name and category.
  Tip: don't add a word to say something is *not* there (e.g. "no
  bikes") — the search would treat that place as a match for "bikes".

## The approved category names

Parks & Trails, Camping & Tenting, Docks & Boat Launches,
Beaches & Water Access, Accommodation, Eating, Groceries & Stores,
Arts & Culture, Playgrounds, Community, Post Offices, Services,
Public Toilets

…plus any new categories added in `cortes_categories.csv` (see
`HOW_TO_EDIT_CATEGORIES_CSV.md`). The name here must match the name
there exactly. If a place's `pin_color` is blank, it uses that
category's default pin colour.

## Adding a new place

Just add a new row at the bottom with the columns filled in. Category
must match one of the names above exactly, or the app won't know where
to put it.

## The two Discover-screen landmark cards (Museum & Archives, Wild Cortes)

The two big cards with owl/mountain icons on the "Discover Cortes" home
screen — separate from the regular map/category screens — are also driven
by this CSV. They're the two rows near the bottom with `Welcome` as their
category:

- one has **id** `landmark-museum` (the Museum & Archives card)
- one has **id** `landmark-wildcortes` (the Wild Cortes card)

Edit their `name`, `latitude`/`longitude`, `description`, `more_details`,
`hours`, `contact` and `photo_file` columns exactly like any other row —
same rules apply (photo must already exist in `assets/photos`, blank line
between paragraphs, etc.). `pin_color` is ignored for these two rows since
they don't show a map pin like ordinary places do.

**Don't change the `id` on these two rows, and don't add other `Welcome`
rows** — the app only recognizes those two exact id values for the
landmark cards; anything else tagged `Welcome` is ignored (it won't show
up as a category either, since `Welcome` isn't one of the 13 above).

If you ever delete or badly mangle one of these two rows, that landmark
card just falls back to its original built-in text/photo — it won't
break the app.

## One thing already spotted

"Hank's Beach" (it appears twice — once under Parks & Trails, once under
Beaches & Water Access) doesn't currently have a matching photo file, so
it's showing a placeholder in the app right now. Add a photo for it
whenever you have one and fill in its file name in both rows.

## Getting your changes into the app

**The app reads this file directly, every time it starts.** There's no
extra step and nothing to send back to Claude — save your changes to
`cortes_island_points_of_interest.csv` (keep the file name exactly as-is,
in the same folder as `cortes_kiosk_prototype.html`), then reload or
relaunch the app and your edits are live.

One important rule: **always open the app through `launch_kiosk.bat`**
(Windows) or **`test_on_mac.command`** (Mac) — never by double-clicking
`cortes_kiosk_prototype.html` directly. Reading this CSV file requires
the app to be running from a real web address (`http://localhost:...`),
which only the launcher scripts set up. Opening the HTML file directly
will fail to load your points of interest at all (map, categories, and
buttons will still work, but everything will look empty). This is the
same reason the map-tile fix a few days ago required using the launcher
— see `README_kiosk_setup.md` for the full explanation.

**If you typo a category name:** that row is silently skipped — the
place just won't show up anywhere, with no error message on screen. If
something you added doesn't appear, double-check its `category` value
matches one of the 13 names above exactly (capitalization and spacing
included) — or is exactly `Welcome` if it's meant to be one of the two
landmark cards. If you want to confirm what happened, you can check the
browser's developer console (in Chrome/Edge: right-click the page →
Inspect → Console tab) — it lists any category names it didn't
recognize.
