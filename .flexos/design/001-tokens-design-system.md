---
id: design-system
title: "Design System"
type: design
subtype: tokens
status: active
sequence: 2
description: "Core design tokens — colors, typography, spacing"
tags: [design, tokens, core]
createdAt: "{{created_at}}"
---

<flex_block type="instructions">
This file contains the project's core design tokens. These values are
used to generate prototype CSS (prototype/shared/tokens.css) and inform
all visual decisions. Update these tokens to change the project's look.

Token blocks use CSS custom property names as keys. The provisioning
system derives the initial color palette from the project's theme color.
</flex_block>

## Color Tokens — Light Mode

<flex_block type="tokens">
{
  "category": "colors",
  "mode": "light",
  "tokens": {
    "--color-primary": "#8b5cf6",
    "--color-primary-dark": "#7c3aed",
    "--color-primary-light": "#a78bfa",
    "--color-accent": "#06b6d4",
    "--color-success": "#22c55e",
    "--color-warning": "#f59e0b",
    "--color-error": "#ef4444",
    "--color-bg": "#ffffff",
    "--color-surface": "#f8fafc",
    "--color-elevated": "#ffffff",
    "--color-border": "#e2e8f0",
    "--color-text-primary": "#0f172a",
    "--color-text-secondary": "#64748b",
    "--color-text-tertiary": "#94a3b8"
  }
}
</flex_block>

## Color Tokens — Dark Mode

<flex_block type="tokens">
{
  "category": "colors",
  "mode": "dark",
  "tokens": {
    "--color-primary": "#a78bfa",
    "--color-primary-dark": "#8b5cf6",
    "--color-primary-light": "#c4b5fd",
    "--color-accent": "#22d3ee",
    "--color-success": "#4ade80",
    "--color-warning": "#fbbf24",
    "--color-error": "#f87171",
    "--color-bg": "#0f172a",
    "--color-surface": "#1e293b",
    "--color-elevated": "#334155",
    "--color-border": "#334155",
    "--color-text-primary": "#f1f5f9",
    "--color-text-secondary": "#94a3b8",
    "--color-text-tertiary": "#64748b"
  }
}
</flex_block>

### Theme Switching

The prototype supports both light and dark modes via a `data-theme` attribute on `<html>`. Setting `data-theme="dark"` activates dark tokens. If no attribute is set, the OS preference (`prefers-color-scheme: dark`) is used as a fallback. A toggle button in the nav lets users switch manually — the preference is saved to `localStorage`.

### Color Usage

- **Primary** — CTAs, links, active states, key interactive elements
- **Accent** — Secondary highlights, badges, supplementary actions
- **Semantic** (success/warning/error) — Feedback states, alerts, validation
- **Surface/Elevated** — Card backgrounds, modals, layered UI
- **Text tiers** — Primary for headings and body, secondary for labels, tertiary for hints

## Typography Tokens

<flex_block type="tokens">
{
  "category": "typography",
  "tokens": {
    "--font-heading": "Inter, system-ui, -apple-system, sans-serif",
    "--font-body": "Inter, system-ui, -apple-system, sans-serif",
    "--font-mono": "JetBrains Mono, ui-monospace, monospace",
    "--font-size-xs": "0.75rem",
    "--font-size-sm": "0.875rem",
    "--font-size-base": "1rem",
    "--font-size-lg": "1.125rem",
    "--font-size-xl": "1.25rem",
    "--font-size-2xl": "1.5rem",
    "--font-size-3xl": "2rem",
    "--font-size-4xl": "2.5rem",
    "--font-weight-normal": "400",
    "--font-weight-medium": "500",
    "--font-weight-semibold": "600",
    "--font-weight-bold": "700",
    "--line-height-tight": "1.25",
    "--line-height-normal": "1.5",
    "--line-height-relaxed": "1.75"
  }
}
</flex_block>

## Spacing & Layout Tokens

<flex_block type="tokens">
{
  "category": "spacing",
  "tokens": {
    "--space-1": "0.25rem",
    "--space-2": "0.5rem",
    "--space-3": "0.75rem",
    "--space-4": "1rem",
    "--space-6": "1.5rem",
    "--space-8": "2rem",
    "--space-12": "3rem",
    "--space-16": "4rem",
    "--space-24": "6rem",
    "--radius-sm": "0.375rem",
    "--radius-md": "0.5rem",
    "--radius-lg": "0.75rem",
    "--radius-xl": "1rem",
    "--radius-full": "9999px",
    "--shadow-sm": "0 1px 2px rgba(0,0,0,0.05)",
    "--shadow-md": "0 4px 6px rgba(0,0,0,0.07)",
    "--shadow-lg": "0 10px 15px rgba(0,0,0,0.1)",
    "--content-max-width": "1200px",
    "--sidebar-width": "240px",
    "--bottom-nav-height": "56px",
    "--touch-target-min": "44px",
    "--transition-fast": "0.15s ease",
    "--transition-base": "0.2s ease",
    "--transition-slow": "0.3s ease"
  }
}
</flex_block>

# Design System

## Design Vision

- **Style:** Modern, clean, minimal
- **Vibe:** Professional yet approachable
- **Dark mode:** Both (light default, dark via toggle and OS preference)

## Typography

- **Headings:** Inter — clean, geometric sans-serif
- **Body:** Inter — highly readable at all sizes
- **Mono:** JetBrains Mono — for code and data display
- **Minimum body size:** 16px (prevents mobile zoom on input focus)

## Spacing Scale

Based on 0.25rem increments. Use `--space-4` (1rem) as the base unit.
Cards and sections use `--space-6` to `--space-8` padding.
