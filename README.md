# forking-paths

An interactive, single-file walkthrough of McElreath's **2M7** — the "garden
of forking paths" problem from *Statistical Rethinking*. It answers a Bayesian
question by *counting*, not by formula: you watch every way the data could have
happened, prune the ways that don't match what you saw, and read the posterior
straight off the surviving counts.

Open [`index.html`](index.html) in any browser, or visit the GitHub Pages site.
No build step, no dependencies, no network needed beyond the web fonts.

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

The page is built in the in-house **Tunnel** aesthetic (`tunnel-aesthetic`,
from [`cuddly-lamp`](../cuddly-lamp)): the locked chart-paper palette, the
Fraunces / Public Sans / IBM Plex Mono type, hard edges, a single red `route`
element (the **Next** control that walks the path), amber reserved for the
high-count "winning" branch, and real labels throughout. It carries the
**seeded signature mark** — the small contour-and-route colophon in the
masthead, the default quiet `mark` variant (no caption, no physics labels) —
generated deterministically from this page's seed (`2M7-forking-paths`), so the
page is unmistakably part of the family while its terrain is its own. The loud
`full` figure is reserved for pages actually about terrain or sampling; this is
a counting argument, so it gets the quiet mark.

```
forking-paths/
├─ index.html        ← the walkthrough (self-contained: markup, styles, logic)
├─ tunnel-figure.js  ← vendored seeded signature generator (from cuddly-lamp)
└─ README.md
```

The page is named `index.html` so GitHub Pages serves it at the site root (it
was previously `2M7-forking-paths.html`). The signature figure's seed is fixed
in the page (`data-seed="2M7-forking-paths"`), so the rename doesn't change the
terrain.

The figure generator is a copy of `cuddly-lamp/assets/tunnel-figure.js`; keep it
in step with the source if the design system updates.
