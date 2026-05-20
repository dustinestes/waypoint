<br><br>
<img align="right" src="../branding/icons/waypoint_standalonemark_lightbg.png" height="44" alt="waypoint">
<h1>Dashboard Guide</h1>
<br clear="both">

A reference for all dashboard features — loading files, tracking progress, editing statuses, managing session state, and customizing themes.

<br>

## Opening the Dashboard

Open `dashboard.html` directly in any modern browser. No server or build step is required. An internet connection is currently needed to load fonts, icons, and the YAML parser from CDN.

### Loading a YAML file

There are three ways to load your learning file into the dashboard:

| Method | When to use |
|--------|-------------|
| **Auto-load** | When `dashboard.html` and your YAML file are in the same directory and served via a local server or GitHub Pages |
| **File picker** | Click **Load YAML** in the navbar to browse for any YAML file |
| **Drag and drop** | Drag any YAML file directly onto the drop zone on the upload screen |

### File naming

The file picker and drag-and-drop methods accept **any filename** — `kubernetes.yaml`, `aws-prep.yaml`, `my-learning.yaml`, or anything else. The dashboard reads whatever you give it and preserves the original filename when you save.

Auto-load is currently hardcoded to look for `waypoint.yaml` in the same directory. If you serve a differently-named file via GitHub Pages or a local server, it won't auto-load — use the file picker or drag-and-drop instead.

> **Planned:** a config block in `dashboard.html` will allow the auto-load filename to be customized. See [GitHub issue #5](https://github.com/dustinestes/waypoint/issues/5).

---

## Dashboard Layout

### Navbar

The navbar runs across the top of the page and contains all primary controls:

- **waypoint logo** — click to return to the project GitHub page
- **File status indicator** — a pill showing the loaded filename with a teal dot, or "No file loaded" with a gray dot
- **Unsaved changes indicator** — an amber pill that appears when you have edits not yet saved
- **Download button** — hidden until a file is loaded; gray when clean, turns teal when unsaved changes exist
- **Theme picker** — palette icon opens a popover with named theme swatches
- **Load YAML button** — opens the file picker to load or switch files

### Summary Bar

Displayed at the top of the dashboard. Shows aggregate counts across all subjects:

| Stat | Color accent | Notes |
|------|-------------|-------|
| Total | — | All modules across all subjects |
| Complete | Amber | Modules marked `complete` |
| In progress | Teal | Modules marked `in_progress` |
| Not started | — | Modules marked `not_started` |
| Skipped | Violet | Modules marked `skipped` |

Below the stat cards, an **Overall Progress** bar shows completion as a percentage. Progress is calculated as `complete ÷ total` — skipped modules count toward the total, so skipping a module lowers the overall percentage rather than removing it from the calculation.

### In Progress Strip

A strip of cards below the summary bar surfaces every module currently marked `in_progress` across all subjects — regardless of which subject or milestone it belongs to. Each card shows the module title, its subject and milestone context, and any metadata chips (estimated time, difficulty, type).

The strip is hidden entirely when no modules are in progress.

### Subject Cards

Each subject is displayed as a collapsible card. The header shows:
- Subject title and description
- Estimated time
- Milestone and module count
- Completion percentage and progress bar
- Chevron indicating open/closed state

Click a subject card header to expand or collapse its milestone list.

### Milestone Rows

Within each expanded subject, milestones appear as collapsible rows. Each row shows:
- Order number, title, and description
- Estimated time
- Completion percentage and progress bar

Click a milestone row to expand or collapse its module list.

### Module Rows

Within each expanded milestone, modules appear as individual rows showing:
- **Status badge** (clickable — opens the status dropdown)
- Module title
- Type and difficulty chips
- Estimated time
- `started_date` and `completed_date` (displayed in monospace when present)
- Resource links

---

## Editing Status

Click any module's **status badge** to open a dropdown with all four status options. The current status is highlighted, and each option includes a short description of what it does.

| Status | Badge | Description shown in dropdown |
|--------|-------|-------------------------------|
| `not_started` | Gray | Reset progress |
| `in_progress` | Green (jade) | Currently active |
| `complete` | Amber | Auto-fills date |
| `skipped` | Lavender | Intentionally bypass |

Clicking anywhere outside an open dropdown closes it without making a change. Only one dropdown can be open at a time.

**Automatic date handling:**
- Setting status to `in_progress` auto-fills `started_date` with today's date (only if not already set)
- Setting status to `complete` auto-fills both `started_date` (if not already set) and `completed_date` with today's date
- Resetting to `not_started` clears both dates

After a status change the dashboard re-renders, but any subjects and milestones you had expanded remain open.

---

## Undo

After every status change, a toast notification appears at the bottom of the screen with a 5-second undo window. Click **Undo** in the toast to fully revert — this restores the previous status and both date fields exactly as they were before the change.

The undo window covers only the most recent change. Once the toast disappears or another status change is made, the previous state cannot be recovered (though your localStorage cache still has the prior state until you save).

---

## Saving Changes

The **Download** button serializes your current in-memory state back to a valid YAML file. Save behavior differs by browser:

| Browser | Save behavior |
|---------|--------------|
| **Chrome / Edge** | Uses the File System Access API — writes directly back to the original file in place. A confirmation toast appears. No file replacement needed. |
| **Firefox / Safari** | Falls back to a standard download — saves a copy to your Downloads folder. Replace your original `waypoint.yaml` with the downloaded file to apply changes. |
| **Auto-loaded files** | Even on Chrome/Edge, files loaded via auto-load (fetch) don't have a file handle, so the download path is used. |

Regardless of browser, after a successful save:
- The unsaved changes indicator disappears
- The Download button returns to its gray state
- The localStorage cache is cleared

The saved file is fully valid YAML and can be committed to git, re-loaded into the dashboard, or opened in any text editor.

---

## Session Persistence

The dashboard writes your current state to `localStorage` on every status change. If you close the tab, refresh, or navigate away before saving, your changes survive.

On the next load (once a file is available), the dashboard shows a **Restore session** banner with the date and time of the last auto-save. Two options:

- **Restore session** — dismisses the banner and keeps the cached state loaded. Your unsaved changes remain active.
- **Discard** — clears the cache, hides the dashboard entirely, and returns to the upload screen. All unsaved changes are lost.

The cache is cleared automatically after any successful save or download.

---

## Themes

Three built-in themes are available via the palette icon in the navbar. Each theme changes the color treatment of subject headers, milestone rows, and module rows independently.

| Theme | Subject header | Milestone rows | Module rows |
|-------|---------------|----------------|-------------|
| **Default** | Dark forest green | Mist green | White surface |
| **Minimal** | White surface | White surface | Light parchment |
| **Warm** | Brand teal | Parchment | White surface |

All three themes share the same base color palette — only the surface colors and hierarchy treatment change. The teal accent, amber badges, and lavender skipped badges remain consistent across themes.

Your selected theme is stored in `localStorage` and restored automatically on every reload.

<br>

---

<img align="left" src="../branding/banners/waypoint_banner_lightbg.png" height="64" alt="waypoint">
<div align="right">v1.0.0</div>
<br clear="both">
