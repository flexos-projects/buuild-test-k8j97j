---
id: patterns-base
title: "Base Patterns"
type: design
subtype: patterns
status: active
sequence: 3
description: "Structural CSS vocabulary — component patterns for prototypes and builds"
tags: [design, patterns, css, components]
relatesTo: [design/001-tokens-design-system.md, prototype/sitemap.md]
createdAt: "{{created_at}}"
---

<flex_block type="instructions">
This file defines the structural CSS class vocabulary that all prototypes
and builds must use. These are not individual token values — they are
component patterns that APPLY tokens. The builder AI extends these patterns
rather than inventing from scratch. This is the minimum floor of quality.

All values reference var() tokens from design/001-tokens-design-system.md.
All patterns are structurally complete but visually neutral until tokens
give them personality.
</flex_block>

# Base Patterns

The structural CSS vocabulary for the project. Every prototype page and production component builds on these patterns. All values reference `var()` design tokens — never raw hex or pixel values.

## Layout

The page structure uses a max-width container with responsive sections.

```css
.page {
  max-width: var(--content-max-width);
  margin: 0 auto;
}

.section {
  padding: var(--space-16) var(--space-4);
}

.section + .section {
  border-top: 1px solid var(--color-border);
}
```

## Grids

Responsive auto-fit grids that adapt to available space. No breakpoint media queries needed — the `minmax()` pattern handles responsiveness.

```css
.grid { display: grid; gap: var(--space-4); }
.grid-2 { grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); }
.grid-3 { grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); }
.grid-4 { grid-template-columns: repeat(auto-fit, minmax(160px, 1fr)); }
```

## Navigation

Sticky top nav with blur backdrop, horizontal scroll on mobile. Brand on the left, links in the middle, actions on the right.

```css
.nav {
  position: sticky;
  top: 0;
  z-index: 100;
  background: var(--nav-bg);
  backdrop-filter: blur(12px);
  border-bottom: 1px solid var(--color-border);
}

.nav-link {
  font-size: var(--font-size-xs);
  color: var(--color-text-secondary);
  border-bottom: 2px solid transparent;
}

.nav-link.active {
  color: var(--color-primary);
  border-bottom-color: var(--color-primary);
}
```

## Buttons

Three variants: primary (filled), outline (bordered), ghost (text only). All respect minimum touch targets on mobile.

```css
.btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  min-height: var(--touch-target-min);
  padding: var(--space-2) var(--space-6);
  font-size: var(--font-size-sm);
  font-weight: var(--font-weight-semibold);
  border-radius: var(--radius-md);
  transition: all var(--transition-fast);
}

.btn-primary {
  background: var(--color-primary);
  color: var(--color-on-primary);
}

.btn-outline {
  border: 1.5px solid var(--color-border);
  color: var(--color-text-primary);
}

.btn-ghost {
  color: var(--color-text-secondary);
}
```

Button states: hover darkens primary, hover highlights outline border, disabled reduces opacity. Small variant (`.btn-sm`) reduces to 32px height.

## Hero

Full-width hero section with centered content: badge, title, subtitle, action buttons, optional stats row.

```css
.hero {
  padding: var(--space-24) var(--space-4) var(--space-16);
  text-align: center;
}

.hero-title {
  font-size: var(--font-size-4xl);
  font-weight: var(--font-weight-bold);
  line-height: var(--line-height-tight);
}

.hero-subtitle {
  font-size: var(--font-size-lg);
  color: var(--color-text-secondary);
  max-width: 640px;
  margin: 0 auto;
}
```

## Cards

Surface-colored containers with border, radius, and subtle hover elevation. Used for feature cards, content items, team members.

```css
.card {
  background: var(--color-surface);
  border: 1px solid var(--color-border);
  border-radius: var(--radius-lg);
  padding: var(--space-6);
  transition: box-shadow var(--transition-base), transform var(--transition-base);
}

@media (hover: hover) {
  .card:hover {
    box-shadow: var(--shadow-md);
    transform: translateY(-2px);
  }
}
```

Cards use `@media (hover: hover)` to prevent sticky hover states on touch devices.

## Forms

Labels above inputs, minimum touch-target height, primary-colored focus rings, error messages below fields.

```css
/* Input base */
input, textarea, select {
  min-height: var(--touch-target-min);
  padding: var(--space-2) var(--space-3);
  border: 1px solid var(--color-border);
  border-radius: var(--radius-md);
  font-size: var(--font-size-base); /* 16px prevents iOS zoom */
  background: var(--color-bg);
  color: var(--color-text-primary);
}

/* Focus state */
input:focus, textarea:focus, select:focus {
  outline: none;
  border-color: var(--color-primary);
  box-shadow: 0 0 0 2px var(--color-primary-light);
}

/* Error state */
.field-error input {
  border-color: var(--color-error);
}

.error-message {
  font-size: var(--font-size-sm);
  color: var(--color-error);
  margin-top: var(--space-1);
}
```

## Toast Notifications

Fixed-position feedback element at bottom-center. Slides up on show, fades out.

```css
.toast {
  position: fixed;
  bottom: var(--space-6);
  left: 50%;
  transform: translateX(-50%) translateY(100px);
  background: var(--color-text-primary);
  color: var(--color-bg);
  font-family: var(--font-mono);
  font-size: var(--font-size-xs);
  padding: var(--space-2) var(--space-4);
  border-radius: var(--radius-full);
  opacity: 0;
  transition: all var(--transition-base);
  z-index: 200;
}

.toast.show {
  opacity: 1;
  transform: translateX(-50%) translateY(0);
}
```

## Animation Keyframes

Standard motion primitives: fade, slide (from top/bottom/left/right), scale.

```css
@keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }
@keyframes slideUp { from { transform: translateY(8px); opacity: 0; } to { transform: translateY(0); opacity: 1; } }
@keyframes slideDown { from { transform: translateY(-8px); opacity: 0; } to { transform: translateY(0); opacity: 1; } }
@keyframes scaleIn { from { transform: scale(0.95); opacity: 0; } to { transform: scale(1); opacity: 1; } }
```

## Theme Switching

Light mode is default. Dark mode activates via `data-theme="dark"` on `<html>`. OS preference is respected as fallback. Theme toggle button saves preference to `localStorage`.

```css
/* Light is default via :root */
:root, [data-theme="light"] { /* light tokens */ }

/* Dark via attribute */
[data-theme="dark"] { /* dark tokens */ }

/* OS fallback (no attribute set) */
@media (prefers-color-scheme: dark) {
  :root:not([data-theme]) { /* dark tokens */ }
}
```

## Responsive Breakpoint

Single mobile breakpoint at 640px. Below: stack layouts, reduce hero size, collapse type rows. Above: multi-column grids, larger padding.

```css
@media (max-width: 640px) {
  .hero-title { font-size: var(--font-size-3xl); }
  .hero { padding: var(--space-12) var(--space-4) var(--space-8); }
  .section { padding: var(--space-8) var(--space-4); }
}
```

## Hover Guards

All hover effects wrapped in `@media (hover: hover)` to prevent sticky hover states on touch devices. This is a hard requirement for all interactive patterns.
