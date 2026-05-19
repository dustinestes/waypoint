<br><br>
<img align="right" src="../.waypoint/branding/icons/waypoint_standalonemark_lightbg.png" height="44" alt="Waypoint">
<h1>notes/</h1>
<br clear="both">

Personal notes organized by subject and module. This is your scratchpad — summaries, key concepts, things worth remembering.

> Note: You don't have to create a bunch of singular notes files for each module. You could, for instance, create one milestone-specific notes file and each module could have a heading and section for its related notes.

<br>

## Suggested Structure

```
notes/
└── <subject>/
    └── <milestone>/
        └── <module>.md
```

## Example

```
notes/
└── kubernetes/
    └── core-concepts/
        ├── what-is-kubernetes.md
        └── cluster-architecture.md
```

Notes files are referenced from `waypoint.yaml` via the `resources:` array with a `type: notes` field on each module.

<br>

---

<img align="left" src="../.waypoint/branding/banners/waypoint_banner_lightbg.png" height="64" alt="Waypoint">
<div align="right">v1.0</div>
<br clear="both">
