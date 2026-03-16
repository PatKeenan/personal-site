# Personal Website Plan

## Reference Site Analysis: justin.poehnelt.com

### Visual Design
- **Color scheme**: Light neutral background, muted gray borders, warm amber/orange accents
- **Typography**: Sans-serif system fonts for body, monospace for code/timestamps, clear size/weight hierarchy
- **Layout**: Max-width constrained, responsive grid, generous padding and consistent spacing

### Navigation & Features
- Top header: About, Posts, Races + social links (GitHub, LinkedIn, RSS)
- Global search with ⌘K keyboard shortcut
- Tag-based filtering on posts
- RSS feed

### Content Types
- **Homepage**: Short intro + recent posts list
- **Posts** (`/posts/`): Chronological feed with title, description, date, tags — 9+ years of content
- **About**: Professional bio, career history, personal interests
- **Tags** (`/tags/`): All tags with post counts

### Technical Stack (Reference Site)
- Built with **SvelteKit** (evidenced by `/_app/immutable/` asset paths)
- Cloudflare CDN
- Google Analytics
- Schema.org JSON-LD structured data

---

## Our Implementation Plan

### Chosen Stack

| Concern | Choice | Rationale |
|---|---|---|
| Framework | **Astro** | SSG-first, excellent Content Collections API, ships zero JS by default, large ecosystem |
| Styling | **Tailwind CSS v4** + `@tailwindcss/typography` | Utility-first, v4 is CSS-native (no config file), prose plugin handles blog post styling |
| Content | **Markdown / MDX** via Astro Content Collections | Type-safe frontmatter with Zod, co-located with source |
| Search | **Pagefind** | Runs at build time, no server needed, supports ⌘K command palette |
| RSS | `@astrojs/rss` | Official Astro integration, trivial to add |
| Sitemap | `@astrojs/sitemap` | Auto-generated at build |
| Deployment | **Vercel** | First-class Astro support, free tier, preview deployments on PRs |

### Architecture

```
src/
├── content/
│   ├── config.ts          # Zod schemas for Content Collections
│   └── posts/             # Markdown blog posts
│       └── *.md
├── layouts/
│   ├── BaseLayout.astro    # <html>, head, meta, nav, footer
│   └── PostLayout.astro   # Extends Base, adds prose wrapper
├── pages/
│   ├── index.astro        # Homepage: intro + recent posts
│   ├── about.astro        # About page
│   ├── posts/
│   │   ├── index.astro    # Post listing with tag filter
│   │   └── [slug].astro   # Individual post
│   ├── tags/
│   │   ├── index.astro    # All tags page
│   │   └── [tag].astro    # Posts filtered by tag
│   ├── rss.xml.ts         # RSS feed
│   └── sitemap-index.xml  # Auto via @astrojs/sitemap
└── components/
    ├── Nav.astro
    ├── Footer.astro
    ├── PostCard.astro     # Card used in listing pages
    └── Search.astro       # Pagefind ⌘K search component
```

---

## Implementation Phases

### Phase 1 — MVP (this ticket)
- [x] Scaffold Astro project
- [x] Install & configure Tailwind CSS v4 + typography plugin
- [x] Content Collections schema (`posts` with title, description, date, tags, draft)
- [x] Homepage with intro and recent 5 posts
- [x] Post listing page (`/posts/`)
- [x] Individual post page (`/posts/[slug]`)
- [x] About page
- [x] Navigation + Footer
- [x] RSS feed (`/rss.xml`)
- [x] Sitemap
- [x] 2–3 sample blog posts
- [x] Deploy to Vercel

### Phase 2 — Search & Tags
- [ ] Tags listing page (`/tags/`)
- [ ] Tag filter page (`/tags/[tag]`)
- [ ] Pagefind integration (⌘K search)

### Phase 3 — Polish
- [ ] Dark mode toggle
- [ ] Open Graph / Twitter card meta tags
- [ ] Reading time estimate on posts
- [ ] Prev/Next post navigation

### Phase 4 — Content & SEO
- [ ] Schema.org JSON-LD (Person + WebSite on homepage)
- [ ] Canonical URLs
- [ ] `robots.txt`
- [ ] First real blog posts

### Phase 5 — Extras (optional)
- [ ] MDX support for interactive components in posts
- [ ] Image optimization with `@astrojs/image`
- [ ] Analytics (Plausible or Fathom — privacy-first)
