# Waypoint — Product Roadmap

A living document tracking planned features, improvements, and ideas across versions.
Items marked ✓ are shipped. Items without a mark are planned or in consideration.

---

## v1 — Minimal viable product

The core read + track experience. A learner can load their `waypoint.yaml`, view their
progress, and update module statuses — all from a single HTML file with no dependencies
beyond a browser.

### Dashboard
- ✓ Auto-load `waypoint.yaml` from same directory (GitHub Pages / local server)
- ✓ File picker + drag-and-drop fallback for local use
- ✓ Summary bar — total, complete, in progress, not started, skipped counts
- ✓ Overall progress bar
- ✓ In progress strip — active modules surfaced at the top
- ✓ Subject cards — collapsible, with progress bar, milestone count, estimated time
- ✓ Milestone rows — collapsible, with progress bar and estimated time
- ✓ Module rows — status badge, type, difficulty, estimated time, resource links
- ✓ started_date and completed_date displayed per module

### Editing
- ✓ Click badge to open status dropdown (not_started / in_progress / complete / skipped)
- ✓ Auto-fill `started_date` when status set to in_progress
- ✓ Auto-fill `completed_date` when status set to complete
- ✓ Clear dates when status reset to not_started
- ✓ Undo toast — 5 second window to revert a status change
- ✓ Unsaved changes indicator — amber pill in navbar
- ✓ Download button state — gray when clean, teal when unsaved changes exist
- ✓ Download updated YAML — serializes in-memory state back to valid YAML
- ✓ localStorage cache — auto-saves state on every change
- ✓ Restore session banner — offered on next load if unsaved cache exists
- ✓ Cache cleared automatically after successful download

### Theming and branding
- ✓ Three built-in themes — Default (dark header), Minimal (left border depth), Warm (teal header)
- ✓ Theme picker — palette icon in navbar, popover with named swatches
- ✓ Theme persisted in localStorage across reloads
- ✓ Subject / milestone / module hierarchy visually distinguished per theme
- ✓ Footer — Waypoint logo, tagline, version number, GitHub link
- ✓ Footer attribution preserved as open source requirement (MIT)

### YAML schema
- ✓ Hierarchy: subject → milestone → module
- ✓ Statuses: not_started | in_progress | complete | skipped
- ✓ Module metadata: difficulty, type, estimated_time, started_date, completed_date
- ✓ Resources: internal (notes, lab, script) and external (url) per module
- ✓ Estimated time optional at subject, milestone, and module level
- ✓ All optional fields present as blank keys for easy authoring

---

## v2 — Authoring and structure editing

Allows users to build and modify their learning path directly in the dashboard,
without needing to hand-edit YAML.

### Editing — structure
- [ ] Add a new module to a milestone (title, type, difficulty, estimated_time)
- [ ] Add a new milestone to a subject
- [ ] Add a new subject
- [ ] Delete a module (with confirmation)
- [ ] Delete a milestone (with confirmation, warns if modules exist)
- [ ] Reorder modules within a milestone via drag-and-drop
- [ ] Reorder milestones within a subject via drag-and-drop
- [ ] Edit module title, description, type, difficulty, estimated_time inline
- [ ] Edit milestone title and description inline
- [ ] Edit subject title, description, and estimated_time inline
- [ ] Add / remove resource links per module

### Dashboard improvements
- [ ] Filter modules by status across all subjects
- [ ] Filter modules by type or difficulty
- [ ] Subject-level completion percentage shown as a ring/donut rather than bar
- [ ] Estimated vs actual time comparison per module (where both dates present)
- [ ] Milestone completion dates (derived from last module completion)
- [ ] Search across all modules by title

### Org branding (v2)
- [ ] Config block at top of dashboard.html — org name, logo URL, accent color overrides
- [ ] Logo replacement — org logo displayed in navbar in place of or alongside Waypoint mark
- [ ] Custom accent colors — override teal ramp via config without touching core CSS
- [ ] Footer customization — org name shown alongside Waypoint attribution
- [ ] Theme locked to org default — disable picker if org config specifies a forced theme

### YAML schema extensions
- [ ] `tags` field on modules — free text array for cross-subject grouping
- [ ] `notes` field on modules — short freeform text for learner annotations
- [ ] `prerequisites` field on modules — list of module ids that should precede this one

---

## v3 — Connectivity and AI

Connects Waypoint to external services and introduces AI-assisted learning path generation.

### GitHub integration
- [ ] GitHub personal access token support (stored in localStorage, never transmitted)
- [ ] Read `waypoint.yaml` directly from a GitHub repo via GitHub API
- [ ] Write changes back to repo via GitHub API (auto-commit on download)
- [ ] Commit message customization before write-back
- [ ] GitHub Pages auto-deploy detection — notify user when live version is out of sync

### AI learning path generation
- [ ] Claude AI skill / instruction set for generating a `waypoint.yaml` from a subject or certification goal
- [ ] AI-assisted module suggestions — given a subject, suggest milestones and modules
- [ ] Repo-as-artifact support — share the entire Waypoint repo with an AI agent for context-aware suggestions
- [ ] AI review of completed modules — suggest next steps based on progress

### Org branding (v3)
- [ ] `waypoint.config.yaml` — separate config file read alongside learning YAML
- [ ] Full theme definition in config — colors, fonts, logo, footer links all configurable
- [ ] Multiple theme files — orgs can ship their own named `.theme.yaml` files
- [ ] Theme marketplace / community themes — shareable theme definitions via GitHub

### `.wayp` custom file type (revisit)
- [ ] VS Code extension — registers `.wayp` as YAML for syntax highlighting and linting
- [ ] File association for `.wayp` across common editors
- [ ] Migrate default file extension from `.yaml` to `.wayp` once editor support exists


---

## Backlog — unversioned ideas

Things worth considering but not yet assigned to a version.

- [ ] Educator mode — hide progress/date fields, show only structure and estimated times for curriculum review
- [ ] Milestone certificates — generated completion summary when all modules in a milestone are done (requires anti-abuse design — see notes below)

---

## v2 additions

### UI and experience
- [ ] Dark mode — manual toggle and/or auto-detection from system `prefers-color-scheme`
- [ ] Multiple YAML files — load and switch between several learning paths without reloading the page

---

## v3 additions

### Portability and sharing
- [ ] Print / PDF export — formatted snapshot of current progress, suitable for sharing with an employer or saving as a record
- [ ] Progress sharing — generate a read-only shareable link (requires hosting infrastructure)
- [ ] Time tracking — optional per-session timer on modules, accumulated total stored in YAML; complements the existing date timestamps with actual invested time
- [ ] Localization — UI language support and locale-aware date formatting (see notes below)

### Milestone certificates (when credibility design is resolved)
- [ ] Certificate generation — visual completion certificate when all modules in a milestone are marked complete
- [ ] Anti-abuse consideration — certificates are self-reported by definition (status is set by the learner); credibility comes from the issuing educator/org publishing the YAML publicly so the syllabus is verifiable, not from the completion itself
- [ ] Possible path — signed certificates using a private key held by the educator/org, with a public verification URL; complex but the only real tamper-resistance without a server

---

## Notes

### Educator mode
Currently in backlog pending clearer use case definition. The core idea: an educator composing a Waypoint YAML for a class or team could open the dashboard in "educator mode" which hides all learner progress fields (status, dates, time) and instead surfaces curriculum design views — estimated time totals per milestone, difficulty distribution, module type breakdown. Useful for reviewing and balancing a learning path before publishing it. A secondary angle: a read-only "syllabus view" a learner could share with a manager showing what they are studying without exposing their personal progress data.

### Milestone certificates
The credibility problem is real and worth designing around carefully before building. A few approaches in increasing order of robustness:
1. **Honor system** — certificate simply states "self-reported completion" clearly. Lowest friction, lowest trust.
2. **Educator countersignature** — the YAML includes an educator ID; certificate requires the educator to have published/signed the original YAML. Learner can't forge the syllabus origin.
3. **Cryptographic signing** — educator signs the YAML with a private key at publish time; certificate includes a verification hash; anyone can verify against the public key. Strong tamper-resistance, high complexity.
Starting at (1) with a path to (2) is the pragmatic v3 approach.

### Localization
Localization in a single HTML file is achievable without an API. The standard approach is a JS object acting as a string lookup table — one object per locale, keys are string identifiers, values are translated strings. On load, detect `navigator.language`, pick the matching locale object, and replace all UI strings via the lookup. Date formatting is handled by the built-in `Intl.DateTimeFormat` API (already in all modern browsers, no library needed). The main effort is authoring the translation files — the community can contribute locale files as separate JS imports, which fits the open source model well. No external API required.

---

*Last updated: see git log*
