---
title: Why Astro Content Collections Are Great for Blogs
description: A quick look at how Astro's Content Collections feature makes managing blog posts type-safe and painless.
date: 2026-03-16
category: Tutorial
tags: [astro, typescript, web]
---

One of the best features in Astro is [Content Collections](https://docs.astro.build/en/guides/content-collections/). If you're building a blog or any site with structured Markdown content, it's worth understanding why.

## The Problem with Plain Markdown Imports

Before Content Collections, you'd import Markdown files directly:

```js
const posts = await Astro.glob('../posts/*.md');
```

This works, but there's no guarantee that a post has a `title` field, or that `date` is actually a valid date. You'd find out at runtime (or worse, in production).

## Content Collections: Type-Safe Content

With Content Collections, you define a schema using [Zod](https://zod.dev):

```ts
// src/content/config.ts
import { defineCollection, z } from 'astro:content';

const posts = defineCollection({
  schema: z.object({
    title: z.string(),
    description: z.string(),
    date: z.coerce.date(),
    tags: z.array(z.string()).default([]),
  }),
});

export const collections = { posts };
```

Now Astro validates every Markdown file in `src/content/posts/` against this schema at build time. Missing a required field? Build fails with a clear error. Wrong type? Same.

## Querying Collections

```ts
import { getCollection } from 'astro:content';

const posts = await getCollection('posts', ({ data }) => !data.draft);
const sorted = posts.sort((a, b) => b.data.date.valueOf() - a.data.date.valueOf());
```

Clean, typed, and straightforward.

## The Result

You get IDE autocomplete on `post.data.title`, build-time validation, and a simple mental model: your content directory *is* your schema. No CMS required.
