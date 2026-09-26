> **Moved.** These assets now live in one repo, split by project:
> https://github.com/souvikb93/framer-assets
>
> This repo is kept so the old Pages URLs keep resolving and so the
> `pre-type-scale` / `type-scale-v1` rollback tags stay reachable.
> **Edit the monorepo, not this one.**

# Streamliner — programme timeline

A twelve-month plan for the Dell Streamliner research and design programme:
seven regional research tracks, five workstreams, and the client checkpoints
between them. One self-contained HTML file, no build step.

**Live:** https://souvikb93.github.io/Stramliner_timeline/

**Framer node:** `ju9AZVRUT` on `/projects/streamliner`

> **The dates are illustrative.** Region names, country lists and interview
> counts are real and match the research map asset (62 interviews, 17 countries,
> 7 regions). The week-by-week schedule is a reconstruction — replace the `s` and
> `e` week numbers in `GROUPS` with the real ones before this goes in front of
> anyone who was on the project.

## Using it in Framer

Embed node → **URL** mode → paste the live URL above → set **Height to Fixed,
700**. URL embeds cannot auto-measure; the file locks its own desktop height with
`@media (min-width:900px){body{min-height:700px}}` so the two agree.

## Editing the plan

Everything lives in two arrays near the top of the script.

```js
const GROUPS=[
 ['Field research by region',[
  //  row label        caption                  [phase, startWeek, endWeek, barLabel, thin?]
  ['North America','USA, Canada · 12',[['disc',2,8,'Interviews'],['disc',8,11,'Follow-ups',1]]],
  …
const MS=[[12,'Interim findings'],[29,'Framework signed off'],…];   // [week, label]
```

- Weeks run `0`–`52`; the month axis is derived, so you never position anything
  in pixels.
- A row can hold any number of bars. Overlapping weeks are the point — that is
  what shows two regions running at once.
- The fifth element marks a bar as **thin** (`1`), used for secondary work like
  follow-up sessions so it reads as subordinate to the main block.
- Phases are keyed in `PH`: `disc`, `syn`, `cc`, `dd`, `vp`.

Then `git commit -am "…" && git push`. Pages redeploys in under a minute; the
Framer node never changes.

## How it reads

A playhead sweeps the year. Bars are dim before their window, solid while
running, and held at partial opacity once passed, so at any moment you can see
what is live, what is finished, and what has not started. The footer names the
tracks currently running — which is where overlap becomes obvious: synthesis
starts in week 8 while four regions are still in the field.

**Show all** drops the playhead and lights the whole plan at once, for when the
question is shape rather than sequence.

## Constraints

- **Fixed desktop height** — Framer measures the embed and writes the value back
  to the node, so a document that changes height makes the page jump.
- **`setTimeout`, not `requestAnimationFrame`** — rAF does not advance under
  headless virtual time, which makes an asset impossible to verify or screenshot
  in CI.
- **Responsive inside the file** — Framer's M (810) and S (390) breakpoints are
  zero-override replicas of L (1200) and share one node height, so all
  responsive behaviour lives here. Below 760px the grid scrolls horizontally at
  a fixed 860px.
- **Reduced motion** respected: the playhead steps slowly, transitions are off,
  content stays readable.
- Phase colours are the shared kit palette, each ≥4.5:1 against white, so white
  bar labels stay legible.

Shared design rules for every asset in this case study:
https://github.com/souvikb93/streamliner-final
