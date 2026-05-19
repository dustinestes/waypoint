<br/><br/>

<div align="center">

<br/>

<picture>
  <source media="(prefers-color-scheme: dark)" srcset=".waypoint/branding/banners/waypoint_banner_darkbg.png">
  <img alt="Waypoint" src=".waypoint/branding/banners/waypoint_banner_lightbg.png" height="130">
</picture>


<br/><br/>

![License](https://img.shields.io/badge/license-MIT%20%2B%20Attribution-1D9E75?style=flat-square&labelColor=085041)
![Version](https://img.shields.io/badge/version-v1.0.0-1D9E75?style=flat-square&labelColor=085041)
![Build Step](https://img.shields.io/badge/build%20step-none-1D9E75?style=flat-square&labelColor=085041)
![Works Offline](https://img.shields.io/badge/works-offline-1D9E75?style=flat-square&labelColor=085041)

<br/>

</div>

<br/><br/>

---

Waypoint is a lightweight, file-based framework for structuring and tracking self-directed learning — across any subject, platform, or learning path. Whether you're grinding through a certification, exploring a new technology, or building knowledge across multiple unrelated topics at once, Waypoint gives you a single place to define what you're learning, track where you are, and navigate what's next.

---

<br/>

## What It Does

- **Scaffold** your learning materials — notes, docs, labs, and scripts — in a consistent, portable folder structure
- **Define** your learning roadmap in a single YAML file: subjects, milestones, and modules
- **Track** your progress by updating module statuses directly in YAML (`not_started`, `in_progress`, `complete`, `skipped`)
- **Visualize** everything through a local dashboard that reads your YAML and displays progress at a glance, with direct links to your materials
- *(Planned)* **Generate** learning plans via AI — share your repo as context and let an agent scaffold a full roadmap for any subject or certification

---

<br/>

## Who It's For

Waypoint is built for anyone who learns outside of a single structured system — people pulling from documentation, YouTube, courses, books, labs, and blog posts all at once and trying to make sense of where they stand.

That includes:
- Developers and engineers pursuing certifications or exploring new tools
- Students and career changers mapping a path into a new field
- Curious generalists tracking progress across multiple subjects simultaneously

If your learning doesn't fit neatly into one platform's progress bar, Waypoint is for you.

---

<br/>

## Project Structure

```
waypoint/
├── .waypoint/          # Project related files, branding elements, AI tooling, and all the other "under the hood" elements
├── docs/               # Reference documentation, whitepapers, study guides
├── labs/               # Hands-on exercises, environment configs, lab files
├── notes/              # Personal notes organized by subject or module
├── scripts/            # Automation scripts, setup helpers, tooling
├── waypoint.yaml       # Your learning roadmap and progress tracker
└── dashboard.html      # Local progress dashboard (opens in browser)
```

---

<br/>

## The YAML Roadmap

Your entire learning plan lives in `waypoint.yaml`. Define subjects, break them into milestones, and list the modules within each. Update statuses as you go.

```yaml
subjects:

  - id: kubernetes                 # Unique slug — never change once set
    title: "Kubernetes"
    description: "Container orchestration from core concepts to production patterns"
    icon:                          # (optional) relative path from repo root e.g. assets/k8s.png
    estimated_time: "40 hours"     # (optional) free text — "40 hours", "6 weeks", "3 days", etc.

    # -------------------------------------------------------------------------
    # MILESTONES
    # Logical groupings of modules within a subject.
    # -------------------------------------------------------------------------

    milestones:

      - id: foundations            # Unique slug within this subject
        title: "Foundations"
        description: "Core concepts and architecture"
        order: 1                   # Controls display order in the dashboard
        estimated_time: "8 hours"  # (optional)

        # ---------------------------------------------------------------------
        # MODULES
        # Individual learning units within a milestone.
        # ---------------------------------------------------------------------

        modules:

          - id: what-is-kubernetes       # Unique slug within this milestone
            title: "What is Kubernetes?"
            order: 1                     # Controls display order in the dashboard
            difficulty: beginner         # (optional) beginner | intermediate | advanced
            type: reading                # (optional) reading | video | lab | quiz | mixed
            estimated_time: "1 hour"     # (optional)
            status: complete             # not_started | in_progress | complete | skipped
            started_date: "2025-03-10"   # (optional) ISO 8601 — fill in when you begin
            completed_date: "2025-03-12" # (optional) ISO 8601 — fill in when done
            resources:
              - type: external
                label: "Docs"
                url: "https://kubernetes.io/docs/concepts/overview/"
              - type: notes              # notes | lab | script | external
                label: "Notes"
                path: "notes/kubernetes/foundations/what-is-kubernetes.md"
```

**Statuses:** `not_started` · `in_progress` · `complete` · `skipped`

---

<br/>

## Dashboard

Open `dashboard.html` in your browser to see a visual summary of your roadmap — progress by milestone, module status at a glance, and direct links to your notes and materials. No build step, no server required.

---

<br/>

## Getting Started

1. **Fork or clone** this repository
   ```bash
   git clone https://github.com/dustinestes/waypoint.git my-learning
   cd my-learning
   ```

2. **Edit `waypoint.yaml`** to define your subject, milestones, and modules

3. **Add your materials** to `docs/`, `notes/`, `labs/`, and `scripts/` as you go and add links to these items in your waypoint.yaml file for easy access

4. **Open `dashboard.html`** in your browser to track progress

5. **Update statuses** in `waypoint.yaml` as you complete modules

---

<br/>

## Roadmap

- **Planned and in-progress** → [GitHub Issues](https://github.com/dustinestes/waypoint/issues)
- **Shipped by version** → [GitHub Releases](https://github.com/dustinestes/waypoint/releases)

---

<br/>

## Contributing

Contributions, ideas, and feedback are welcome. Please read [CONTRIBUTING.md](CONTRIBUTING.md) before opening a pull request.

---

<br/>

## License

This project is licensed under the MIT License with an Attribution Condition. You are free to use, fork, and modify Waypoint for any purpose. The footer attribution must remain intact in any redistribution or derivative work. See [LICENSE](LICENSE) for full terms.

---

<br/>

## Contributors

- **Dustin Estes** — creator, product design, and development
- **[Claude](https://claude.ai) (Anthropic)** — AI development assistant

<br>

---

<img align="left" src=".waypoint/branding/banners/waypoint_banner_lightbg.png" height="64" alt="Waypoint">
<div align="right">v1.0.0</div>
<br clear="both">
