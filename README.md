# MTB Annual Maintenance Cost Calculator

**Post Millennium Renaissance — Interactive Tool**
[postmillenniumrenaissance.com](https://postmillenniumrenaissance.com)

An interactive, single-file calculator that helps mountain bikers estimate their annual maintenance spend. Adjust cost dials for every major service category, set your own replacement intervals, and use the Ride Worksheet to get ballpark suggestions based on how you actually ride.

Live: [postmillennium-mtb.github.io/maintenance-mtb](https://postmillennium-mtb.github.io/maintenance-mtb/)

---

## What it does

- **Cost dials** for every major service category — suspension, drivetrain, consumables, and ancillary
- **Clickable interval badges** on chain, cassette, chainring and pivot bearings to cycle between 12 / 24 / 36 month replacement schedules
- **Annualized math** — every line item is converted to a per-year cost regardless of its service interval, so the grand total is always apples-to-apples
- **Semicircle gauge** showing Budget / Typical / Premium zones at a glance
- **"Where it goes" breakdown bar** showing the proportion of spend across four categories
- **Ride Worksheet** — a collapsible section where you enter your riding volume (XC rides/week, miles/ride, enduro rides, and bike park days, which can be 0) and the tool suggests how many tires, brake pad sets, rotors, chains per year, and sealant refills you're likely to burn through per year
- **Apply to dials** button — pushes all five worksheet suggestions into the dials: tire / pad / rotor quantities, the sealant dial (refills × $25), and the chain interval (chains/yr snapped to 12 / 24 / 36 months). Each value is clamped to its dial's range (max 7 tires, 12 pad sets, 4 rotors)
- **Share and print icons** — Lucide paper-plane (share) and printer icon buttons sit under the PMR badge at the top. Share turns into a check mark with a "Link copied!" note for 2 seconds. Both are named by `aria-label`, 44px touch targets, and hidden on the printout
- **Share link** — the paper-plane button copies a link to postmillenniumrenaissance.com/maintenance/ with your settings in the URL hash (`#s=…`). Links in the old `?s=` format still load. Malformed values fall back to defaults and out-of-range values are clamped
- **E-bike battery toggle** — adds a $25/yr reserve for eventual battery replacement; off by default for analog bikes
- **Reset to defaults** button

---

## Service categories

| Category | Line items |
|---|---|
| Suspension & Pivots | Front suspension service, rear suspension service, dropper service, pivot bearings |
| Drivetrain | Chain, cassette, chainring (all with adjustable intervals), e-bike battery reserve |
| Ongoing Consumables | Chain lube/wax, tubeless sealant, tires, brake pads, brake rotors |
| Ancillary | Tire plugs, quick links, UDH hangers, misc. |

---

## Cost ranges and defaults

All costs are in USD. Ranges reflect the realistic spread across budget and premium parts/labor.

| Item | Range | Default | Interval |
|---|---|---|---|
| Front suspension service | $110–$165 | $135 | Annual* |
| Rear suspension service | $130–$200 | $150 | Annual* |
| Dropper service | $50–$100 | $75 | Annual* |
| Pivot bearings | $50–$260 | $150 | 24 months (adjustable) |
| Chain | $50–$100 | $75 | 24 months |
| Cassette | $75–$500 | $175 | 24 months |
| Chainring | $20–$100 | $45 | 36 months |
| Battery wear & tear | $25/yr | off | Annual (toggle) |
| Chain lube or wax | $30–$100 | $50 | Annual |
| Tubeless sealant | $25–$100 | $50 | Annual* |
| Tire (each) | $50–$110 | $75 | Per unit |
| Brake pads (per set) | $15–$50 | $25 | Per unit |
| Brake rotor (each) | $20–$100 | $50 | Per unit |
| Ancillary | $10–$500 | $50 | Annual* |

*Interval assumed — not specified by the user. See note in the tool footer.

**Default grand total at baseline settings: $975/yr (~$81/mo)**

---

## Ride Worksheet — wear model

The worksheet converts riding volume into suggested replacement quantities using a simple mileage-based wear model.

**Inputs**
- XC/trail: rides per week (1–7), miles per ride (1–50)
- Enduro/aggressive: rides per week (0–7), miles per ride (1–50)
- Bike park days this season (0–50)

**Assumptions** (all are named constants at the top of the wear model in `index.html`; change both together)

| Constant | Value | Meaning |
|---|---|---|
| `WEEKS_PER_SEASON` | 30 | Weeks ridden per year; turns rides/week into yearly trail miles |
| `PARK_DAY_TRAIL_RIDES` | 3 | A bike park day counts as this many average trail rides of mileage |
| `PARK_TIRE_SEVERITY` | 1.6× | Park miles wear tires faster than trail miles (cornering load) |
| `PARK_PAD_SEVERITY` | 2× | ...brake pads (sustained braking) |
| `PARK_ROTOR_SEVERITY` | 1.5× | ...rotors (heat) |
| `REAR_TIRE_LIFE_MI` / `FRONT_TIRE_LIFE_MI` | 800 / 1,600 mi | Front lasts ~2× the rear; tires/yr is the sum of both |
| `PAD_LIFE_MI` × `BRAKE_COUNT` | 1,000 mi × 2 | Miles per pad set on one brake; the bike has a front and a rear |
| `ROTOR_LIFE_MI` × `ROTOR_COUNT` | 4,000 mi × 2 | Miles per rotor; front and rear wear in parallel |
| `CHAIN_LIFE_MI` | 2,000 mi | Miles per chain; gives chains/yr (shown to one decimal) and the interval Apply sets |
| `SEALANT_LIFE_MI` / `MIN_SEALANT_REFILLS` | 1,200 mi / 2 per yr | Mileage-based refills, with a floor because sealant also dries out with time |
| `SEALANT_REFILL_COST` | $25 | Converts refills into the sealant dial ($50 default = 2 × $25) |

Chains and sealant use the same tire-severity miles (park miles × 1.6).

These are ballpark figures, not measured data. They're calibrated to feel reasonable across casual, typical, and heavy/park-rat rider profiles. The tool is transparent about this — the note at the bottom of the worksheet results says to tune the dials yourself after applying suggestions.

**Suggested replacements at default worksheet settings (3 XC rides/wk × 12 mi, 2 enduro/wk × 8 mi, 5 park days):**

| Item | Suggested/yr |
|---|---|
| Tires | 3 |
| Brake pad sets | 4 |
| Rotors | 1 |
| Chains | 0.9 |
| Sealant refills | 2 |

---

## Printing and PDF export

The page has a dedicated print stylesheet (one `@media print` block at the end of the `<style>` section, with a header comment explaining each group). Use the **Print / save as PDF** button, or Ctrl/Cmd+P, then choose "Save as PDF".

What it does:

- Two pages, Letter or A4 (no fixed paper size is forced; margins only)
- Prints correctly whether or not "Background graphics" is ticked (`print-color-adjust: exact`)
- Print-only colors (`--p-*` tokens): all text at 4.8:1 or better against white, hairlines darkened so they survive a laser printer
- Grayscale-safe: breakdown bar uses solid / hatch / dot / plain textures, skipped items use strike-through plus a "SKIPPED" tag, the e-bike switch prints as ON / OFF
- Ride Worksheet is opened for the print job and restored afterward
- Cards and slider rows never split across a page break
- Footer with a QR code to postmillenniumrenaissance.com, the URL as text, and the print date

**The QR code is static.** It is an inline SVG (error-correction level Q, 4-module quiet zone) generated once, so the tool stays zero-dependency. Changing the destination URL means regenerating it; it is not computed at runtime.

**Inside an iframe:** Ctrl+P on a parent page prints the wrapper, not the tool. The Print button calls `window.print()` from inside the frame, which prints the tool alone.

**Print QA checklist (run on every change to layout or colors):** print to PDF on Letter and A4; look at it in grayscale; confirm 2 pages with nothing split mid-card; scan the QR from the PDF; test a state with skipped items and the battery switch on.

---

## Accessibility

- Touch targets: skip chips, interval badges and slider hit areas are 40px+ tall; buttons are 44px; the e-bike switch has a 44×44 hit area.
- Text contrast on screen is 4.5:1 or better (secondary text is `#71717A`).
- `prefers-reduced-motion` turns off every transition and animation, including the Game Over drop-in and the smooth scroll after Apply.
- The Game Over overlay takes focus, closes on Escape / Enter / Space or a click, and returns focus to the button that opened it.

---

## Technical notes

**Zero dependencies.** The tool is a single `index.html` file with no frameworks, no build step, and no CDN requests (Google Fonts is the only external link, and it degrades gracefully to system fonts if unavailable). Vanilla HTML, CSS, and JavaScript only.

**Deployment.** Drop `index.html` into any web host or GitHub Pages repository. No configuration required.

**How the annualized math works.** Each line item stores a raw cost and a service interval in months. The annualized cost is `cost / (interval_months / 12)`. For example, a $175 cassette on a 24-month interval costs $87.50/yr. All section totals and the grand total sum annualized values only, so the number always represents a true yearly spend estimate regardless of how frequently each item recurs.

**Interval cycling.** Drivetrain interval badges are interactive buttons. Clicking cycles through 12 → 24 → 36 → 12 months and immediately recalculates.

---

## Repository structure

```
maintenance-mtb/
└── index.html      # The entire tool — one file
└── README.md       # This file
```

---

## Part of the Post Millennium Renaissance tool suite

This calculator is one of a growing set of interactive MTB tools built for riders, advocates, and municipal stakeholders:

- **MTB Patent Atlas** — 200+ patents, color themes, Colorado innovation panel
- **Wheel Strength Lab** — spoke tension physics, hub database, failure mode classifier
- **Singletrack Density Dashboard** — 26 North American destinations benchmarked
- **Trail Investment ROI Calculator** — economic impact framing for council audiences
- **Sports Popularity Over Time** — animated 17-sport visualization
- **MTB Inflation Dashboard** — FRED/BLS data, affordability framing

[postmillenniumrenaissance.com](https://postmillenniumrenaissance.com)

---

*Built by Jon @ Post Millennium Renaissance MTB — Castle Rock, Colorado*
*Writing at [Pinkbike](https://www.pinkbike.com) · Advocacy for Philip S. Miller Park & Ridgeline Open Space*
