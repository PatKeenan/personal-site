---
title: First Look at Tailwind CSS v4
description: Tailwind CSS v4 drops the JavaScript config file in favor of pure CSS configuration. Here's what changed and why it matters.
date: 2026-03-16
category: Tutorial
tags: [css, tailwind, web]
---

Tailwind CSS v4 is a ground-up rewrite that changes how you configure and use the framework. The biggest shift: **no more `tailwind.config.js`**.

## CSS-Native Configuration

In v4, configuration moves into your CSS file:

```css
@import "tailwindcss";

@theme {
  --font-display: "Inter", sans-serif;
  --color-brand: oklch(60% 0.2 250);
}
```

That's it. No JavaScript, no separate config file, no build tool plugin configuration beyond adding the Vite plugin.

## The Vite Plugin

Instead of PostCSS, v4 ships a Vite plugin:

```js
// vite.config.js (or astro.config.mjs)
import tailwindcss from '@tailwindcss/vite';

export default {
  plugins: [tailwindcss()]
};
```

This makes the build significantly faster because Tailwind can work as a native Vite transform rather than going through PostCSS.

## What I Like

1. **Fewer config files** — One less thing to maintain
2. **CSS variables everywhere** — All design tokens become CSS custom properties, usable in any CSS
3. **Faster builds** — The new engine (Oxide, written in Rust) is dramatically faster

## The Catch

The plugin ecosystem needs to catch up. Some community plugins (like `@tailwindcss/typography`) have v4-compatible versions but the API has changed. Worth checking before upgrading.

Overall, v4 feels like a mature version of the framework: fewer moving parts, better performance, and more aligned with platform standards.
