# Project Selection Brief — Choosing What to Build for EEE 2124 / UIU CSE Project Show

**Date:** 26 November 2026
**Status it supports:** the team has **not finalized the project**. The CropGuard AI dossier is the most-developed candidate but is not locked.
**Inputs (all in `selection/sources/`, extracted text in `selection/extracted/`):**
1. `Curated Project Problems.docx` — the course teacher's problem menu
2. `CSE Project Show _ Summer '26 .xlsx` — all 36 registered teams this season (sanitized scan: `../competition-scan-summer26.md`)
3. `_Previous Projects_ 261.xlsx` — 23 earlier project entries with drive links
4. `Project Video Submission Guidelines-CSE-2124.docx` — **official evaluation rubric** + 10-minute video format (filename says CSE-2124, content header says EEE 2124 Electronics Laboratory — same document)
5. `Viva Preparation Guideline.docx` — 15-mark viva structure
6. `Project_Presentation_Template.pptx` — official 19-slide presentation skeleton
7. `Sample project report.pdf` ("Ingenious Kitchen") and `Project Proposal Sample.pdf` ("E-Mart") — UIU report/proposal format examples
8. `Journal Articles/IOT for Agriculture.pdf` — Chong et al., IoT environmental monitoring & control for mushroom cultivation (teacher-provided reference paper)
9. `docs/CropGuard_AI_Project_Dossier.docx` — the existing CropGuard candidate dossier

**Every claim below is traceable to one of those files. Judging weights, marks and video rules are quoted from the official guideline document — they are no longer assumptions.**

---

## 1. What the course officially grades (verified — closes dossier gap #4)

### Evaluation rubric (final grading in the project show)

| Criterion | Weight | What it rewards |
|---|---|---|
| **Features & Hardware Implementations** | **40%** | Implemented, demonstrated hardware features — the heaviest criterion by far |
| Project Idea & Novelty | 15% | A fresh idea — but less than a quarter of Features+Impact combined |
| Real-Life Application & Impact | 15% | Real users, realistic (not exaggerated) use cases |
| Cost Effectiveness | 10% | Performance-vs-cost, component-wise breakdown |
| Tidiness & Professionalism | 10% | Build quality, wiring, stability |
| Presentation | 10% | Slides + narration quality |

### The 10-minute demonstration video (submission gate for recommended teams)

- English mandatory, max 10 min (over-length loses marks), slides allowed everywhere **except** the feature demo, which must show the real hardware live.
- Required flow: (1) intro/problem, (2) real-life applications, (3) **minimum 3 features** + block diagram + named components (MCU, sensors, motors, power) with *why chosen*, (4) live feature-by-feature demo (inputs → sensor/actuator → output), (5) **component-wise cost breakdown + total + justification**, (6) future plans, (7) conclusion.
- Upload to the drive link given in the show registration form by the committee deadline; folder must be public-viewer.

### The 15-mark viva (course component)

| Viva block | Marks |
|---|---|
| Name all sensors/actuators/MCU modules | 3 |
| How the sensors really work (IR twin-LED, PIR fresnel, MPU acceleration, DC vs stepper vs servo, encoders) | 3 |
| How the MCU controls actuators (PID, speed feedback, filters, ML/DL models used) + operate it live | 4 |
| Code walkthrough: reading sensor data, denoising, intermediate features, actuator control, dashboard, WiFi | 5 (approx. — remaining weight) |

Printed connection diagrams, flowcharts and code may be brought to the viva but not shared with other teams.

### Deliverable templates (format expectations)

- **Proposal** (E-Mart sample): abstract → project overview → component list with pin diagrams + per-component features.
- **Final report** (Ingenious Kitchen sample): IEEE-style — abstract, overview, numbered component list with figures, working principle per part, code listings, web-source references.
- **Presentation**: fixed 19-slide skeleton (title → motivation → solution → components → sensor/actuator deep-dives → MCU wiring → complete connection diagram → control logic → code → demo → results → conclusion).

**Direct consequences for any candidate:**
1. 40% sits on *working, demonstrated hardware* — feature count and demo stability dominate. A project with 3–4 robust features beats a project with 6 flaky ones.
2. The video's section 5 *is* a priced BOM — the BOM work already done for CropGuard transfers verbatim.
3. The viva rewards depth on exactly the parts the power budget covers (encoders, DC/servo differences, PWM, filtering) — engineering-process evidence pays twice.

---

## 2. The allowed problem space (teacher's menu)

The curated problems doc gives two directions plus a suggestion table:

1. **Sensor-based data acquisition, storage, analysis + visual dashboard** — worked examples: patient monitoring (BPM/SpO2 → SD card → cloud → dashboard), and **energy harvesting** (wind + solar + piezo meeting part of a location's demand, e.g., bus-shed scenario).
2. **Motion & robotics (IMU sensors)** — self-balancing monocycle, robotic arms, drones, ornithopters, cars, CNC machines.
3. Suggestion table categories: robotics (LFR, BT car, autonomous boat, robotic arm), manufacturing (CNC pen plotter), **smart agriculture (hydroponics, smart irrigation)**, renewable energy (solar monitoring, home/kitchen energy management), IoT/smart home, AI/TinyML/CV (waste sorting, attendance, object detection), healthcare (health monitoring, medicine reminder).

**Fit check:** a multi-operation agricultural robot is inside the menu (Smart Agriculture + Motion & Robotics). So are all the alternatives considered in §6. Nothing in the menu rules CropGuard out; nothing forces it either.

---

## 3. The field you would enter (Summer '26, 36 registered teams)

Full sanitized table: [competition-scan-summer26.md](competition-scan-summer26.md). Computed headline:

| Cluster | Teams | Share |
|---|---|---|
| Agriculture & aquaculture | 10 | 28% |
| Rescue / security rovers | 6 | 17% |
| Assistive devices | 4 | 11% |
| Other (comms, pet care, vending, misc) | 4 | 11% |
| Energy & power | 4 | 11% |
| Monitoring & IoT dashboards | 4 | 11% |
| Road & personal safety | 2 | 6% |
| Environment & water | 1 | 3% |
| Instrumentation & 3D scanning | 1 | 3% |

**The three direct concept collisions with CropGuard:**
- **Team RuBiSTa** — "smart multi-purpose agricultural robot … through mobile control"
- **Team Phoenix** — "autonomous agricultural robot … monitor farming conditions and automatically irrigate … sensors, IoT, robotic control"
- **Breadboard Bandits** — "Smart Agriculture Rover … ploughing, seed sowing, and targeted water and pesticide spraying, real-time field monitoring through an onboard camera and mobile control"

Breadboard Bandits in particular is the *same top-level concept* as CropGuard (multi-operation agri rover + camera + mobile control). Plus 5 irrigation-style teams (Green Leaf, Zero, Photon Grove, Vertex, 4Logn) and Pond Guard's aquaculture device.

**What is *not* in the field:** energy *harvesting* (0 entries), CNC/pen-plotter (0), mesh communication (1), instrumentation/3D scanning (1), machine-vision manufacturing (0). If differentiation on "first on the floor" grounds matters, these are the open lanes — see §6.

**Previous years** (`_Previous Projects_ 261.xlsx`, 23 entries): hydroponic nutrient management, ESP32 self-sustaining garden, pond monitoring (BlueCycle), SCARA arm, CNC pen plotter, patient monitor, nurse-assistant robot, flood/rescue rovers, wall-climber, drowsiness detection, battery analyzer, mosquito bat, smart road bin, traffic controller, inverter. The agri-monitoring cluster is a *recurring* pattern — but **no previous entry built a multi-operation field robot**, and none of the previous entries shows the process-evidence style (priced BOM, power budget, reliability gates) that the repo now carries.

---

## 4. CropGuard AI scored against the verified rubric

| Rubric criterion | Weight | CropGuard's evidence today | Gap / risk |
|---|---|---|---|
| Features & hardware | 40% | Four genuinely distinct operations on one base; module-swap interface; power-rail design; bench tests T1–T5 defined | **Schedule risk is the #1 threat.** 4 mechanical modules in 2–3 months for 4 students is heavy. If only 2 modules work by video time, the score collapses toward 20/40 rather than 35+/40. Mitigation: the video needs *minimum 3* features — freeze 3, treat the 4th as upgrade |
| Novelty | 15% | Buzz-pollination assist (no one else, and rare in literature at this scale); transplanting on raised beds | Agri robots are 28% of the field — the *category* is not novel. Novelty must be claimed at the operation level, never as "agri robot" |
| Real-life impact | 15% | Brinjal/raised-bed labour story, DAE-verifiable practice | Needs the real bed measurements (dossier §17.1) to stay concrete |
| Cost effectiveness | 10% | Priced BOM: ৳24.8k scenario with line-by-line sources; video section 5 ready-made | Fabrication quotes still unverified (est items) |
| Tidiness | 10% | Rail architecture, fusing, star ground, e-stop rules — unusually engineered for a student build | Only pays off if the physical build matches the documents |
| Presentation | 10% | 3-min booth script exists; 19-slide template maps cleanly; metrics board planned | 10-minute English video must be produced — new deliverable, needs owner + rehearsal |

**Viva fit:** strong. The bill of materials forces the team to *know* why BTS7960 over L298N, why SLA over 18650, why a UBEC rail — exactly the "how does it really work" marks. Encoder/PID/filter questions map to the odometry and current-logging work.

**Verdict: CropGuard is the highest-ceiling candidate in the field, and the only one whose evidence chain is already built. Its dominant risk is execution bandwidth, not concept.**

---

## 5. Honest alternatives (from the teacher's menu), quickly scored

| Alternative | Field density | Hardware/demo character | Why choose it | Why not |
|---|---|---|---|---|
| **CropGuard AI (4 ops)** | 28% agri, 3 direct collisions | High wow, high risk | 40%-criterion fit; investment already made; pollination story is unique | Schedule; mechanical failures on stage |
| **CropGuard focused (3 ops: transplant + weeding + spray, pollination as stretch)** | same | Slightly less wow, meaningfully lower risk | Fits "min 3 features" exactly; each module gets polish + reliability gates; 4th module still shown if it passes its PoC gate | Loses the four-features framing in low-stakes settings |
| **Energy-harvesting bus stop (wind + solar + piezo)** | 0 entries | Medium wow, low mechanical risk | Only untouched lane; measurement-friendly (watt-hours logged); dashboard direction per teacher | Off-dossier (starts over); less emotionally memorable than a field robot |
| **CNC pen plotter** | 0 entries | Deterministic, repeatable demo | Safe 40% scorer; G-code depth for viva | Common in previous years (Arduino CNC plotter already an entry); novelty ceiling low |
| **Mesh communication device** | 1 entry (Team Eitt) | Hardware-light | Real-world BD flood relevance | Thin on actuators — weak against the 40% criterion |
| **Instrumentation (3D-scanner style)** | 1 entry | Technically deep | Viva gold | Already taken this season by a strong-looking entry |

---

## 6. Recommendation and decision gates

1. **Primary: stay with CropGuard AI, but reposition the pitch.** Never lead with "agricultural robot" — three teams own that line. Lead with: *"one base, four physically distinct field operations, each shown live with a measured pass-rate, on a priced ৳25k budget"* — and make **transplanting** and **buzz-pollination** the memorable moments, because no other team has either.
2. **De-risk the 40% criterion now:** lock the video's minimum-3 features as **transplanting, weeding, targeted spraying** (the dossier's own risk-first ordering), with pollination as the 4th if and only if its Week-5 gate passes (8/10). This keeps the full story available without betting the grade on the riskiest module.
3. **Decision gates (pre-committed):**
   - **Week 3:** gripper mock passes 8/10 pick-and-place on the tray → transplanting confirmed as headline. Below 6/10 → swap headline emphasis to weeding+spraying+pollination.
   - **Week 5:** fourth-operation PoC gate per `research/fourth-operation-analysis.md` → pollination vs earthing-up decided.
   - **Video-minus-2-weeks:** whichever 3 modules pass their gates get filmed; nothing half-working is ever shown live.
4. **New deliverables the official docs add (owner needed):** 10-minute English video (7-section flow), 19-slide deck from the template, IEEE-style final report from the sample's structure, viva prep sheet (sensor working principles + code walkthrough). The repo's existing research plugs into sections 3, 5 of the video directly.
5. **If the team wants to leave agriculture entirely**, the energy-harvesting lane is the only untouched, rubric-compatible option — but it forfeits the dossier, the BOM, the power budget and three weeks of analysis. That trade is only worth it if the team doubts its mechanical build capacity, not because of competition fear: the 40% criterion rewards *implemented features*, and the agri lane's 28% density is survivable when your entry is measurably better engineered.

---

## 7. Gap tracker update (dossier open decisions)

| Gap | Status |
|---|---|
| #4 Judging rubric unknown | **CLOSED** — verified weights (this brief §1) |
| #5 Competition scan | **CLOSED** — 36 teams scanned (`competition-scan-summer26.md`) |
| Video/deliverable formats unknown | **CLOSED** — rubric + templates in `selection/sources/` |
| #1 Priced BOM | Done (research/bom-priced-components.md); fabrication quotes still to verify in person |
| #2 Fourth operation | Analysis done; PoC gate pending (Week 5) |
| #3 Motor/power budget | Done (research/motor-power-budget.md); bench tests pending |
| Crop validation (brinjal vs tomato/chilli) | Open — local grower / DAE check |
| Real bed measurements | Open — dossier §17.1 |
| Official submission deadlines for Summer '26 | Open — monitor projectshow.uiucomputerclub.com |

---

*Prepared from the nine source files listed in the header. Judging weights, marks and video rules are quoted from `Project Video Submission Guidelines-CSE-2124.docx`; competition counts computed by `scripts/categorize_show_entries.py` from the registration sheet.*
