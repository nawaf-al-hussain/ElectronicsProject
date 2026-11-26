# CropGuard AI — Fourth Operation: Candidate Analysis and Recommendation

**Date:** 26 November 2026
**Decision it supports:** choosing the fourth headline operation (dossier §5.5 — currently *unresolved*; pruning is a candidate but flagged high-risk).
**Method:** candidates scored against six weighted criteria derived from the dossier's own rules — the five acceptance tests (§2.1), the four-genuinely-distinct-operations rule (§2), and the 8/10 proof-of-concept gate (§5.9). Prior art was checked via web research on 26 Nov 2026; sources listed at the end.

---

## 1. The six criteria and weights

| Criterion | Weight | Why |
|-----------|--------|-----|
| Live demonstrability & observable result | 0.25 | Dossier core rule: judges must see the physical change happen |
| Distinctness from transplanting / weeding / spraying | 0.20 | Four features must be four genuinely distinct operations (§2) |
| Probability of passing the 8/10 reliability gate | 0.20 | §5.9 gate; a feature that cannot pass must not be locked |
| Cost & build time within 2–3 month schedule | 0.15 | Budget ~৳1,500–2,500 allocation; schedule is aggressive (§12.1) |
| Crop fit: brinjal / Bangladesh context | 0.10 | Brinjal is the provisional first crop; local relevance matters to judges |
| Safety & fast reset between runs | 0.10 | Booth demo must reset quickly and safely (§15.3) |

Scores are 1 (poor) to 5 (excellent); they are engineering judgements from this research, to be revised after the bench proof-of-concept tests.

---

## 2. The candidates

### 2.1 Selective pruning / de-leafing

- **What it is:** robot identifies a selected leaf/shoot and cuts it with a guarded cutting tool.
- **Agronomic basis:** brinjal pruning is practised (studies test no-pruning vs 2–3-stem retention; pruning affects yield).
- **Prior art:** NARO (Japan) announced an AI tomato de-leafing robot with a specialised arm-mounted end-effector (6 March 2026); Kompano de-leafing robot operates commercially (claims >85% effectiveness); Penn State built a robotic apple-pruning end-effector (Zahid et al. 2020, cuts branches up to ~12 mm). The general concept is established — CropGuard cannot claim novelty in pruning itself (dossier §10 already flags this).
- **Mechanism sketch:** camera + plant-part model → servo-driven scissor/secateurs on a small carriage → cut validation photo.
- **Demo metrics:** correct-cut %, wrong-cut %, cut completion, cycle time, unintended damage.
- **Risks (why the dossier hesitates):** plant-part recognition in cluttered foliage; the tool must reach the target without contacting fruit/other tissue; a missed or misplaced cut on a live plant is visible damage; cut quality varies with stem moisture.
- **Cost/build:** cutting head + servo cheap (৳800–1,200 fab); perception is the expensive part — days of dataset work for an unreliable skill.
- **Score rationale:** highly distinct and visible, but the reliability gate probability is the worst of all candidates (2/5).

### 2.2 Sucker removal (2–3 stem training)

- **What it is:** remove side shoots at leaf–stem junctions to train the plant to 2–3 stems (common for tomato; practised on brinjal).
- **Prior art:** active research field — robotic tomato sucker removal with branch-length recognition and pruning-point localisation (Qiu et al. 2025); three-stage sucker-pruning methods for greenhouse tomatoes (Li et al.). Established, not novel as an idea.
- **Risks:** essentially pruning with a narrower target — same perception and cutting risks; juvenile suckers are softer (easier to remove than woody stems) which slightly raises the gate probability (2.5/5).
- **Score rationale:** distinctness is a bit weaker than pruning (removing a small shoot looks similar to weeding's plant-removal action from the booth distance, dossier §5.7 concern).

### 2.3 Support/tie clip placement (staking assistance)

- **What it is:** robot clips a spring/clip tie connecting the plant stem to a stake, preventing lodging under fruit load.
- **Agronomic basis:** staking eggplant/brinjal is common practice; plant support clips are a large commercial market (~USD 1.8B in 2025) for trellised vegetables.
- **Prior art:** no commercial or research robot for automated tie/clip placement was found in this scan (only manual clip products) — a genuine mechanisation gap. That is attractive for a showcase, but it also means no proven design to copy; treat as unknown-unknowns territory.
- **Mechanism sketch:** clip magazine + servo-driven applicator that opens a spring clip, positions it around stem+stake, releases. Simple 2-DOF positioning.
- **Demo metrics:** clips placed %, correct placement (stem+stake both engaged) %, stem damage %, clips jammed, cycle time.
- **Risks:** clip handling/jamming in the magazine; flexible stem moves on contact; grip force must be gentle.
- **Score rationale:** excellent distinctness and visibility (a clip snapping shut is unmistakable); reliability uncertain (2.5/5) because clip feeding mechanisms are fiddly.

### 2.4 Buzz-pollination assist (flower vibration) — **recommended primary**

- **What it is:** robot touches/vibrates an open flower cluster with a small vibrating probe so the poricidal anthers release pollen — the same mechanism bumblebees use. Eggplant/brinjal is a buzz-pollinated crop (documented: bumblebee pollination of greenhouse eggplant; Cooley 2021 global review of buzz-pollinated crops).
- **Prior art:** electric/manual vibration wands are established tools; robot-bee lab prototypes (Stirling 2022); camera-guided robot pollination with air-puff (e.g., the "Polly"-type rover concept aimed at student builds); sonic-vibration research on tomato anthers (Anwar 2025). The idea is not new — the low-cost, measurable integration on a multi-operation robot is the defensible angle.
- **Mechanism sketch:** small vibration motor or servo-tapper on a soft probe at the end of a short arm; detection of receptive flowers can start as manual targeting (assisted mode) before any vision work.
- **Demo metrics (all directly measurable):** flowers contacted %, pollen released % (pollen visibly deposited on a black card / transparent slide under the flower — count deposition squares by phone photo), flower damage % (petals/anthers intact), cycle time, and a **vibration vs no-vibration controlled comparison** on matched flowers — a genuine experiment with a visible, countable outcome.
- **Risks (honest):** flowers must be freshly open (demo timing dependent — bring spare potted flowering plants); too much force can scar petals (use compliant probe tip); open-field brinjal is normally pollinated by wind/insects, so the honest value claim is *pollination assurance for protected or low-pollinator settings and a measurable pollen-release study*, **not** a yield-increase claim.
- **Score rationale:** top-ranked. Nothing about it collides with the other three operations; the outcome (pollen burst) is visible from a metre away and measurable to research-report standard; failure is benign (no plant damage); cost is minimal; reset is instant.

### 2.5 Earthing-up (soil ridging at plant base) — **recommended fallback**

- **What it is:** two angled ridger blades draw friable soil up around the plant base as the robot advances, strengthening the stem, covering exposed roots, and improving root development.
- **Agronomic basis:** documented practice for tomato (earthing-up + pruning studies show yield benefit — e.g., AJAHR 2021 triple-stem + earthing-up recommendation); benefits listed for tomato farming: strengthens stem, prevents lodging, covers exposed roots; practised in brinjal systems for root volume (anecdotal — verify with DAE/local grower).
- **Prior art:** hilling/ridging implements are ancient and standard on tractors and wheel hoes — no novelty claim possible or needed; the contribution is miniaturisation onto a low-cost robot platform.
- **Mechanism sketch:** passive! Two shaped blades + adjustable depth stop; no actuators, no AI. The robot's drive system must handle the draft force.
- **Demo metrics:** soil mounded to target height %, blade depth consistency, crop damage %, cycle time, draft-force/current draw logged.
- **Risks:** chassis must be strong enough to pull soil (adds a requirement to the power/motor budget); needs friable demo-bed soil; messier reset (re-flatten bed) than other candidates.
- **Score rationale:** highest reliability of all candidates (4/5 — passive tool, nothing to misfire), highly visible, but slightly weaker crop-fit evidence for brinjal specifically and the messy reset.

### 2.6 Selective crop thinning

- **What it is:** identify overcrowded crop seedlings and remove selected excess plants, preserving the strongest per a defined rule (spacing or vigour).
- **Prior art:** machine-vision thinning is an established research area (lettuce thinning robots commercialised elsewhere).
- **Score rationale:** agronomically distinct from weeding, but **physically looks identical from the booth** — a tool pulls a plant out of soil (dossier §5.7 warns exactly this). Weakest on distinctness (2.5/5). Keep as the known fallback family behind precision seeding (dossier §5.8), not as the fourth operation.

---

## 3. Scoring matrix (computed)

| Candidate | Live demo (0.25) | Distinctness (0.20) | Gate probability (0.20) | Cost/build (0.15) | Crop fit (0.10) | Safety/reset (0.10) | **Weighted total /5** |
|-----------|------|------|------|------|------|------|------|
| **Buzz-pollination assist** | 5.0 | 5.0 | 3.0 | 4.5 | 3.5 | 5.0 | **4.38** |
| **Earthing-up (soil ridging)** | 5.0 | 4.5 | 4.0 | 3.5 | 3.5 | 4.0 | **4.23** |
| Support/tie clip placement | 5.0 | 5.0 | 2.5 | 3.5 | 4.5 | 4.0 | **4.12** |
| Selective pruning / de-leafing | 4.0 | 5.0 | 2.0 | 3.5 | 4.0 | 3.0 | **3.62** |
| Sucker removal (2–3 stem) | 4.0 | 4.5 | 2.5 | 3.5 | 4.0 | 3.0 | **3.62** |
| Selective crop thinning | 2.5 | 2.5 | 2.5 | 3.5 | 3.5 | 3.5 | **2.85** |

(Computation script: `scripts/compute_bom_and_scores.py` in this repo. Sensitivity note: pruning and sucker removal would only overtake the top three if the gate-probability weight were halved — i.e., only if perception reliability stopped mattering, which contradicts the dossier's own gating philosophy.)

---

## 4. Recommendation

1. **Primary: buzz-pollination assist (flower vibration).** Distinct (touches flowers, not soil/weeds/seedlings), instantly visible (pollen burst on a dark card), cheap (≤৳1,000 prototype, already reserved in BOM section G), safe (compliant probe, no cutting), instantly resettable, and it produces a real controlled experiment (vibration vs no-vibration pollen counts) that fills the "research value" acceptance test better than any other candidate. It also showcases the modular architecture story: base stays the same, tool changes, purpose changes completely.
2. **Fallback: earthing-up.** If the flower-probe prototype fails its gate by Week 5, the earthing-up blades are the highest-probability substitute (passive tool, 4/5 gate probability). Cost already reserved in BOM section G. Decision point follows the dossier's risk-first prototype phase (Weeks 3–5).
3. **Do not lock pruning or sucker removal** unless the team independently builds a cutting prototype that beats the 8/10 gate on expendable plants before Week 5 — the research says these are the riskiest paths (perception-heavy, damage-prone), consistent with the dossier's own hesitation.
4. **Support/tie placement** remains a stretch candidate if the team finds a reliable clip-feeding design early; it is the most "novel-looking" option but has the least prior art to learn from, which cuts both ways.

**Honest-value framing for the pitch:** "One low-cost modular base, four genuinely different crop-care operations — establishment (transplanting), protection (weeding), treatment (targeted spraying), and plant support/pollination (fourth module) — each measured, with published-style metrics and stated limitations." Avoid: first/only claims of any kind (FarmDroid, NARO, Kompano, Penn State end-effectors, and robot-pollination research all predate this project).

---

## 5. Proof-of-concept gate plan for the recommended candidate

**Objective:** decide buzz-pollination vs earthing-up with data, per dossier §5.9 (≥8/10 consecutive successes, failures recorded).

**Test protocol (buzz-pollination assist):**
1. Prepare 20+ potted brinjal plants with fresh open flowers; mark matched pairs (similar flower stage) for vibration vs control.
2. Hand-held probe first (no robot): vibration motor at ~100–200 Hz contact 1–2 s per flower, black card/slide held under the flower.
3. Score each trial: pollen deposition visible/countable (pass), no visible flower damage (must), contact accuracy on targeted flower.
4. Record all 10+ consecutive attempts including failures; compute pass rate and damage rate.
5. Only after the hand-held probe passes ≥8/10, mount the probe on the robot base and repeat with assisted targeting (manual position first; vision later).
6. Repeat after module removal/reinstallation to test calibration repeatability (dossier §11.1 step 7).

**Test protocol (earthing-up fallback, run in parallel on the same soil tray):**
1. Friable soil tray, marked row; blades set to target depth.
2. 10 passes: measure mound height consistency, crop-simulant (stake) disturbance, current draw of drive motors under draft load.
3. If motor current exceeds the drive budget, the candidate gets a cost flag that must be resolved before it can replace the pollination module.

**Decision rule:** lock buzz-pollination if its gate passes by end of Week 5; otherwise lock earthing-up if its gate passes; otherwise fall back to precision-seed-dispensing per dossier §5.8.

---

## 6. Sources (checked 26 Nov 2026)

- NARO (Japan), "Development of an automated tomato de-leafing robot," 6 March 2026 — naro.go.jp/english/topics/laboratory/iam/173138.html
- Kompano de-leafing robot — futurefarming.com (commercial de-leafing, >85% effectiveness claim)
- Zahid et al. 2020, robotic apple-pruning end-effector, Penn State — pure.psu.edu; projects.sare.org (2R_EE.pdf); farmprogress.com coverage
- Qiu et al. 2025, "Branch length recognition and pruning point localization" (robotic tomato sucker removal) — sciencedirect.com (S2772375525009700)
- Li et al., "3s-Tpp: A three-stage method for tomato sucker pruning" — papers.ssrn.com (abstract 5203179)
- Cooley 2021, "Buzz-Pollinated Crops: A Global Review and Meta-Analysis" — PMC8042731 (includes eggplant among buzz-pollinated crops)
- Garden Professors, "Eggplants getting their buzz on" (2015) — gardenprofessors.com; Texas Dept. of Agriculture bumblebee/eggplant note
- Anwar et al. 2025, "Sonic-induced cellular vibrations unzip intertwined anther" (tomato pollination vibrations) — PMC12060008
- University of Stirling, "Building a buzz: robot bees to simulate pollination" (April 2022) — stir.ac.uk
- Robot pollination guide incl. student rover concept ("Polly"-type, camera-guided air-puff) — projectech.in/guides/how-robot-pollination-works-guide
- "Effects of Earthing up and Pruning Systems on Growth and Yield of Tomato," AJAHR (2021) — journalajahr.com/article/view/150; related 2026 earthing-up/pruning study
- Plant Support Clip market report (USD 1.8B, 2025) — dataintelo.com (context for clip availability)
- Brinjal/eggplant pruning practice references — Search results incl. pruning-technique studies (3-stem retention) and grower guidance

*Sources were read via web search snippets on 26 Nov 2026 to establish prior art and agronomic practice; verify page details when citing in the final report.*
