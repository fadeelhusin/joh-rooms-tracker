# JOH Room Tracker — v0.5

Room identity, location, finishing schedule, element code libraries, a
handover Clearance Status checklist, room documents (shop drawings /
material approvals / TQs), and site issues (RFIs) for Jeddah Opera House
(S4-01-056). English-only UI. Works fully offline; syncs to a shared
GitHub repo automatically whenever the device is online.

## Deploying a code update (GitHub Desktop)

1. Copy every file/folder from this package into your cloned repo folder
   (e.g. `Desktop/opera-finishing`), replacing files with the same name.
2. Open GitHub Desktop — it lists the changed files automatically.
3. Type a short summary, click **Commit to main**, then **Push origin**.
4. The live site updates within about a minute.

## Setting up sync (once per device)

Tap the pill in the header ("⚙️ Set up sync"), paste a fine-grained GitHub
token scoped to just this repo with **Contents: Read and write**, confirm
the repo owner/name, and save. See the in-app hint text for details.

## What's new in this version

- **Clearance Status** — a per-room handover checklist (MEP closed,
  waterproofing tested, shop drawing approved, snagging closed, etc.).
  Each item is a checkbox; check it and optionally record who checked it.
  Any item can carry **evidence** — one or more photos/PDFs and/or links
  (Drive, SharePoint, anything) proving that item is cleared. The default
  10-item checklist is in `clearance.js` (`CLEARANCE_ITEMS`) — ask to
  add/remove/rename items any time, it's a one-line change per item.
- **Multiple files and links everywhere** — Documents (shop drawing /
  material approval / TQ), RFI responses, and Clearance evidence all now
  accept as many files as needed in one go (camera or upload), plus any
  number of links pasted in directly. Previously these accepted one file
  each; existing single-file records still display correctly.
- **Room Schedule parsing fixes** — sheets with a separate Code column
  plus a separate plain-name column (e.g. "Floor Code" + "Floor Finish")
  now parse correctly; skirting has its own code library, separate from
  floor codes; a handful of noisy duplicate columns (No., Room Name,
  Level, Area, # Parts) are skipped instead of cluttering the room page.

## What syncs, and how

- **RFIs**, **Documents**, and **Clearance Status**: each entry/item has
  its own id, so entries from different devices simply add up; the later
  edit wins on conflicts.
- **Room Schedule** and **Item Library**: each upload is bulk, so the
  most recently *uploaded* file wins as a whole, per category.
- **File attachments** (photos, PDFs) sync too, stored under
  `tracker-data/files/` in the repo.
- Sync runs automatically moments after any change (if online), the
  instant the device regains a connection, and every 2 minutes as a
  safety net while online.
- **Known limitation:** deleting an RFI, a document, or a clearance
  attachment on one device won't remove it from other devices that
  already synced it earlier. Prefer marking an RFI "closed" over deleting.

## What's inside

- index.html / app.js / viewer.js / styles.css — the app shell
- rfi.js — RFIs (issue type, description, priority, photos, responses)
- docs.js — room documents (shop drawings / material approvals / TQs)
- clearance.js — handover Clearance Status checklist
- library.js — per-category code schedules (walls/ceilings/floors/
  skirting/doors/furniture/other), cross-referenced against room codes
- files.js — IndexedDB-backed storage for attached PDFs/photos
- schedule.js — Room Schedule upload (door type, finishes, furniture codes)
- sync.js — GitHub-backed sync engine
- vendor/xlsx.full.min.js — SheetJS, reads xlsx/xls/csv fully offline
- data.js — 988 rooms (identity + plan position), embedded for offline use
- png/*.png — color scope plans (blue=ZAK, green=MBL Marine, red=BAUMAT;
  theatre halls & stages stay ICONIC), rasterized at 300 DPI from the IFC PDFs
- Source: Rev F00 IFC 31-01-2024 architect plans
