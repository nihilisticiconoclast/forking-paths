# forking-paths

An interactive walkthrough of McElreath's **2M7** — the "garden of forking
paths" problem from *Statistical Rethinking*. It answers a Bayesian question by
*counting*, not by formula: you watch every way the data could have happened,
prune the ways that don't match what you saw, and read the posterior straight off
the surviving counts.

Open [`index.html`](index.html) in any browser, or visit the GitHub Pages site.
It is a single page that steps through the argument — candidates → observe black
→ observe white → posterior — one column of the count at a time. No build step;
the shared Tunnel assets and the web fonts are linked from the CDN.

## The problem

Three cards — one black/black, one black/white, one white/white. You draw a
card and a **black** face shows. You set it aside, draw a second card from the
two that remain, and a **white** face shows. What's the chance the first card is
black on its hidden side?

## The count

| first card | ways to show black (1st draw) | × white faces on the two remaining | paths |
|------------|:-----------------------------:|:----------------------------------:|:-----:|
| **BB**     | 2                             | BW + WW → 1 + 2 = 3                 | **6** |
| **BW**     | 1                             | BB + WW → 0 + 2 = 2                 | **2** |
| **WW**     | 0 (ruled out immediately)     | —                                  | **0** |

Eight paths survive; six of them start from a BB card. The hidden side is black
exactly when the first card is BB, so the answer is `6 : 2 : 0 → 6/8 = 0.75`.
That is identical to what Bayes' theorem returns — probabilities are just these
counts rescaled to sum to one. The four steps in the page (candidates →
observe black → observe white → posterior) walk that table one column at a time.

## Design

Built in the in-house **Tunnel** aesthetic (`tunnel-aesthetic`, from
[`cuddly-lamp`](https://github.com/nihilisticiconoclast/cuddly-lamp)): the locked
chart-paper palette and Fraunces / Public Sans / IBM Plex Mono type, hard edges,
a single red `route` element (the **Next** control that walks the path), and
amber reserved for the high-count "winning" branch. The locked layer and the
signature generator are **linked from cuddly-lamp's CDN, never inlined**, so a
design-system update propagates here automatically. The page carries the fixed
house mark in the masthead and a per-page doodle in the margin, both generated
deterministically from this page's seed (`2M7-forking-paths`), so the page is
unmistakably part of the family while its terrain is its own.

```
forking-paths/
├─ index.html   ← the walkthrough: markup, styles, and logic (Tunnel assets via CDN)
└─ README.md
```

The page is named `index.html` so GitHub Pages serves it at the site root (it
was previously `2M7-forking-paths.html`). Its signature seed is fixed in the page
(`data-seed="2M7-forking-paths"`), so the rename doesn't change the terrain.
