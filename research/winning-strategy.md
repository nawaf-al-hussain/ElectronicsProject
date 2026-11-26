# CropGuard AI — UIU CSE Project Show: Winning Strategy

**Date:** 26 November 2026
**Purpose:** Close dossier gap #5 (competition strategy) with a plan grounded in verified facts about how the UIU CSE Project Show actually works — and explicit "to be confirmed" flags where only the official rubric can settle a question.
**Honesty rule for this document:** facts in §1 carry sources. Judging dimensions in §3 are *assumptions* until the official rubric arrives (dossier open-decision 6). Nothing here claims knowledge of the rubric we do not have.

---

## 1. Verified facts about the event (with sources)

| Fact | Detail | Source |
|---|---|---|
| Scale | Spring 2025 show: **417 projects from 8 lab courses**; software + hardware domains | UIU CSE Project Show FB page (@uiucseps); UIU CSE dept news |
| Finalist funnel | **32 top teams (~157 students)** advanced to the final showcase, UIU Multipurpose Hall (Aug 4, 2025) | @uiucseps |
| Two-stage structure | Initial evaluation → "top projects advancing to the final round showcase" | projectshow.uiucomputerclub.com (finalists page) |
| Official platform | Registration, team portal, schedule, judging, winners run on projectshow.uiucomputerclub.com; Summer 2026 season active | same |
| Recurring event | Spring 2026 showcase page on cse.uiu.ac.bd; per-season cycles with prize-giving ceremonies | cse.uiu.ac.bd event page |
| **Official judging rubric** | **Not public.** Platform pages do not publish criteria/weights. | checked 26 Nov 2026 — must be obtained from supervisor/organizers |

**What is NOT known (do not design against guesses):** the exact rubric categories and weights, whether Electronics Lab projects compete in the same pool as CSE lab courses, per-team demo time, first-stage submission format. Owner: team lead via supervisor + the platform's Register page. **Action: fill §3's weights column the day the rubric arrives.**

---

## 2. Strategic read of the funnel: 417 → 32

The filter eliminates ~92% of projects *before* the showcase floor. Two consequences drive everything below:

1. **The first-stage package is a product, not paperwork.** A hardware project that reads as "a robot that does farming stuff" on a registration form loses to one that reads as "four measured operations, each with a live pass-rate, on a ৳25k budget." CropGuard's dossier discipline and this repo's priced BOM, power budget and candidate analyses are exactly the evidence first-stage evaluators can see. The repo link goes on the registration.
2. **On the floor, 32 teams compete for attention.** Judges spend minutes per booth across a full hall. The demo must land its value in ~3 minutes, show measurable results at a glance, and reset fast for the next visitor. That is an engineering requirement — it gets a script, a metrics board, and a spares kit, not good intentions.

A third consequence: most UIU show projects are software (web/app/IoT dashboards dominate university showcases). A *physically working, four-operation robot with printed pass-rates* is intrinsically rare on that floor — our differentiation is structural, not cosmetic.

---

## 3. Assumed judging dimensions (until the rubric arrives)

Standard hardware-project-show dimensions, clearly labeled as assumptions to be re-weighted the day the official rubric lands:

| Dimension (assumed) | Weight (unknown — fill in) | CropGuard's evidence asset | Where it comes from |
|---|---|---|---|
| Technical depth / engineering quality | ? | Power budget with bench tests T1–T5; rail architecture; stall-cutoff firmware; module interface spec | research/motor-power-budget.md; dossier §4 |
| Innovation / novelty (honest) | ? | Low-cost modular quick-change platform for BD raised-bed geometry; buzz-pollination assist is a genuinely uncommon robot operation | fourth-operation-analysis.md; digest prior-art section |
| Live demo quality | ? | 3-minute script; every feature live and repeatable; 60-second reset | §5 below |
| Measurable results | ? | Live metrics board: pick rate, placement error, weed removals, spray hit %, pollen-burst counts vs control | §6 below |
| Real-world usefulness | ? | Brinjal/raised-bed focus with local cost case in BDT; labour-cost framing from dossier | dossier §1, §7 |
| Documentation / presentation | ? | This repo (research + reports), poster, one-pager, video evidence | reports/ (to be built) |

The dossier's own five acceptance tests (live, observable, repeatable, depth, research value) already anticipate these dimensions — the strategy is to make each one *visible at the booth*, not merely true.

---

## 4. Claims discipline (what we say vs what we show)

Judges punish overclaims harder than modest scope. Every claim we make aloud must have booth evidence within 60 seconds of being challenged:

| Claim | We may say | We may NOT say | Booth evidence |
|---|---|---|---|
| Modular platform | "tool swap without rewiring, measured changeover time" | "industry-first modularity" | Live swap on stage: timed, shown twice |
| Transplanting | "picked/placed N of 10 seedlings, X% success on camera" | "autonomous transplanting solved" | Counter + repeated live runs |
| Weeding | "removed K of K weeds, zero crop contact in demo" | "novel weeding invention" | Before/after bed section on the plot |
| Spraying | "hit M of M targets with metered pulses" | "pesticide spraying" | Water + food dye on target cards |
| Fourth operation (pollination) | "vibration probe releases pollen visibly; fruit-set comparison vs control" | "increases yield by X%" (until measured) | Pollen burst on black card, live |
| AI | "detection-assisted targeting with manual fallback, confidence threshold" | "AI agriculture" | Dashboard log of thresholds + miss cases shown |

The fourth-operation PoC gate (8/10 runs) decides whether pollination or earthing-up is presented — §5's script has both variants ready.

---

## 5. The 3-minute demo script (rehearsed to a stopwatch)

| Time | Action | Judge sees |
|---|---|---|
| 0:00–0:20 | Frame the problem: vegetable-crop care is labour-heavy; one robot base, four tools, ৳25k budget — point at printed BOM with real prices | The cost poster (novel for student shows) |
| 0:20–0:50 | **Live module swap** while talking: dock transplanter, undock, dock weeder — timer on display | Quick-change standard working under their eyes |
| 0:50–1:40 | Transplanter run: 2 consecutive pick-place cycles on the mock tray; success counter updates | Pass rate counting up; gripper handling a living seedling |
| 1:40–2:20 | Weeding pass along a bed section with known weeds; then targeted spray (dyed water) onto AI-designated targets | Blade removes weed; spray dots only on targets |
| 2:20–2:50 | Fourth-operation highlight: vibration probe → pollen burst on black card, vs untouched control card | A visible, measurable biological effect — the memorable moment |
| 2:50–3:00 | Close on metrics board + repo QR code | Evidence they can photograph |

**Manual-mode interleave:** every operation is first shown in manual mode (buttons) — this is the dossier's AI-is-never-a-single-point-of-failure rule turned into a demo feature: judges see autonomy as an assist, not a gamble.

---

## 6. Live metrics board and the 60-second reset

- **Metrics board (a small display or laminated sheet updated live):** transplant success %, placement error (cm), weeds removed / weeds total, spray hit %, pollen bursts vs control, changeover time (s), uptime since boot. Numbers accumulate across the day — judges visiting late still see the day's totals, which also proves repeatability beyond cherry-picked runs.
- **Reset procedure (target 60 s, rehearsed):** reset tray to indexed start → reseed weed targets from the reserve pot row → swap spray tank to reserve bottle → counters zeroed → robot back to start mark. Two team members drill it; it doubles as the fault-recovery routine, so any mid-demo failure becomes a 60-second recovery instead of a dead booth.
- **Camera-ready bench setup:** mock tray + bed section + target cards sit on a single board that lifts off the plot onto the table — so the demo works on the hall floor even if the soil plot can't be in the hall (confirm venue rules early — unknown, flagged).

---

## 7. Demo-day spares kit and fault tree (priced from the BOM)

| Spares kit item | Price (BDT) | Source |
|---|---|---|
| 1× MG996R spare servo | 354 | RoboticsBD (BOM C1) |
| 1× BTS7960 spare driver | 519 | Dream RC (BOM A2) |
| Spare blade fuses 10/15/20 A | 120 | est (BOM A7) |
| XT60 pair + jumper wires + zip ties | 150 | est (BOM A8/A16) |
| Hot glue + double tape + cable ties | 100 | est |
| Pre-charged SLA (charged night before) | 0 | procedure |
| **Total** | **≈1,243** | within contingency H6 |

Fault tree (pre-decided responses, not improvisation):
- **Drive motor/driver dies** → swap driver (10 min drill), else switch to single-motor mode with reduced payload; the two-stage demo script (§5) runs fully on the bench board without driving.
- **Servo dies** → swap (7 min); gripper can complete demo at reduced success rate with the failure honestly announced — judges respect measured honesty.
- **WiFi/laptop fails** → manual mode + phone hotspot; AI layer is assist-only by design.
- **Pump clogs** → clear nozzle (spare bottle flush); demo continues on weeding/transplanting.
- **Power drain** → 45-min session is 19% capacity (power budget §7); lunchtime recharge; no mid-show swap needed.

---

## 8. First-stage registration package (the 92% filter)

Checklist assembled *before* registration closes (dates unknown — monitor the platform):

1. **90-second video:** the §5 script, shot on the real plot — this video is also the fallback demo if the venue forbids soil.
2. **One-pager (PDF):** problem → four operations → architecture → measured targets → budget with priced BOM headline numbers → team + supervisor.
3. **Repo link** (this repository) — evidence of engineering process: priced BOM, power budget, candidate analyses, test protocols.
4. **Novelty statement** in the dossier's honest framing: *low-cost modular multi-operation platform locally calibrated for Bangladeshi raised-bed vegetable cultivation* — no "world's first" phrasing anywhere.
5. **Registration fields exactly per platform** (projectshow.uiucomputerclub.com) — assign one owner.

---

## 9. Rehearsal timeline (mapped to the dossier's phases)

| Dossier phase | Strategy output due |
|---|---|
| 0. Scope freeze (W1) | Crop + fourth-operation PoC order + plot path levelness requirement (≤3° per power budget §5) |
| 1–2. Base + interface (W1–4) | Bench tests T1–T3 done; reset procedure v1; first swap timing measured |
| 3–4. Risk-first prototypes + tools (W3–7) | Metrics counters implemented per module; fault-tree drills begin |
| 5. AI integration (W5–8) | Dashboard log with confidence thresholds; miss-case display |
| 6. System testing (W8–10) | Full §5 script under 3:00 five times; reset under 60 s five times; day-long endurance run (validates §7 runtime) |
| 7. Showcase prep (final 2 wks) | Video shot; one-pager printed; spares kit packed; booth layout drawn; rubric re-check |

---

## 10. Immediate actions (owner: team)

1. **Get the official rubric + registration dates** from the supervisor / projectshow.uiucomputerclub.com — fills §3 weights and the schedule column. *(Blocked on organizers; everything above stands without it, weights may re-order emphasis.)*
2. **Confirm venue rules:** can the soil plot enter the hall? power strip availability? bench-board fallback decides §6 setup.
3. **Order the Week-1 first-purchase list (BOM §4)** — the pull test (T1) needs the chassis more than anything else.
4. **Measure the real brinjal bed** (dossier §17.1) — row spacing sets gripper reach and wheel path; plot levelness requirement gets real numbers.
5. **Assign owners:** metrics dashboard, reset drill, video/one-pager, registration form — four members, four deliverables.

*Standing rule: update this document — not hallway memory — when the rubric, dates, or venue answers arrive.*
