---
title: Why Static Sites Still Win on Performance
description: A look at why statically generated sites consistently outperform server-rendered alternatives on core web vitals.
date: 2026-03-16
category: Web Development
tags: [web, performance, astro]
---

Static sites get dismissed as "too simple" for real applications. In practice, that simplicity is often their biggest advantage.

## What Makes Static Fast

A static site is just files: HTML, CSS, maybe some JavaScript. When a user visits a page, the server delivers a pre-built HTML file directly. No database queries. No server-side rendering. No waiting.

The latency is bounded by how fast your CDN can deliver a file — usually under 50ms globally if you're using a modern edge network.

## Core Web Vitals

Google's [Core Web Vitals](https://web.dev/vitals/) measure three things that actually affect user experience:

- **LCP** (Largest Contentful Paint): How quickly the main content loads
- **CLS** (Cumulative Layout Shift): How stable the layout is while loading
- **INP** (Interaction to Next Paint): How responsive the page is to input

Static sites naturally excel at LCP and CLS because the HTML is fully formed before it reaches the browser. There's no hydration flash, no skeleton screens, no layout shift while data loads.

## When Static Falls Short

Static generation isn't the right tool for everything. Pages that need real-time data (stock prices, live inventory) or that are user-specific (authenticated dashboards) are better served by server-side rendering or client-side fetching.

But for content sites — blogs, docs, marketing pages — static is almost always the right call.

## The Astro Approach

Astro's island architecture gives you the best of both: a statically generated base with opt-in interactivity for the parts that need it. You pay the JavaScript cost only where it matters.

This site is built with Astro. The search works via Pagefind — a static search index built at compile time, delivered as static files, no server required.
