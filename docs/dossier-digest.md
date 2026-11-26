# CropGuard AI — Dossier Digest

Condensed working summary of `docs/CropGuard_AI_Project_Dossier.docx` (dated 18 November 2026, status: **CONCEPT UNDER VALIDATION**). The full dossier is the authoritative reference; this digest is for quick orientation.

## One-line description

An affordable (~BDT 25,000), modular, semi-autonomous agricultural robot: one shared mobile base carrying interchangeable tools for vegetable-care operations, with an AI perception layer — designed so that every headline feature is live-demonstrable, repeatable and measurable on showcase day.

## Confirmed constraints

| Parameter | Value |
|---|---|
| Team | 4 students |
| Time | 2–3 months |
| Budget | ~BDT 25,000 |
| Context | University electronics/hardware project showcase |
| Feature rule | 4 genuinely distinct agricultural operations — not 4 subcomponents of 2 operations |
| Core demo rule | Every headline feature must work live on showcase day |
| Architecture | One common robot base + interchangeable modules |

## Recommended direction (not yet locked)

- **Target:** open-field vegetable cultivation on raised beds with row planting (not paddy rice — flooded fields need a different mobility platform).
- **First crop:** brinjal (eggplant) — provisional; tomato/chilli as alternates; to be validated with a local grower / agricultural extension source.
- **Four-operation shortlist:**
  1. **Automated seedling transplanting** — recommended; highest risk module.
  2. **Crop-aware mechanical weeding** — recommended; medium-high risk.
  3. **AI-guided targeted spraying** (water/coloured water only in public demo) — recommended; medium risk.
  4. **Selective plant maintenance** — UNRESOLVED; pruning is a candidate but high mechanical/plant-damage risk.
- **Compute split:** ESP32 owns real-time motor/actuator control + safety; laptop/external computer runs AI inference initially.

## Five acceptance tests for every headline feature

Live demonstration · Observable result · Repeatability · Technical depth · Research value (quantified metrics with baselines and limitations).

## Key engineering positions

- Manual/test mode is mandatory; AI assists but is never a single point of failure.
- Wheel-encoder odometry is relative-only; no centimetre-level absolute positioning claims without a measured positioning system.
- Camera-to-tool calibration, safety zones and no-action thresholds are required before any AI-triggered actuation.
- Power: separate motor/logic rails, DC-DC regulation, main + branch fusing, e-stop, watchdogs, limit switches.
- The user's "1800 AMP 12V" car jump starter is unverified — inspect label/manual (chemistry, Wh, continuous output) before use; never connect clamps directly to electronics.
- Solar charging: optional supporting feature only, not a core feature.
- Soil sensing + precision irrigation: rejected as a headline feature (too generic / already showcased by similar projects).
- UV-C treatment: not a core feature (biological outcome invisible; safety + validation burden).

## Prior art and novelty discipline

FarmDroid FD20/FD60 (precision seeding + seed-position memory + mechanical weeding + spot spray), NARO AI tomato de-leafing robot (March 2026), nursery-seedling transplanting review (2025), vision-guided spot-spraying research (2025). CropGuard's defensible contribution: **low-cost modular integration for Bangladeshi vegetable-bed geometry, quick-change tools, shared electronics/software, locally calibrated perception-to-tool coordinates, measured multi-operation performance.** Avoid all "world's first" style claims.

## Proposed acceptance gates

- Mechanical module proof: ≥ 8 successful runs out of 10 consecutive attempts in controlled conditions before it counts as a headline feature.
- E-stop must work in every tested condition; no spray on stale/low-confidence detections.
- Crop-damage threshold defined in advance; all damage counted and explained.
- Module changeover without rewiring or unsafe exposed connections.

## Budget allocation (planning only — no supplier quotes confirmed yet)

| Category | BDT |
|---|---|
| Chassis, wheels, frame, fabrication | 4,000–5,000 |
| Drive motors, encoders, drivers | 3,500–4,500 |
| ESP32, wiring, connectors, protection, regulators | 2,000–2,800 |
| Camera / AI integration | 1,000–2,500 |
| Transplanting mechanism | 3,000–4,000 |
| Weeding mechanism | 1,500–2,500 |
| Sprayer module | 1,000–1,800 |
| Fourth module prototype | 1,500–2,500 |
| Test plot, seedlings, consumables, contingency | 2,000–3,000 |

## Open decisions

1. Final crop (brinjal vs tomato/chilli) — validate with local grower / DAE extension source.
2. Fourth operation — compare pruning, support/tie placement, etc. via proof-of-concept before committing.
3. Robot geometry — measure a real bed and row layout before freezing chassis dimensions.
4. Power source — verify jump starter; build a current/energy budget and select battery safely.
5. AI Lab collaboration (friend's project) — agree task/dataset/interface/delivery; keep manual fallback.
6. Showcase requirements — confirm event/course eligibility and obtain the official judging rubric.

## Immediate action plan (dossier §17)

1. Document a typical brinjal bed from a local grower: row/plant spacing, bed width, seedling age/size, soil.
2. Build a physical mock bed; define wheel path and tool reach before finalising the chassis.
3. Bench-prototype the seedling gripper; run 10 consecutive pick-and-place attempts, record success + damage.
4. Prototype the weeding tool on a soil tray with known crop/weed positions.
5. Prototype the water-only targeted sprayer against a fixed target card; measure hit/miss.
6. Research and prototype one fourth plant-maintenance operation (do not assume pruning works).
7. Inspect the jump starter's label/manual; record chemistry, Wh, output ports, continuous ratings.
8. Freeze the module interface and power distribution only after motor/actuator loads are estimated.
9. Create a one-page test plan and a shared failure log before integrating AI.

## Reviewer's notes (repo assistant, 26 Nov 2026)

Gaps the dossier itself flags, ranked by what research can close:

1. **No real supplier prices** — budget is allocation only. Needed: component-level BOM with actual Bangladesh prices (e.g., TechShop BD, Robo Tech Valley, ArduinoBD, local Nilkhet/Banglamotor suppliers) and availability checks.
2. **Fourth operation unresolved** — the single biggest spec gap. Needed: a structured candidate comparison (pruning, sucker removal, support/tie, training, other) scored on demonstrability, risk, distinctness, cost, build time.
3. **No motor torque / power budget calculations** — chassis mass, wheel radius, stall current estimates and battery selection depend on this.
4. **Judging rubric unknown** — the winning strategy should be built on the official rubric once obtained, plus typical project-show criteria (technical depth, live demo, innovation, results, presentation).
5. **Competition scan** — what agri-robot projects typically appear at UIU/national project shows, so CropGuard differentiates rather than repeats.
