<br><br>
<img align="right" src="../branding/icons/waypoint_standalonemark_lightbg.png" height="44" alt="waypoint">
<h1>Project Structure</h1>
<br clear="both">

A guide to the waypoint folder layout — what each directory is for, how to organize content within it, and how each folder connects to your `waypoint.yaml`.

<br>

## Overview

```
waypoint/
├── .waypoint/          # Framework files — not your content
├── docs/               # Reference documentation and saved resources
├── labs/               # Hands-on exercises and environment files
├── notes/              # Personal notes and study summaries
├── scripts/            # Automation scripts and setup helpers
├── waypoint.yaml       # Your learning roadmap and progress tracker
└── waypoint.html       # waypoint — opens in any browser
```

The four content directories (`docs/`, `labs/`, `notes/`, `scripts/`) are yours to fill. They are intentionally separate from `.waypoint/` so your learning content is never mixed with framework internals.

---

## Structure is a Suggestion

The folder names above are a starting convention — not a requirement of the framework. waypoint doesn't enforce any particular layout. The only thing that matters is that `path:` values in your `waypoint.yaml` point to real files relative to the repo root.

That means you are free to:

- **Omit folders you don't need.** If you never write lab files, don't create a `labs/` folder. If all your resources are external links, you may not need any content folders at all.
- **Rename folders to suit your workflow.** Nothing in waypoint or the schema assumes a folder is called `notes/` or `labs/`.
- **Organize by subject at the root.** Rather than grouping by content type first (`notes/kubernetes/`, `notes/python/`), you might prefer to group by subject first (`kubernetes/notes/`, `python/notes/`). Both are valid — the path in the YAML just needs to match wherever the file actually lives.
- **Create folders that don't exist here.** A `certifications/` folder for completion certificates, a `resources/` folder for downloads, a `diagrams/` folder for architecture sketches — if it helps you organize, it belongs.

The reference sections below describe how each suggested folder is typically used. Treat them as a guide, not a prescription.

> For complete examples showing different structures alongside their matching `waypoint.yaml` files → [`examples.md`](examples.md)

---

## notes/

Personal notes organized by subject and module — summaries, key concepts, things worth remembering.

### Suggested structure

```
notes/
└── <subject>/
    └── <milestone>/
        └── <module>.md
```

### Example

```
notes/
└── kubernetes/
    └── foundations/
        ├── what-is-kubernetes.md
        └── cluster-architecture.md
```

### Linking to waypoint.yaml

```yaml
resources:
  - type: notes
    label: "My Notes"
    path: "notes/kubernetes/foundations/what-is-kubernetes.md"
```

> You don't need a separate file per module. A single milestone-level notes file with section headings per module is a perfectly valid approach.

---

## docs/

Reference documentation, study guides, whitepapers, and saved resources. Use this folder when you want your reference materials to be portable and included in the repo.

If all your reference material is external (links only), this folder can remain empty.

### Suggested structure

```
docs/
└── <subject>/
    └── <milestone>/
        └── <filename>.<ext>
```

### Example

```
docs/
└── kubernetes/
    └── architecture/
        ├── cka-exam-guide.pdf
        └── kubernetes-architecture-overview.md
```

### Linking to waypoint.yaml

Use `type: external` with a local file path if you want to link a document directly from waypoint:

```yaml
resources:
  - type: external
    label: "CKA Exam Guide"
    url: "docs/kubernetes/architecture/cka-exam-guide.pdf"
```

---

## labs/

Hands-on exercises, environment configurations, and lab files. Anything you *do* rather than just read lives here.

### Suggested structure

```
labs/
└── <subject>/
    └── <lab-name>/
        ├── README.md
        └── <lab-files>
```

### Example

```
labs/
└── kubernetes/
    └── deploy-nginx/
        ├── README.md
        └── nginx-deployment.yaml
```

### Linking to waypoint.yaml

```yaml
resources:
  - type: lab
    label: "Deploy Nginx"
    path: "labs/kubernetes/deploy-nginx/README.md"
```

> Each lab should have its own subdirectory with a `README.md` that describes the objectives, prerequisites, and steps.

---

## scripts/

Automation scripts, setup helpers, and teardown scripts. Anything that makes your learning environment faster to spin up or reset.

### Suggested structure

```
scripts/
└── <subject>/
    └── <script-name>.<ext>
```

### Example

```
scripts/
└── kubernetes/
    ├── setup-local-cluster.sh
    └── teardown.sh
```

### Linking to waypoint.yaml

```yaml
resources:
  - type: script
    label: "Setup Local Cluster"
    path: "scripts/kubernetes/setup-local-cluster.sh"
```

---

## .waypoint/

Framework files — branding assets, AI tooling, and internal documentation. This directory is not part of your learning content. You generally won't need to touch it.

See [`.waypoint/README.md`](../README.md) for a full breakdown of what's inside.

---

## waypoint.yaml

Your entire learning roadmap. Defines subjects, milestones, and modules, and tracks the status of each. This is the file you edit as you plan your learning and the one waypoint reads to render your progress.

See [`yaml-schema.md`](yaml-schema.md) for a complete field reference.

---

## waypoint.html

A single HTML file containing the complete waypoint application — no dependencies, no build step. Open it directly in any modern browser. When served from the same directory as your YAML file (e.g. via GitHub Pages or a local server), it auto-loads on startup.

See [`waypoint.md`](waypoint.md) for a full feature guide.

<br>

---

<img align="left" src="../branding/banners/waypoint_banner_lightbg.png" height="64" alt="waypoint">
<div align="right">v1.0.0</div>
<br clear="both">
