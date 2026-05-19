<br><br>
<img align="right" src=".waypoint/branding/icons/waypoint_standalonemark_lightbg.png" height="44" alt="Waypoint">
<h1>Contributing</h1>
<br clear="both">

Thanks for your interest in contributing. Waypoint is a small, focused project and contributions are welcome — whether that's a bug fix, a new feature, documentation improvements, or just opening an issue with a thoughtful idea.

<br>

## Ways to Contribute

- **Bug reports** — something broken or behaving unexpectedly? Open an issue.
- **Feature requests** — have an idea that fits the project's direction? Open an issue and describe the use case.
- **Pull requests** — fixes, improvements, or new functionality. See the process below.
- **Documentation** — clearer explanations, better examples, or corrected typos are always appreciated.

---

## Before You Open a PR

1. **Check existing issues and PRs** to avoid duplicating work in progress.
2. **Open an issue first** for anything significant — a new feature, a change to the YAML schema, or a restructure of the scaffold. This keeps effort aligned before code is written.
3. **Keep PRs focused.** One concern per pull request makes review faster and merging cleaner.

---

## Development Setup

No build tooling is required. Clone the repo and open files directly.

```bash
git clone https://github.com/dustinestes/waypoint.git
cd waypoint
```

The dashboard (`dashboard.html`) opens directly in any modern browser. The YAML schema is documented in `waypoint.yaml` and the README.

---

## Code & Style Guidelines

- **YAML** — keep the schema human-readable and flat where possible. Avoid nesting beyond three levels.
- **HTML/CSS/JS** — vanilla only for the dashboard; no build dependencies.
- **Comments** — write comments for anything non-obvious. This project is used by learners, so clarity matters.
- **Naming** — use `snake_case` for YAML keys and file names. Match existing conventions in the repo.

---

## Commit Messages

Use a conventional commit prefix followed by a short, present-tense description:

```
feat: add drag-and-drop reordering for modules
fix: resolve status badge color for skipped modules
docs: update README with getting started steps
chore: remove unused CSS variables
```

| Prefix | When to use |
|--------|-------------|
| `feat:` | New feature or user-facing enhancement |
| `fix:` | Bug fix |
| `docs:` | Documentation changes only |
| `chore:` | Maintenance, tooling, or non-functional changes |
| `breaking:` | Change that breaks backwards compatibility |

---

## Attribution Requirement

Per the project license, any derivative work or fork that is publicly distributed must retain the footer attribution intact. Contributions to this repo are made under the same license terms. By submitting a pull request, you agree that your contribution may be distributed under the project's MIT + Attribution license.

---

## Questions

Open an issue and tag it `question`. There's no wrong question here.

<br>

---

<img align="left" src=".waypoint/branding/banners/waypoint_banner_lightbg.png" height="64" alt="Waypoint">
<div align="right">v1.0.0</div>
<br clear="both">
