# Modillion Field Report (iPad app)

A web app that runs in Safari on the iPad, installs to the home screen like a
native app, works offline, takes the photos with the iPad camera, and builds
the Word report on the iPad itself. No App Store, no Mac, no developer
account. It is one HTML file plus a few small support files.

Files:

    index.html            the whole app (all code is inside)
    sw.js                 offline cache (service worker)
    manifest.webmanifest  home-screen app definition
    icon-180.png / icon-192.png / icon-512.png

## 1. Put it on a web address (once, ~5 minutes)

The app has to be opened from an https:// address for "Add to Home Screen"
and offline mode to work. Easiest free option is GitHub Pages:

1. Create a GitHub repository (private is fine if the whole team is in the
   org; otherwise public - the app contains no data, all photos stay on the
   iPad).
2. Upload the files from this folder to the repository root.
3. Repository *Settings > Pages > Source: Deploy from a branch*, branch
   `main`, folder `/ (root)`. Save.
4. After a minute the app is live at
   `https://<your-user-or-org>.github.io/<repository>/`.

Any other static host works the same way (Netlify Drop, Cloudflare Pages,
an internal web server, SharePoint's "Pages" does NOT work).

**Quick test on the same Wi-Fi without any hosting:** on a PC in this folder
run `python -m http.server 8000`, then open `http://<PC IP>:8000/` on the
iPad. Camera and report generation work; only "Add to Home Screen"/offline
need the https address.

## 2. Install on each iPad (once)

1. Open the address in **Safari** (not Chrome/Edge).
2. Tap the Share button, then **Add to Home Screen**, then **Add**.
3. Launch it from the home-screen icon from now on. The first launch caches
   the app; after that it runs with no internet at all.

Each iPad keeps its own project and photos (they never leave the device
unless you export). Storage is generous - a full 300-modillion report is well
under 500 MB - but iOS can clear website data if the app is not opened for a
long time, so **export a project zip at the end of each shift** (Report tab).

## 3. Using it

**Capture tab** - the screen you live on:

* Type the **Zone** and **Modillion #** once. **Next** keeps the zone and
  increments the number; only change the zone when you move to a new one.
* Tap the **Left / Front / Right** tile - the camera opens, take the photo,
  done. Tap again to retake. The small buttons on a tile: rotate 90 degrees,
  choose from the photo library instead, remove.
* **Pick photos from library (in order)** - select photos in the Photos
  picker in the order Left, Front, Right (the tile order); the first three
  fill this modillion, every further three become the next modillion with the
  number incremented. Handy if you prefer shooting with the Camera app (which
  also leaves copies in the camera roll): shoot a run of modillions, then
  select them all at once.
* Tap **quick-pick defect** chips - the standard sentence is added to the
  notes and the defect is tagged for the summary table. Tap again to remove.
  Then add anything specific in the notes (the keyboard's microphone dictates
  well for this).
* **Comments** = the bottom area of the page: optional text and extra photos
  with captions (they get A), B)... and their own figure numbers).
* **Prev / Next** to move; **Delete** removes the current modillion.

**List tab** - every modillion by zone with its three thumbnails; red text if
photos are missing, and duplicate labels are called out at the top. Tap one
to jump to it.

**Zones tab** - the intro sentence and optional elevation drawing (camera or
library) for each zone's heading page.

**Report tab**

* **Generate Word document** - whole report or one zone. The file is built on
  the iPad (about 200 KB per photo at the default settings; a 100-modillion
  zone is ~60 MB and takes a minute or two).
* **Share / Save to Files** opens the iOS share sheet. Choose *Save to Files*
  and then *On My iPad* (instant, local) or *OneDrive*, or send by Mail /
  Teams. **Download** puts it in Files > Downloads. If OneDrive is slow,
  save locally first and move it later.
* **Export project zip** - all photos + `project.json`. This is your backup
  and the hand-off to the office: the desktop *Modillion Report Builder* opens
  the zip directly (Open Project > choose the .zip).
* **Import zip (merge)** - append another iPad's export into this one, so
  several people can shoot different zones and one iPad (or the desktop
  tool) assembles the full report.

**Settings tab** - footer text, section number, first figure / page number,
element name, the order of the capture tiles on screen (`LFR` by default:
Left, Front, Right - the report layout itself always matches the reference
report), photo sizes, and the quick-pick defect list (one per line:
`Label | sentence`). Press *Save settings*.

## What can go wrong, and what the app does about it

* **Battery dies / app closed / Safari glitches** - nothing is lost. Every
  photo is written to the iPad's storage before the tile even updates, and
  text is saved within a fraction of a second. Reopen the app and you are on
  the same modillion.
* **The iPad is the only copy** - photos taken in the app do NOT go to the
  camera roll. Until you export, they exist only inside the app on that iPad.
  The line under the Next button shows when the last export was; export a project zip from the Report tab at the end of every shift,
  and save it somewhere off the device (OneDrive, Mail, a laptop).
* **Two people on two iPads** - give each person whole zones. Set *Your name
  or initials* in Settings on each iPad: exports are then named like
  `USHMM_Z1_M1-39_Z2_M1-12_Dave_2026-09-12_0230.zip` - the zones and
  modillion ranges inside, who exported it, and when (no two iPads produce the
  same file name). Word files are named the same way without the name/time.
  With no internet, **AirDrop** the zip from one iPad to the other (share
  sheet > AirDrop), then Import it and each modillion records who captured it. Combine either by
  importing one zip into the other iPad (Report > Import zip) or in the
  office with the desktop tool's *Merge...* button. If both people shot the
  same modillion number, the import asks whether to skip those or keep both.
* **Wrong numbers** - if two modillions on an iPad end up with the same
  zone/number, a yellow warning appears on the capture screen and the List
  tab names them. Modillions are sorted by zone and number when the report is
  generated, so a missed one photographed later still lands in the right
  place.
* **Accidental erase** - *Start a new project* requires typing ERASE.
  *Delete* and photo *Remove* ask first.
* **Storage** - a shift's worth of photos is a few hundred MB; the Report tab
  shows usage and warns above 80 %. Do not use Safari's "Clear History and
  Website Data" on the iPad - that erases the app's photos.
* **Address change** - the app's data is tied to its web address. If the
  hosting URL ever changes, export from the old address before switching.
* **Generating the report** takes a minute or two; keep the app on screen
  (iOS pauses it in the background).

## Tips for the night shift

* **Dark mode** (Settings) for the night shift.

* The camera tile uses the rear camera at full resolution; photos are
  downscaled to 1600 px on the long edge when saved (plenty for a 3-inch
  print) which keeps the iPad fast and the report small.
* Rotate the iPad however is comfortable - the layout adapts.
* Everything is saved instantly; there is no Save button.
* If Safari ever shows the plain website instead of the app, you opened the
  address instead of the home-screen icon; both use the same data.

## Updating the app

Replace the files on the web host. Installed iPads pick the new version up
on the next launch with internet (the old version keeps working offline
until then). Bump `VERSION` in `sw.js` when you change files so the cache
refreshes.
