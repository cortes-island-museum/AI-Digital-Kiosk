OPENING SCREEN PICTURE
======================

This folder holds the picture shown on the kiosk's opening screen
("Welcome to Cortes Island - Touch anywhere to begin").

It is separate from the kayakers photo on the "About Cortes Island" screen,
so you can change one without affecting the other.

TO CHANGE THE PICTURE
  1. Put your picture in this folder and name it:  opening-image
     with its usual ending: .jpg, .jpeg, .png or .webp
     (for example opening-image.jpg)
  2. Keep only ONE file named opening-image here. If there are several,
     the kiosk uses .jpg first, then .jpeg, then .png, then .webp.
     Rename the ones you want to keep, e.g. opening-image-map-old.png.
  3. Refresh / restart the kiosk.

  If no opening-image file is found, the kiosk falls back to
  assets/photos/kayaking.jpg.

Right now opening-image.png is a copy of the island map
(assets/maps/cortes-map-background.png).

MAP OR PHOTO? - HOW IT FILLS THE SCREEN
  In cortes_kiosk_prototype.html, near the top, in the
  "KIOSK LAYOUT SETTINGS (safe to edit)" section:

    --opening-image-fit: contain;
        contain = show the whole picture (best for a map)
        cover   = fill the whole screen, cropping edges (best for a photo)

    --opening-image-position: center top;
        for a photo with "cover", center 62% is what the kayakers used

    --opening-image-background: #F6F3EA;
        colour around the picture when using "contain"

  To go back to the kayakers photo exactly as before: rename
  opening-image.png (e.g. to opening-image-map.png) and set
      --opening-image-fit: cover;
      --opening-image-position: center 62%;
