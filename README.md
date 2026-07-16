# Responsive Layouts — Flexbox & Grid Playground

**Week 1 · Frontend Web Development**

Same 3-column pricing section (with header and footer), built twice — once with
Flexbox only, once with CSS Grid only — to compare the two approaches directly.

## Structure

```
Week-1/
│
├── flexbox.html     → pricing section built with Flexbox only
├── grid.html        → the exact same layout, rebuilt with CSS Grid only
├── flexbox.css      → flexbox layout + shared visual styles
├── grid.css         → grid layout + shared visual styles
├── images/          → reserved for screenshots (none needed — no image assets used)
└── README.md        → this file
```

Open `flexbox.html` or `grid.html` directly in a browser — each page links to
the other so you can flip between them. Resize the window below 600px on
either page to see the pricing cards stack into a single column.

## How each version works

**flexbox.html / flexbox.css**
```css
.pricing-row {
  display: flex;
  gap: 24px;
}
.plan { flex: 1 1 0; }
.plan.featured { flex: 1.08 1 0; } /* slightly wider */

@media (max-width: 600px) {
  .pricing-row { flex-direction: column; }
}
```

**grid.html / grid.css**
```css
.pricing-row {
  display: grid;
  grid-template-columns: 1fr 1.08fr 1fr;
  gap: 24px;
}

@media (max-width: 600px) {
  .pricing-row { grid-template-columns: 1fr; }
}
```

Everything else — header, footer, card borders, typography, button styling —
is identical between the two files, so the only real difference on screen is
which engine is doing the column layout.

## Comparison — what was easier / harder

**Flexbox**
Easier to reach for on instinct — one line turns the row into three columns,
and `flex: 1` on each card meant I didn't have to think about sizing at all.
Making the "Growth" card a bit wider took a slightly awkward flex-basis tweak
(`flex: 1.08 1 0`) instead of a clean number, since flex ratios are relative,
not exact — took a bit of trial and error to get the width right. Responsive
stacking was trivial: just flip `flex-direction` to `column` in the media
query.

**CSS Grid**
Defining the three columns up front with `grid-template-columns: 1fr 1.08fr 1fr`
felt more explicit and predictable — the exact proportions are declared in
one place instead of inferred from flex-grow math. Because column widths
live on the parent, not each child, tweaking the featured column's width
meant editing one line instead of hunting through child rules. Stacking on
mobile was just as simple — swap the column list for `1fr`.

**Verdict**
For this exact layout — a fixed number of same-height columns — Grid felt
more precise and easier to reason about, since the column structure is
declared once on the container. Flexbox felt faster to get to "good enough"
but fuzzier when I wanted an exact, deliberate width ratio.

In general: reach for **Flexbox** when content should size itself and flow
in one direction (nav bars, button groups, card content). Reach for **Grid**
when you're defining an actual structure of rows and columns, like this
pricing table.

## Still to do

- [ ] Record a 1–2 min video: show `flexbox.html`, then `grid.html`, and
      resize the browser on both to demonstrate the responsive stacking.
- [ ] Upload the video to LinkedIn, tagging **Neurofive Solutions**.
- [ ] Submit the LinkedIn video link along with this folder.
