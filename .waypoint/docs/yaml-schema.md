<br><br>
<img align="right" src="../branding/icons/waypoint_standalonemark_lightbg.png" height="44" alt="waypoint">
<h1>YAML Schema Reference</h1>
<br clear="both">

Complete field-by-field reference for `waypoint.yaml`. All fields listed as optional can be omitted or left blank — waypoint handles missing values gracefully.

<br>

## Structure Overview

```
waypoint.yaml
└── subjects[]
    ├── (subject fields)
    └── milestones[]
        ├── (milestone fields)
        └── modules[]
            ├── (module fields)
            └── resources[]
```

---

## Subject

The top-level learning area. A waypoint.yaml can contain one or more subjects.

```yaml
subjects:

  - id: kubernetes
    title: "Kubernetes"
    description: "Container orchestration from core concepts to production patterns"
    icon:
    estimated_time: "40 hours"
    milestones:
```

| Field | Required | Type | Description |
|-------|----------|------|-------------|
| `id` | Yes | string | Unique slug — lowercase, hyphens only. **Never change once set.** |
| `title` | Yes | string | Display name shown in waypoint |
| `description` | No | string | Short description shown on the subject card |
| `icon` | No | string | Relative path to an icon image (e.g. `assets/k8s.png`) |
| `estimated_time` | No | string | Free text — `"40 hours"`, `"6 weeks"`, `"3 days"` |
| `milestones` | Yes | array | List of milestone objects (see below) |

---

## Milestone

A logical phase or chapter within a subject. Milestones group related modules.

```yaml
    milestones:

      - id: foundations
        title: "Foundations"
        description: "Core concepts and cluster architecture"
        order: 1
        estimated_time: "8 hours"
        modules:
```

| Field | Required | Type | Description |
|-------|----------|------|-------------|
| `id` | Yes | string | Unique slug within this subject — lowercase, hyphens only |
| `title` | Yes | string | Display name shown in waypoint |
| `description` | No | string | Short description shown on the milestone row |
| `order` | No | integer | Controls display order in waypoint (ascending). Defaults to YAML order if omitted. |
| `estimated_time` | No | string | Free text — same format as subject |
| `modules` | Yes | array | List of module objects (see below) |

---

## Module

An individual learning unit — a resource to consume, a lab to complete, or a concept to study.

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
```

| Field | Required | Type | Description |
|-------|----------|------|-------------|
| `id` | Yes | string | Unique slug within this milestone — lowercase, hyphens only |
| `title` | Yes | string | Display name shown in waypoint |
| `order` | No | integer | Controls display order within the milestone |
| `type` | No | enum | `reading` · `video` · `lab` · `quiz` · `mixed` |
| `difficulty` | No | enum | `beginner` · `intermediate` · `advanced` |
| `estimated_time` | No | string | Free text |
| `status` | Yes | enum | See [Statuses](#statuses) below |
| `started_date` | No | string | ISO 8601 date — `"2025-03-10"`. Auto-filled by waypoint when status is set to `in_progress`. |
| `completed_date` | No | string | ISO 8601 date — `"2025-03-12"`. Auto-filled by waypoint when status is set to `complete`. |
| `resources` | No | array | List of resource objects (see below) |

---

## Statuses

| Value | Meaning |
|-------|---------|
| `not_started` | Default — not yet begun |
| `in_progress` | Currently being studied |
| `complete` | Finished |
| `skipped` | Intentionally skipped (excluded from progress calculation) |

waypoint auto-fills `started_date` when a module moves to `in_progress`, and `completed_date` when it moves to `complete`. Both dates are cleared if status is reset to `not_started`.

---

## Resources

Each module can have zero or more resources — links to external content or local files.

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

              - type: script
                label: "Setup Script"
                path: "scripts/kubernetes/setup-local-cluster.sh"
```

| Field | Required | Type | Description |
|-------|----------|------|-------------|
| `type` | Yes | enum | `external` · `notes` · `lab` · `script` |
| `label` | Yes | string | Display text for the link in waypoint |
| `url` | Conditional | string | Required when `type: external` |
| `path` | Conditional | string | Required for all other types — relative path from repo root |

### Resource types

| Type | Use |
|------|-----|
| `external` | Link to any external URL — documentation, videos, courses |
| `notes` | Path to a local notes file in `notes/` |
| `lab` | Path to a lab directory or file in `labs/` |
| `script` | Path to an automation script in `scripts/` |

---

## Blank Template

A complete copyable template with every field present. Remove or leave blank any optional fields you don't need. Add additional subjects, milestones, and modules by duplicating the respective block.

```yaml
subjects:

  - id:
    title: ""
    description: ""
    icon:
    estimated_time: ""

    milestones:

      - id:
        title: ""
        description: ""
        order: 1
        estimated_time: ""

        modules:

          - id:
            title: ""
            order: 1
            type:
            difficulty:
            estimated_time: ""
            status: not_started
            started_date:
            completed_date:
            resources:
              - type:
                label: ""
                url:
                path:
```

> For real-world examples of how to structure a `waypoint.yaml` for different learning scenarios → [`examples.md`](examples.md)

<br>

---

<img align="left" src="../branding/banners/waypoint_banner_lightbg.png" height="64" alt="waypoint">
<div align="right">v1.0.0</div>
<br clear="both">
