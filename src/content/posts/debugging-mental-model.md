---
title: Debugging Is a Mental Model Problem
description: Most bugs aren't logic errors — they're gaps between how you think the system works and how it actually works.
date: 2026-03-16
category: Engineering
tags: [engineering, debugging, practices]
---

When I get stuck on a bug, it's almost never because I don't know how to code. It's because my mental model of the system is wrong.

## The Real Error

You look at a bug and think: "This code should work. Why doesn't it?" That thought is the error. The code is telling you exactly what it does. You just expected something different.

The fix isn't in the code — it's in updating your mental model until your expectation matches reality.

## A Framework for Debugging

Here's how I approach bugs that have me stuck:

1. **State what you think is happening.** Write it down. "I believe X is causing Y because Z." Be specific.

2. **Test your assumption.** Add a log, a breakpoint, an assertion — whatever lets you observe the actual state. Don't guess. Measure.

3. **Compare.** If the observed state matches your assumption, your model was right and the bug is elsewhere. If it doesn't match, you found the gap. Update your model and repeat.

This is just the scientific method applied to code. It sounds obvious, but most debugging sessions skip step one — the explicit statement of the assumption being tested.

## Rubber Duck Debugging Works Because...

...explaining a problem to someone (or something) forces you to articulate your mental model. The moment you say "it should do X" to the rubber duck, you're setting up the hypothesis. The duck doesn't need to respond. The act of stating it clearly is enough.

## The Faster Path

The fastest path to fixing a bug is often:

1. Stop assuming you know what's wrong.
2. Find the smallest reproducible case.
3. Instrument aggressively.
4. Trust the output, not your intuition.

Experience helps — you build a library of failure modes. But the method stays the same.
