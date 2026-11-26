# CropGuard AI — Motor, Traction & Power Budget (Build-Ready Calculations)

**Date:** 26 November 2026
**Purpose:** Close dossier gap #3 ("no motor torque / power budget calculations") and unlock the deferred purchases flagged in the BOM (battery A10, charger A11, second drive motor A3). This document decides: drive motor variant, wheel size confirmation, battery chemistry, rail architecture, and protection — with the bench tests that verify each assumption on real hardware before the module interface freezes (dossier §17 action 8).
**Method:** All numbers below were computed by `scripts/compute_power_budget.py` in this repo — no hand arithmetic. Component specs come from named datasheets/retailers listed in §14. Where no datasheet exists (rolling resistance on our soil, workshop masses), the value is an **assumption with a measurement protocol**, not a guessed fact. Every assumption feeds a Week-1 bench test whose result replaces it.

---

## 1. Headline decisions (what this budget settles)

1. **Drive motor: buy the 37GB 12V 200 RPM variant (৳850, RoboTechShop) — not the 300/500 RPM (৳1,149–1,500).** Worst-case demand is 9.5 kg·cm per motor against a ≥10 kg·cm conservative floor, and the slower variant gives 1.05 m/s top speed — high enough to traverse the plot, low enough that 0.30 m/s operating speed sits at 29% PWM (healthy range) instead of 19% (noisy low end). It is also the cheapest torque on the market: 2× saves ৳598 vs the 300 RPM Dream RC listing.
2. **2WD + 100 mm wheels is sufficient for the controlled demo plot; 4WD is a pre-priced contingency, not a default.** Worst-case (12 kg robot, firm path, 5° grade, 0.5 m/s²) needs 9.5 kg·cm per motor in 2WD and 4.8 in 4WD. Traction needs μ = 0.40 against rubber-on-firm-soil ≈ 0.5–0.7. The 130 mm off-road wheels (৳850 ea) would *worsen* torque demand to 12.4 kg·cm — bigger wheels multiply torque needed for the same push force — so the BOM's S4 choice (100 mm, ৳80 ea) is confirmed by physics, not just price.
3. **Battery: 12 V 7 Ah SLA (৳1,350). Confirmed by numbers, not habit.** Average draw 1.75 A → a 45-minute demo/test session consumes 19% of capacity; even 80% DoD emergency use gives 3.2 h. The lighter 18650 3S route was priced but adds BMS + balance-charger cost and fire-safety discipline for zero budget saving — keep SLA for v1, document Li-ion as the upgrade path.
4. **Two wiring catches the BOM couldn't show:** the ৳130 e-stop button is a logic-rated part and must **not** break motor current directly (wire it to the BTS7960 EN/R_EN pins + ESP32 interrupt instead), and the LM2596 3 A buck **cannot** power five MG996R servos (worst brief 12.5 A) — a dedicated 5 A UBEC rail is required. Both fixes are priced into the updated budget (§11).
5. **Peak-current honesty:** simultaneous full stall of both drive motors + 3 servos + pump is 22–48 A. Rather than trusting the battery to shrug it off, the firmware gets a **stall cutoff** (INA219 or multimeter-verified current limit: cut PWM if > 10–12 A for > 1 s). This is standard practice, protects the battery and gearbox, and doubles as measured technical depth for judges.

---

## 2. Verified component specifications (the inputs that are real)

| Component | Spec used | Value | Source |
|---|---|---|---|
| 37GB / JGB37-550 geared motor | free-run current | 1.1 A @ 12 V | Handsontec JGB37-550 datasheet PDF; Scribd copy |
| 37GB / JGB37-550 | stall current | 20 A @ 12 V (datasheet max); openimpulse variant row: 7 A | Handsontec datasheet; OpenImpulse gearmotor selector |
| 37GB / JGB37-550 | torque range across ratios | 0.7–40 kg·cm rated; one 12 V variant row 26 kg·cm stall | PrecisionMiniDrives 37 mm table; OpenImpulse |
| 37GB 200 RPM BD listing | torque claim | "10 kg torque" (class floor used in this budget) | RoboTechShop product page |
| 37GB / JGB37-550 | weight | 300–320 g | Handsontec; PrecisionMiniDrives |
| MG996R servo | stall torque | 9.4 kg·cm @ 4.8 V; 11 kg·cm @ 6.0 V | TowerPro official page; TowerPro PDF (ElectronicosCaldas mirror) |
| MG996R | current | idle 10 mA; running ~500 mA; stall 1.4 A (TowerPro claim) – 2.5 A @ 6 V (Components101) | TowerPro; Components101; Tinkered.ai |
| MG996R | weight | 55 g, 40.7×19.7×42.9 mm | TowerPro |
| SLA 12 V 7 Ah | weight / size | 2.2 kg; 151×65×93.5 mm | RS PRO 12V 7Ah datasheet PDF (class-verified; Long/Marsriva units weigh on arrival) |
| BTS7960 driver | rating | 43 A max (listing claim); has over-temperature protection | RoboticsBD/Dream RC listings (BOM A2) |
| LM2596 buck | rating | 3 A max module | ElectroxBD/RoboticsBD listings (BOM A5) |

**Note on the 10 kg·cm floor.** The BD listing's "10kg torque" does not say stall vs continuous; vendors are loose here. Using it as the *capability floor* for sizing is conservative in the safe direction: if it is the continuous rating, actual stall capability is higher (the JGB37-550 family reaches 26–40 kg·cm at high ratios). If the unit then measures below 9 kg·cm in bench test T2, the contingency plan in §12 triggers.

---

## 3. Design assumptions (each with its measurement)

| Symbol | Value | Status | How it gets measured (bench test) |
|---|---|---|---|
| m — robot mass | 10.1 kg nominal / **12 kg design envelope** | computed §4; est items marked | Weigh assembled chassis + heaviest module on bathroom/kitchen scale |
| Crr — firm prepared path | 0.10 | assumption | **T1 pull test:** luggage scale drags robot at constant speed on the prepared path; Crr = F/weight |
| Crr — loose bed soil | 0.18 | assumption envelope | Same test on unplanted bed edge |
| η — gearbox+driveline | 0.75 | assumption (typical spur range 0.6–0.8) | Absorbed into T2 stall-margin check |
| μ — rubber/firm soil | 0.5–0.7 typical | assumption | Slip test: mark wheel, run 2 m, compare wheel-revolutions×circumference vs true distance (also calibrates odometry) |
| Stall current per drive motor | 7–20 A envelope | verified range, unit-specific value unknown | **T2 stall test:** clamp-meter/multimeter + lever-arm scale; measure current and torque together |
| Cruise current per motor | 0.8 A | estimate | **T3 current logging:** INA219 (~৳300, or team multimeter) on the prepared path |

The pull test is the single most important measurement in this document: it converts the weakest assumption (Crr) into a measured fact on the actual demo plot soil for the cost of a ৳300 luggage scale.

---

## 4. Mass budget (computed)

| Item | Unit | Qty | Subtotal | Basis |
|---|---|---|---|---|
| SLA 12 V 7 Ah battery | 2.20 kg | 1 | 2.20 | RS PRO datasheet (verified class value) |
| Chassis frame + fabrication | 1.80 kg | 1 | 1.80 | est — weigh before finalising |
| 37GB motors | 0.32 kg | 2 | 0.64 | 320 g (verified) |
| BTS7960 drivers | 0.09 kg | 2 | 0.18 | est |
| ESP32 + buck×2 + e-stop + wiring | 0.35 kg | 1 | 0.35 | est |
| Wheels + casters | 0.15 kg | 4 | 0.60 | est |
| Module interface plate | 0.20 kg | 1 | 0.20 | est |
| Transplanter module | 0.90 kg | 1 | 0.90 | 3×55 g servos verified; rest est |
| Weeding module | 0.65 kg | 1 | 0.65 | est |
| Sprayer module (incl. 1 L water) | 1.60 kg | 1 | 1.60 | 1 L water = 1.0 kg |
| Fourth module (heavy case: ridger) | 0.80 kg | 1 | 0.80 | pollination probe is 0.15; budget the heavy case |
| Encoders, fasteners, guards | 0.20 kg | 1 | 0.20 | est |
| **Nominal total** | | | **10.12 kg** | |
| **Design envelope (+15%)** | | | **12 kg** | used for worst-case torque |

The heavy-case fourth module (earthing-up ridger, per the fourth-operation analysis fallback) is budgeted here so the chassis is sized correctly whichever candidate wins the proof-of-concept gate.

---

## 5. Drive torque requirement (the decision table)

Formula per driving wheel: `F = Crr·m·g + m·g·sin(grade) + m·a`, then `T_motor = F·r / (n_drive · η)`.

| Case | m (kg) | Crr | Grade | Accel | Wheel | Drive | F total | Per-motor torque | Verdict vs ≥10 kg·cm floor |
|---|---|---|---|---|---|---|---|---|---|
| 1. Cruise on firm prepared path | 10.1 | 0.10 | 0° | 0.2 | 100 mm | 2WD | 11.9 N | **4.1 kg·cm** | OK — 2.4× margin |
| 2. **Design worst:** firm path + 5° + 0.5 m/s² | 12 | 0.10 | 5° | 0.5 | 100 mm | 2WD | 28.0 N | **9.5 kg·cm** | OK — inside floor |
| 3. Loose bed soil, level | 12 | 0.18 | 0° | 0.2 | 100 mm | 2WD | 23.6 N | **8.0 kg·cm** | OK |
| 4. Same worst case on 130 mm wheels | 12 | 0.10 | 5° | 0.5 | 130 mm | 2WD | 28.0 N | **12.4 kg·cm** | MARGINAL — exceeds floor |
| 5. Same worst case with 4WD | 12 | 0.10 | 5° | 0.5 | 100 mm | 4WD | 28.0 N | **4.8 kg·cm** | OK — 2× margin |

**Readings that change the build:**

- The **5° grade is the expensive term** (10.3 N of the 28.0 N). The demo plot is ours to prepare: keep the wheel path level (or ≤3°) and case 2 collapses to ~5–6 kg·cm — comfortable. This is a design requirement for the test plot, now written down where the plot builder will see it.
- **130 mm wheels hurt torque** (12.4 vs 9.5 kg·cm). Their ৳850-ea price made them a budget problem; physics now confirms they are also a performance problem for this drivetrain. 100 mm on a prepared path is the correct spec, and obstacle-crossing is managed by plot preparation, not wheel diameter.
- **4WD is the pre-priced escape hatch** (+৳1,860: two more 200 RPM motors + two wheels), halving per-motor torque and cutting required traction to μ = 0.25. It is triggered by measurements, not anxiety (§12 gates).

**Traction check (2WD worst case):** μ_required = 28.0 N / (12 kg × 9.81 × 0.60) = **0.40**, against rubber-on-firm-soil ≈ 0.5–0.7. Passes with thin margin — on damp morning soil the plot must be rolled/firmed; if the slip test shows spinning, the fix sequence is: firm the path → shift battery forward to load drive wheels → 4WD contingency.

---

## 6. Speed and PWM operating point

| Variant | Top speed @ 100 mm | 0.30 m/s operating duty | Note |
|---|---|---|---|
| **200 RPM (chosen)** | 1.05 m/s | **28.6%** | healthy PWM range; more torque per listing |
| 300 RPM | 1.57 m/s | 19.1% | low-duty operating point → coarser speed control |

Operating speed 0.30 m/s covers the transplanter row travel (2 m in 6.7 s) and keeps camera exposure/crop detection tractable. The 200 RPM choice gives the same operating speed at nearly double the PWM duty — better resolution from the ESP32's 8-bit LEDC PWM (1/256 steps ≈ 0.4% speed quantization).

---

## 7. Average current and runtime (computed)

| Consumer | Draw | Duty | Average |
|---|---|---|---|
| Drive motors | 0.8 A × 2 | 60% (moving) | 0.96 A |
| Peristaltic pump | 0.8 A | 20% | 0.16 A |
| Servos (sequenced) | 1.5 A | 15% | 0.22 A |
| ESP32 + WiFi | 0.25 A | 100% | 0.25 A |
| Buck/wiring overhead | +10% | — | +0.16 A |
| **Average total** | | | **1.75 A ≈ 21 W** |

| Depth of discharge | Usable | Runtime | Meaning |
|---|---|---|---|
| 30% DoD | 2.1 Ah | 1.2 h (72 min) | battery-health practice |
| 50% DoD | 3.5 Ah | 2.0 h (120 min) | max sensible |
| 80% DoD | 5.6 Ah | 3.2 h (192 min) | emergency only |

**A 45-minute demo/test session consumes 1.32 Ah = 19% of rated capacity.** The 7 Ah SLA supports a full morning of runs plus the showcase itself, recharged at lunch by the ৳400 SLA charger (BOM A11). Runtime anxiety is retired with arithmetic.

---

## 8. Peak current and protection (the honest part)

Worst-case simultaneous stall: 2 drive motors at 7–20 A each + 3 servos at 2.5 A + pump 0.8 A = **22–48 A**. A 7 Ah SLA is commonly rated to deliver ~5 C (35 A) short pulses; the top of the envelope exceeds that. Rather than hoping, three layers of protection — all cheap, all standard:

1. **Firmware stall cutoff (primary).** Sense current (INA219 on the main rail, ~৳300, or a multimeter during T3) and cut PWM to any motor drawing > 10–12 A for > 1 s — far below the 20 A single-motor stall, which makes the both-motors-stalled-forever case unreachable. Also protects gearboxes from stall damage. If the team's multimeter is spare, this costs ৳0.
2. **Main fuse 20 A automotive blade (time-delay characteristic)** — tolerates the 22–28 A transients for the seconds that matter, blows on genuine sustained faults; protects the 14 AWG harness (≈30 A chassis ampacity, short runs). Branch fuses: 10 A per motor, 5 A servo rail, 2 A logic rail.
3. **BTS7960 over-temperature protection** as the backstop, per its module design.

Connector/wire audit: XT60 (60 A) on the battery main — OK; 14 AWG silicone power runs (BOM A9) — OK for ≤30 A short runs; servo extensions 22 AWG — OK for ≤2.5 A stall each. All checks pass with margin.

---

## 9. Power-rail architecture and wiring rules (build this exactly)

```
SLA 12V 7Ah ── XT60 ── 20A blade fuse ── rocker main switch ──┬─ 10A fuse ─ BTS7960 #1 ─ motor L
                                                              ├─ 10A fuse ─ BTS7960 #2 ─ motor R
                                                              ├─ 5A fuse  ─ 5A UBEC ─ servo rail (5x MG996R) + 4700µF
                                                              ├─ 5A fuse  ─ peristaltic pump (via relay)
                                                              └─ 2A fuse  ─ LM2596 #1 ─ 5V logic rail: ESP32 + sensors + 1000µF
ESP32 3.3V GPIO ── BTS7960 EN/R_EN/PWM pins (logic level; verify V_IH at bring-up)
E-STOP (16mm button, logic-rated) ── pulls both BTS7960 EN+R_EN low ── AND ── ESP32 GPIO interrupt (safe-stow routine)
```

Wiring rules, each traceable to a failure mode:

1. **E-stop is logic-rated, not power-rated.** The ৳130 AB6-V button cannot break 20 A DC safely (its rating is small-signal AC). It must switch the driver-enable lines, not the motor supply. Physical battery disconnect is the 12 V rocker's job. This is the single most important wiring correction over a naive build.
2. **Servo rail must be separate from the logic rail.** Five MG996R servos can briefly draw 12.5 A at simultaneous stall; the LM2596 3 A logic buck would sag into brownout and reset the ESP32 mid-demo. Dedicated 5 A UBEC + 4700 µF at the rail + firmware move-sequencing (never command two simultaneous stall-torque moves) keeps the worst sustained case ≈ 6.5 A brief.
3. **Star ground.** Motor returns and logic returns join only at the distribution point. Chopped ground paths from motor current through the ESP32 ground are the classic source of phantom resets and ADC noise.
4. **Fuse every rail** as drawn; a module hot-plug fault (the quick-change interface invites them) must be able to blow a ৳10 fuse, not a ৳520 driver.
5. **Brownout caps:** 1000 µF at the 5 V logic rail, 4700 µF at the servo rail. ESP32 brownout is triggered in microseconds; caps bridge UBEC/servo sag overlap.

---

## 10. Battery decision (recorded so it isn't re-litigated)

| Option | Mass | Cost | Verdict |
|---|---|---|---|
| **SLA 12 V 7 Ah (BOM A10)** | 2.2 kg (verified) | ৳1,350 + ৳400 charger | **Chosen.** Flat 12 V, tolerant of over-current pulses, dumb charger, zero fire-safety protocol. Heaviest single component but the mass budget already carries it. |
| 18650 3S2P (6 cells + BMS + charger) | ~0.5 kg packed | ≈৳1,400–1,600 all-in | Lighter and higher energy density, but 3S sags to 9–12.6 V, needs a BMS and balanced charging discipline, and saves no money. Documented upgrade path for the microcontrollers-course version, not v1. |
| Team's 12 V jump-starter (dossier §8.4) | — | ৳0 | Remains **unverified** — read the label/manual for chemistry, Wh, and *continuous* (not peak) amps before any connection; never connect clamps to electronics. Keep as emergency backup only. |

---

## 11. Budget impact (updates the BOM totals)

New lines this budget requires, none previously priced:

| Add | Est (verify) | Why |
|---|---|---|
| 5 A UBEC / buck for servo rail | 300–450 | LM2596 3 A cannot carry 5 servos |
| 12 V rocker main switch | 60–120 | physical disconnect (e-stop is logic-only) |
| 4700 µF + 1000 µF caps | 40–80 | brownout protection per §9 |
| Spare blade fuses (20 A/15 A/10 A) | 80–150 | demo-day spares + branch fusing |
| **Total adds (mid)** | **≈640** | |

Updated totals from the BOM's scenario table:

| Scenario | Total (BDT) | Within ৳25,000? |
|---|---|---|
| S1+S4 (webcam reuse + 100 mm wheels) — BOM baseline | 24,834 | Yes (margin 166) |
| S1+S4 + power-system adds | 25,474 | **No — over by 474** |
| **S1+S4+S5 (also drop solenoid valve; pulse the pump) + adds** | **24,774** | **Yes — margin 226** |
| 4WD contingency + adds (only if tests T1/T2 force it) | 26,634 | No — over by 1,634; funded by cutting contingency H6 or supervisor top-up |

**Procurement posture update:** commit to **S1+S4+S5 + the four power adds**. Dropping the ৳700 solenoid is now justified twice over — pump pulsing gives metered droplets without it, and the money buys the servo rail the build actually needs. The current-sensing task (stall cutoff, T3) should start with the team's existing multimeter at ৳0; buy an INA219 (≈৳300) only from the ৳1,000 contingency (H6) if logging convenience proves useful during integration.

---

## 12. Bench verification protocol (replaces every assumption with a measurement)

| Test | Procedure | Replaces | Pass gate | On fail |
|---|---|---|---|---|
| **T1 — pull test** | Luggage scale drags the assembled chassis (with heaviest module mounted) at steady walking speed: 10 runs on prepared path, 5 on bed edge; Crr = F/weight | Crr 0.10/0.18 | Crr_firm ≤ 0.12 and F_pull < 14 N | Firm/roll the path material; re-check; if unreachable → 4WD contingency |
| **T2 — stall test** | Lock one wheel on a lever arm against the scale; full PWM for ≤2 s; record torque (kg·cm = kg-force × arm-cm) and clamp-meter amps together; 3 trials | "10 kg torque" claim; stall current 7–20 A | ≥ 9 kg·cm and ≤ 20 A | If 9–10: restrict grades ≤3° (fine for the plot). If < 9: invoke 4WD plan or 300 RPM variant swap |
| **T3 — cruise current logging** | Drive figure-8 laps on the path; log average current (multimeter series or INA219) | 0.8 A cruise estimate | ≤ 1.0 A per motor | Re-run runtime table with measured value (script is parameterised) |
| **T4 — slip/odometry test** | Mark wheel; drive 2.0 m; compare encoder-derived distance vs tape measure; 5 trials | μ 0.5–0.7 assumption | slip ≤ 10% | Firm the path; move battery over drive axle; then 4WD |
| **T5 — sag/stall integration** | Deliberately stall a drive motor at full PWM with main fuse installed; observe fuse holds, stall cutoff trips < 1 s, rail sag < 0.5 V on logic rail, no ESP32 reset | §8/§9 protections | no reset, cutoff trips | Add cap size / re-route grounds until it passes — before any AI integration |

T1–T3 run in Week 1–2 on the first-purchase chassis (BOM §4 lists exactly these parts, ~৳5,000), which is also the dossier's own risk-first ordering. T4/T5 gate the module-interface freeze (dossier §17 action 8).

**Decision gates (pre-committed so nobody re-argues with feelings):**
- T1 fails → firm the path; still failing → 4WD (+৳1,860, budget per §11).
- T2 < 9 kg·cm → swap to 300 RPM full-metal variant (+৳598) or 4WD; decide by which measurement failed (torque vs current).
- T5 reset persists after cap/ground fixes → separate battery for logic rail (use the jump-starter only after its label verification clears it).

---

## 13. What remains genuinely unknown (and who owns it)

1. **Unit-specific stall torque/current of the purchased 37GB units** — measured in T2 on arrival; the 7–20 A envelope is datasheet-level truth, not unit truth.
2. **Actual plot soil rolling resistance** — measured in T1; the 0.10/0.18 envelope is a literature-level assumption pending the plot's existence.
3. **Long/Marsriva SLA unit weight vs the 2.2 kg class value** — weigh on arrival (affects mass budget ±0.4 kg).
4. **BTS7960 3.3 V GPIO compatibility** — the module is commonly driven by 3.3 V MCUs; confirm at bring-up before wiring EN permanently (5-minute test).

---

## 14. Sources

**Datasheets (specifications):**
- Handsontec — JGB37-550 Geared Motor datasheet PDF: handsontec.com/dataspecs/motor_fan/JGB37-550-Geared%20Motor.pdf (free-run 1.1 A, stall 20 A @ 12 V, gear table)
- Scribd copy of JGB37-550 datasheet: scribd.com/document/451905802 (corroborates currents)
- PrecisionMiniDrives — 37 mm JGB37-550 parameter table: precisionminidrives.com (rated torque 0.7–40 kg·cm, 320 g)
- OpenImpulse — JGB37-550 gearmotor selector: openimpulse.com/blog (12 V variant row: 7 A stall, 26 kg·cm)
- TowerPro — MG996R official specification: towerpro.com.tw/product/mg996r (55 g, 9.4/11 kg·cm, idle 10 mA)
- TowerPro MG996R PDF mirror: electronicoscaldas.com/datasheet/MG996R_Tower-Pro.pdf (running 500 mA)
- Components101 — MG996R datasheet page: components101.com/motors/mg996r-servo-motor-datasheet (stall 2.5 A @ 6 V)
- RS PRO — 12 V 7 Ah lead-acid battery datasheet PDF: docs.rs-online.com/8e84/A700000009435584.pdf (2.2 kg, 151×65×93.5 mm)

**Bangladesh retailer listings (prices, from BOM §5):** RoboTechShop 37GB 200 RPM ৳850 ("10kg torque"); Dream RC 37GB full-metal 300/500 RPM ৳1,149; RoboticsBD 37GB 300 RPM ৳1,500, BTS7960 ৳490, MG996R ৳354; TechLand SLA 12V7Ah ৳1,350.

**Concepts and typical values (not build inputs):**
- EngineeringToolBox — rolling friction/resistance overview: engineeringtoolbox.com/rolling-friction-resistance-d_1303.html
- Robotics StackExchange — wheeled-robot force/motor sizing method: robotics.stackexchange.com/questions/12848
- Lippert & Speck — *Rolling Resistance and Industrial Wheels* whitepaper (tread-material vs surface coefficient discussion)

*All computations: `scripts/compute_power_budget.py` (this repo). Assumptions are deliberately visible so the bench tests can replace them; nothing in this document should be treated as verified until its corresponding test number exists in the failure log.*
