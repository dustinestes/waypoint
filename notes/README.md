# notes/

Personal notes organized by subject and module. This is your scratchpad — summaries, key concepts, things worth remembering.

> Note: You don't have to create a bunch of singular notes files for each module. You could, for instance, create one milestone-specific notes file and each module could have a heading and section for its related notes.

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

---

<sub>Powered by Waypoint — github.com/dustinestes/waypoint</sub>
