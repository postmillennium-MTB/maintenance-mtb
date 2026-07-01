# MTB Annual Maintenance Cost Calculator

**Post Millennium Renaissance — Interactive Tool**
[postmillenniumrenaissance.com](https://postmillenniumrenaissance.com)

An interactive, single-file calculator that helps mountain bikers estimate their annual maintenance spend. Adjust cost dials for every major service category, set your own replacement intervals, and use the Ride Worksheet to get ballpark suggestions based on how you actually ride.

Live: [postmillennium-mtb.github.io/maintenance-mtb](https://postmillennium-mtb.github.io/maintenance-mtb/)

---

## What it does

- **Cost dials** for every major service category — suspension, drivetrain, consumables, and ancillary
- **Clickable interval badges** on drivetrain items (chain, cassette, chainring) to cycle between 12 / 24 / 36 month replacement schedules
- **Annualized math** — every line item is converted to a per-year cost regardless of its service interval, so the grand total is always apples-to-apples
- **Semicircle gauge** showing Budget / Typical / Premium zones at a glance
- **"Where it goes" breakdown bar** showing the proportion of spend across four categories
- **Ride Worksheet** — a collapsible section where you enter your riding volume (XC rides/week, miles/ride, enduro rides, and bike park days) and the tool suggests how many tires, brake pad sets, rotors, chains, and sealant refills you're likely to burn through per year
- **Apply to dials** button — pushes the worksheet suggestions directly into the quantity dials
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
| Pivot bearings | $50–$260 | $150 | 24 months* |
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

**Default grand total at baseline settings: ~$725/yr (~$60/mo)**

---

## Ride Worksheet — wear model

The worksheet converts riding volume into suggested replacement quantities using a simple mileage-based wear model.

**Inputs**
- XC/trail: rides per week (1–7), miles per ride (1–50)
- Enduro/aggressive: rides per week (0–7), miles per ride (1–50)
- Bike park days this season (1–50)

**Assumptions**
- Season length: 30 weeks
- Rear tire life: ~800 miles
- Front tire life: ~1,600 miles (front lasts ~2× longer)
- Brake pad life: ~1,000 miles per set (front + rear)
- Rotor life: ~4,000 miles per rotor
- Bike park days count as ~3 trail rides of wear (heavier braking, more cornering load)
- Park miles apply additional severity multipliers vs. trail miles for pads (2×) and rotors (1.5×)

These are ballpark figures, not measured data. They're calibrated to feel reasonable across casual, typical, and heavy/park-rat rider profiles. The tool is transparent about this — the note at the bottom of the worksheet results says to tune the dials yourself after applying suggestions.

**Suggested replacements at default worksheet settings (3 XC rides/wk × 12 mi, 2 enduro/wk × 8 mi, 5 park days):**

| Item | Suggested/yr |
|---|---|
| Tires | 3 |
| Brake pad sets | 4 |
| Rotors | 1 |
| Chains | 1 |
| Sealant refills | 2 |

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
