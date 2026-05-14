# Design md

# 🪙 Design Tokens

## Colors

```css
:root {
  /* Brand */
  --brand-blue:     #3f75f5;   /* CTAs, links, active states, accents */

  /* Neutrals */
  --neutral-950:    #0a0a0a;   /* Primary text, dark backgrounds */
  --neutral-800:    #1f2937;   /* Body text */
  --neutral-600:    #4b5563;   /* Secondary text, borders */
  --neutral-400:    #9ca3af;   /* Placeholder, muted text */
  --neutral-200:    #e5e7eb;   /* Light borders */
  --neutral-100:    #f3f4f6;   /* Light backgrounds */
  --neutral-50:     #f9fafb;   /* Subtle / off-white backgrounds */
  --white:          #ffffff;   /* Primary background */
}
```

**Color Rules:**

- Backgrounds alternate: `--white` ↔ `--neutral-50` only
- `--neutral-950` can be used for dark section backgrounds when needed
- `--brand-blue` reserved for CTAs, links, active states, small accents
- Never use blue as a section background fill

---

## Typography

```css
:root {
  --font-heading: "PP Monument Extended Black", system-ui, sans-serif;
  --font-body:    'Roboto', sans-serif;
}
```

> ⚠️ [PP Monument font file](https://www.notion.so/PP-Monument-Extended-Black-28b7cf9e26b881868d95f29473b5bb58?pvs=21)
> 

| Role | Size | Line Height | Letter Spacing | Transform |
| --- | --- | --- | --- | --- |
| H1 | 64px | 70px | -3.2px | uppercase |
| Section Title | 24px | 26px | -0.5px | uppercase |
| Body Large | 18px | 1.6 | — | — |
| Body Default | 16px | 1.6 | — | — |
| Label / Caption | 12px | — | +0.6px | uppercase |

**Rules:**

- All headings: PP Monument Extended Black, UPPERCASE
- Body copy: Roboto, regular weight, generous line-height
- Labels / captions: PP Monument, tracked out (+0.6px)
- Avoid long body paragraphs (3–4 lines max)

---

## Spacing & Layout

```css
.container {
  max-width: 1440px;
  margin: 0 auto;
  padding: 0 53px;
}

--read-width:      760px;    /* text-heavy sections */
--section-desktop: 120px;   /* section top / bottom padding */
--section-mobile:  72px;
```

---

## Border Radius

```css
:root {
  --radius-full: 999px;   /* Buttons (pill shape), pills, chips */
  --radius-xl:   24px;    /* Cards, large panels */
  --radius-md:   8px;     /* Small UI elements, inputs */
}
```

---

# 🧩 Components

## Buttons

| Class | Background | Text | Border | Hover |
| --- | --- | --- | --- | --- |
| `.btn` | `var(--neutral-950)` | `var(--white)` | none | `opacity: 0.8` |
| `.btn-brand` | `var(--brand-blue)` | `var(--white)` | none | `opacity: 0.8` |
| `.btn-outline` | transparent | `var(--neutral-800)` | 1px solid | `opacity: 0.8` |
| `.btn-cta-white` | `var(--white)` | `var(--neutral-950)` | none | `opacity: 0.9` |

> 除 `.btn-cta-white` 外，其他 buttons 共用通用 hover `.btn:hover { opacity: 0.8 }`。
> 

```css
.btn {
  height: 52px;
  padding: 0 32px;
  border-radius: var(--radius-full);
  font-family: var(--font-body);
  font-weight: 700;
  font-size: 16px;
  transition: opacity 0.2s;
}
```

**States**

| State | Effect |
| --- | --- |
| Default | Solid background |
| Hover | `opacity: 0.8` (0.9 for `.btn-cta-white`), `cursor: pointer` |
| Active | `transform: translateY(-1px)`, slightly darker background |
| Disabled | `opacity: 0.5`, `cursor: not-allowed` |

---

## Pills

[https://www.figma.com/design/Pdk2JtwKcmLuLfEeHiW5HH](https://www.figma.com/design/Pdk2JtwKcmLuLfEeHiW5HH)

```css
.pill {
  height: 32px;
  padding: 0 20px;
  border-radius: var(--radius-full);
  font-family: var(--font-body);
  font-weight: 600;
  font-size: 12px;
}
```

---

## Cards

[https://www.figma.com/design/Pdk2JtwKcmLuLfEeHiW5HH](https://www.figma.com/design/Pdk2JtwKcmLuLfEeHiW5HH)

```css
.card {
  background: var(--white);
  border: 1px solid var(--neutral-200);
  border-radius: var(--radius-xl);   /* 24px */
  padding: 32px 40px;
  box-shadow: 0 2px 12px rgba(0,0,0,0.04);
}
```

Use cards sparingly. Prefer spacing + typography over containers.

---

## Logo Grid

[https://www.figma.com/design/Pdk2JtwKcmLuLfEeHiW5HH](https://www.figma.com/design/Pdk2JtwKcmLuLfEeHiW5HH)

```css
.logo-grid img {
  filter: grayscale(100%) opacity(0.5);
  transition: filter 200ms ease;
}
.logo-grid img:hover { filter: none; }
```

---

## Stats / Metrics

[https://www.figma.com/design/Pdk2JtwKcmLuLfEeHiW5HH](https://www.figma.com/design/Pdk2JtwKcmLuLfEeHiW5HH)

```css
.stat-number {
  font-family: var(--font-heading);
  font-size: 64px;
  line-height: 70px;
  letter-spacing: -3.2px;
  text-transform: uppercase;
  color: var(--neutral-950);
}
.stat-label {
  font-size: 12px;
  color: var(--neutral-400);
  margin-top: 8px;
  letter-spacing: 0.6px;
  text-transform: uppercase;
}
```

Max 4 items per row. Vertical `1px --neutral-200` dividers between items.

---

# 📐 Layout Patterns

## Two-Column Section

```
Left (5/12):   heading + supporting copy
Right (7/12):  visual, UI mockup, or content list
gap:           80px desktop / 40px mobile
```

## Three-Column Cards

```
cols:     3 desktop / 1 mobile
gap:      24–32px
style:    border-radius: --radius-xl, border: 1px --neutral-200
```

## Stat Row

```
layout:   flex, justify-content: space-between
items:    3–4 max
bg:       --neutral-50
padding:  64px top/bottom
divider:  1px solid --neutral-200 (vertical, between each item)
```

## Horizontal Step / Process

```
3 numbered steps (01 / 02 / 03)
connected by a thin horizontal line
label + short description per step
style: infographic — not a bulleted list
```

---