<br><br>
<img align="right" src="../branding/icons/waypoint_standalonemark_lightbg.png" height="44" alt="waypoint">
<h1>Customizing the Dashboard</h1>
<br clear="both">

A technical guide to modifying `dashboard.html` — color palette, typography, layout, navbar, themes, and status badges — for teams or individuals who want to adapt the dashboard to their own visual style.

All customization is done by editing `dashboard.html` directly in a text editor. There is no build step — save the file and reload in the browser to see changes.

<br>

---

## Before You Start

### What you can change

Everything inside the `<style>` block and the `<nav>` element is open for modification. The sections below describe each area and where to find it in the file.

### What you must not change

The `<footer>` element must remain **completely untouched** — no additions, no removals, no rewording of any kind. The footer contains the attribution required by the MIT + Attribution license.

```html
<!-- IMPORTANT: You must retain the footer attribution element in its entirety
     and without modification. See LICENSE for details. -->
<footer class="footer">
  ...
</footer>
```

Do not add your organization name, tagline, logo, or any other content to the footer. The waypoint mark, tagline, version, and GitHub link must remain exactly as shipped.

---

## Color Palette

All colors are defined as CSS custom properties inside the `:root` block near the top of the `<style>` section (around line 15). These variables are referenced throughout the dashboard — updating a value here propagates everywhere it is used.

```css
:root {
  /* ── Brand greens ── */
  --wp-mist:        #E1F5EE;
  --wp-jade:        #9FE1CB;
  --wp-mint:        #5DCAA5;
  --wp-teal:        #1D9E75;   /* primary accent */
  --wp-deep:        #0F6E56;
  --wp-forest:      #085041;
  --wp-midnight:    #04342C;

  /* ── Neutrals ── */
  --wp-parchment:   #F1EFE8;
  --wp-stone:       #D3D1C7;
  --wp-drift:       #888780;
  --wp-slate:       #444441;
  --wp-ink:         #2C2C2A;

  /* ── Amber (complete badge, unsaved indicator) ── */
  --wp-amber:       #FAC775;
  --wp-gold:        #EF9F27;
  --wp-honey:       #BA7517;
  --wp-amber-bg:    #FAEEDA;
  --wp-amber-dark:  #412402;
  --wp-amber-mid:   #854F0B;

  /* ── Lavender (skipped badge) ── */
  --wp-lavender:    #AFA9EC;
  --wp-violet:      #534AB7;
  --wp-indigo:      #26215C;
  --wp-lavender-bg: #EEEDFE;

  /* ── Page surfaces ── */
  --bg:             #F4F2EB;   /* page background */
  --surface:        #FDFCF9;   /* card and row background */
  --border:         #D3D1C7;
  --border-light:   #EBEBDF;

  /* ── Text ── */
  --text-primary:   #2C2C2A;
  --text-secondary: #5F5E5A;
  --text-muted:     #888780;
}
```

To replace the brand teal with a different accent, update `--wp-teal` and the surrounding shades (`--wp-deep`, `--wp-jade`, `--wp-forest`, etc.) to form a coherent scale.

---

## Page Title

The browser tab title is set in `<head>` at line 6:

```html
<title>Waypoint</title>
```

Change `Waypoint` to your team name, project name, or anything else.

---

## Typography

Two fonts are loaded from Google Fonts:
- **Ubuntu** — body text, labels, buttons
- **Ubuntu Mono** — module dates and version stamp

Both are loaded at the top of `<head>`:

```html
<link href="https://fonts.googleapis.com/css2?family=Ubuntu:wght@300;400;500;700&family=Ubuntu+Mono:wght@400;700&display=swap" rel="stylesheet">
```

To use different fonts, replace the Google Fonts URL and update the `font-family` declarations in the `body` rule and any `monospace` rules (look for `'Ubuntu Mono'`):

```css
body {
  font-family: 'Ubuntu', system-ui, sans-serif;
}
```

`system-ui` is the fallback if Google Fonts is unavailable.

---

## Page Width

Content is constrained to `1080px` in both the content layout and the navbar. Both values appear near lines 164 and 169:

```css
.layout { max-width: 1080px; ... }
.navbar { max-width: 1080px; ... }
```

Increase or decrease the value consistently in both declarations to change the overall page width.

---

## Page Background

The overall page background is controlled by `--bg` in the `:root` block:

```css
--bg:      #F4F2EB;   /* page background */
--surface: #FDFCF9;   /* card and row background */
```

Both can be changed independently. `--bg` is the outer parchment tone; `--surface` is the brighter white used for subject cards, milestone rows, and module rows.

---

## Navbar

The entire `<nav>` element is yours to modify. You can replace the logo and wordmark with your own branding, restructure the right-hand controls, add or remove elements, or restyle the bar completely.

The navbar has two sections:

```html
<nav>
  <div class="navbar">

    <!-- Left: logo and wordmark — replace with your own branding -->
    <a class="navbar-logo" href="#">
      <svg ...>...</svg>
      <div class="navbar-wordmark">
        <span class="way">way</span><span class="point">point</span>
      </div>
    </a>

    <!-- Right: controls — add, remove, or rearrange as needed -->
    <div class="navbar-right">
      <!-- file status pill, unsaved indicator, download, theme picker, load YAML -->
    </div>

  </div>
</nav>
```

The `.navbar` CSS rule (around line 167) controls layout, padding, and positioning. Update it alongside any HTML changes.

---

## Themes

The three built-in themes — **Default**, **Minimal**, and **Warm** — each set a group of CSS variables on the `body` element. They control subject header colors, milestone row backgrounds, and module row backgrounds independently of the global palette.

Each theme block looks like this (around lines 52–98):

```css
body.theme-default {
  --theme-subject-bg:         var(--wp-forest);
  --theme-subject-bg-hover:   var(--wp-deep);
  --theme-subject-title:      var(--wp-mist);
  --theme-subject-desc:       var(--wp-jade);
  --theme-subject-pct:        var(--wp-teal);
  --theme-subject-border:     var(--wp-forest);
  --theme-milestone-bg:       var(--wp-mist);
  --theme-milestone-bg-hover: var(--wp-jade);
  --theme-milestone-title:    var(--wp-forest);
  --theme-milestone-border-l: 3px solid var(--wp-teal);
  --theme-module-bg:          var(--surface);
  --theme-module-bg-hover:    var(--bg);
  --theme-module-border-l:    3px solid var(--wp-stone);
}
```

### Modifying an existing theme

Find the `body.theme-*` block you want to change and update the variable values.

### Adding a new theme

1. Add a new CSS block with all the `--theme-*` variables set:
   ```css
   body.theme-yourname {
     --theme-subject-bg:  #...;
     /* ... all other theme variables */
   }
   ```

2. Add `'yourname'` to the `THEMES` array in the JavaScript (search for `const THEMES`):
   ```js
   const THEMES = ['default', 'minimal', 'warm', 'yourname'];
   ```

3. Add a `<div class="theme-option">` entry inside the `#theme-popover` element, following the pattern of the existing options. Include three `.theme-swatch` divs with preview colors, a `.theme-name`, a `.theme-desc`, and the checkmark `<i>` icon.

---

## Status Badge Colors

Module status badges are styled by class name. The rules appear around line 399:

```css
.badge-not_started { background: #E8E6DF;            color: var(--wp-slate);      }
.badge-in_progress { background: var(--wp-jade);     color: var(--wp-midnight);   }
.badge-complete    { background: var(--wp-amber);    color: var(--wp-amber-dark); }
.badge-skipped     { background: var(--wp-lavender); color: var(--wp-indigo);     }
```

Change `background` and `color` directly to restyle any badge. Note that `.badge-in_progress` uses `--wp-jade` and `.badge-complete` uses `--wp-amber` — updating those palette variables in `:root` will affect both the badges and anywhere else those colors appear.

<br>

---

<img align="left" src="../branding/banners/waypoint_banner_lightbg.png" height="64" alt="waypoint">
<div align="right">v1.0.0</div>
<br clear="both">
