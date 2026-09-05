# JOH Room Tracker — Mobile Site Setup (GitHub Sync)

## What this gives you
- Every engineer opens **one web link** on their phone.
- Works **fully offline** in the field.
- The moment any phone gets internet, its edits **sync automatically** to GitHub.
- Everyone sees everyone's updates (progress %, room-info edits, site notes, photos/voice/video).
- Excel files are regenerated on demand with the **Update Excel Files** button.

---

## PART A — Publish the app once (you, on a computer or phone browser)

1. Go to your GitHub repo **fadeelhusin/joh-rooms-tracker**.
2. Upload ALL files from this folder (drag-drop in the web UI, or `git push`).
3. Make it public + turn on Pages:
   - **Settings → General → Danger Zone → Change visibility → Public**
   - **Settings → Pages → Source: `main` branch → /(root) → Save**
4. After ~1 minute your link is live:
   **https://fadeelhusin.github.io/joh-rooms-tracker/**

---

## PART B — Create ONE GitHub token (shared by the team, or one each)

1. GitHub → **Settings → Developer settings → Personal access tokens → Fine-grained tokens → Generate new**.
2. **Repository access:** Only select repositories → **joh-rooms-tracker**.
3. **Permissions → Repository → Contents: Read and write** (nothing else).
4. Generate, copy the `ghp_…` token.

> One token can be shared with all site engineers, OR give each engineer their own — both work. Merge is safe: edits never overwrite each other.

---

## PART C — Each engineer, once, on their phone

1. Open **https://fadeelhusin.github.io/joh-rooms-tracker/**
2. (Optional) **Add to Home Screen** so it opens like an app:
   - iPhone Safari: Share → Add to Home Screen
   - Android Chrome: ⋮ → Add to Home screen
3. Tap **⚙️ Set up sync** (top left).
4. Paste the **token**, confirm Owner `fadeelhusin`, Repo `joh-rooms-tracker`, Branch `main`.
5. Type **your name** (tags your notes & edits).
6. **Save & sync.**

Done. From now on: work offline all day → whenever there's signal, it syncs by itself. The pill at the top shows **✅ Synced / ⏳ pending / 📴 Offline**.

---

## Daily use
- **Plan tab** → tap a room dot → edit **Site Progress**, **Room Info**, **Site Notes** (voice/video/photo/files).
- Notes & media are saved on the phone and uploaded to `tracker-data/files/` on sync.
- Tap **💾 Update Excel Files** anytime to download the two updated spreadsheets for reporting.

## Where the data lives on GitHub
```
joh-rooms-tracker/
  tracker-data/
    progress.json      ← site progress %
    roominfo.json      ← room-info edits
    notes.json         ← site notes
    clearance.json     ← clearance ticks
    rfis.json, docs.json
    files/             ← photos, voice, video, uploaded files
```
