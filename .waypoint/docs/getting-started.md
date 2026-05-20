<br><br>
<img align="right" src="../branding/icons/waypoint_standalonemark_lightbg.png" height="44" alt="waypoint">
<h1>Getting Started</h1>
<br clear="both">

A step-by-step walkthrough for setting up waypoint and tracking your first learning path.

<br>

## Prerequisites

- A modern browser (Chrome, Firefox, Edge, Safari)
- Git (optional — you can also download the repo as a ZIP)
- A text editor for editing YAML

No build tools, no package manager, no server required.

---

## 1. Get the Repo

Fork or clone the waypoint repository into a directory named after your learning context:

```bash
git clone https://github.com/dustinestes/waypoint.git my-learning
cd my-learning
```

If you're using this for a specific goal, name it something meaningful:

```bash
git clone https://github.com/dustinestes/waypoint.git cka-prep
```

---

## 2. Clear the Example Content

The repo ships with a sample `waypoint.yaml` to demonstrate the structure. Before adding your own content, remove the example subjects and start fresh.

Open `waypoint.yaml` and replace everything under `subjects:` with your own entries. Keep the top-level key — only clear the content beneath it:

```yaml
subjects:
  # your subjects go here
```

---

## 3. Define Your First Subject

A subject is your top-level learning area — a certification, a technology, a domain. Add one to get started:

```yaml
subjects:

  - id: kubernetes
    title: "Kubernetes"
    description: "Container orchestration from core concepts to production patterns"
    estimated_time: "40 hours"
    milestones:
```

- `id` — a unique slug, lowercase with hyphens. **Never change it once set** — it's used as a stable identifier.
- `title` — display name shown in waypoint
- `description` — optional, shown on the subject card
- `estimated_time` — free text, shown alongside the subject

---

## 4. Add Milestones

Milestones are logical phases or chapters within a subject. Add them under `milestones:`:

```yaml
    milestones:

      - id: foundations
        title: "Foundations"
        description: "Core concepts and cluster architecture"
        order: 1
        estimated_time: "8 hours"
        modules:
```

- `order` — controls display order in waypoint (ascending)

---

## 5. Add Modules

Modules are the individual learning units — a video to watch, a doc to read, a lab to complete. Add them under `modules:`:

```yaml
        modules:

          - id: what-is-kubernetes
            title: "What is Kubernetes?"
            order: 1
            type: reading
            difficulty: beginner
            estimated_time: "1 hour"
            status: not_started
            started_date:
            completed_date:
            resources:
              - type: external
                label: "Official Docs"
                url: "https://kubernetes.io/docs/concepts/overview/"
```

> See the full field reference → [`yaml-schema.md`](yaml-schema.md)

---

## 6. Create Your Folder Structure

As you add modules, create matching folders for your materials. The structure mirrors your YAML:

```
notes/
└── kubernetes/
    └── foundations/
        └── what-is-kubernetes.md

labs/
└── kubernetes/
    └── deploy-nginx/
        ├── README.md
        └── nginx-deployment.yaml
```

> See the full structure guide → [`project-structure.md`](project-structure.md)

---

## 7. Link Resources in Your YAML

Reference your local files directly in each module's `resources:` array:

```yaml
            resources:
              - type: external
                label: "Official Docs"
                url: "https://kubernetes.io/docs/concepts/overview/"
              - type: notes
                label: "My Notes"
                path: "notes/kubernetes/foundations/what-is-kubernetes.md"
              - type: lab
                label: "Deploy Nginx"
                path: "labs/kubernetes/deploy-nginx/README.md"
```

Resource types: `external` · `notes` · `lab` · `script`

---

## 8. Open waypoint

Open `waypoint.html` directly in your browser. If your YAML file is in the same directory (e.g., serving via GitHub Pages or a local server), it loads automatically. Otherwise, use the file picker or drag-and-drop your YAML file onto the page.

> See the full guide → [`waypoint.md`](waypoint.md)

---

## 9. Update Your Progress

As you complete modules, click the status badge in waypoint to cycle through statuses:

`not_started` → `in_progress` → `complete` → `skipped`

Dates are filled in automatically when you change status. Use the **Download** button to save your updated YAML back to disk.

---

## 10. Keep It in Git

Commit your `waypoint.yaml` regularly so your progress is version-controlled:

```bash
git add waypoint.yaml notes/ labs/ docs/ scripts/
git commit -m "chore: update progress — kubernetes foundations in progress"
```

<br>

---

<img align="left" src="../branding/banners/waypoint_banner_lightbg.png" height="64" alt="waypoint">
<div align="right">v1.0.0</div>
<br clear="both">
