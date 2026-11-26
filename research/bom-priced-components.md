# CropGuard AI — Priced Component BOM (Bangladesh Market Check)

**Date:** 26 November 2026
**Purpose:** Replace the dossier's planning-only budget allocations (dossier §13) with a component-level bill of materials priced against actual Bangladesh online-shop listings observed on 26 Nov 2026.
**Method:** Web search of Bangladeshi robotics/electronics retailers (TechShopBD, RoboticsBD, Dream RC, BDTronics, KathalTech, RoboTechShop, ElectroxBD, Daraz, TechLand, Skyland, Tekko, BigganProject, Droban, myGardenBD, and others). Prices are the listed retail prices found on 26 Nov 2026; each line cites its source. Items marked **est (verify)** are local-market estimates (workshop fabrication, hardware-store items) and must be confirmed in person — they are deliberately ranged, not invented point values.

**Rule carried over from the dossier:** do not buy motors before the torque/stall-current estimate, and do not choose the battery before the power budget. This BOM prices the *intended* architecture so the power budget has a cost envelope to work against.

---

## 1. Headline findings

1. **The ৳25,000 budget is achievable, but only with two disciplined choices:** reuse an existing laptop/phone as the AI camera (৳0 instead of ৳2,300) and use 100 mm wheels on a prepared path instead of 130 mm off-road wheels (৳160 instead of ৳1,700). With both choices the likely total is **৳24,834** — inside budget with ~৳166 of headroom, before any local-negotiation savings on fabrication.
2. **The dossier under-allocated the base platform.** Chassis (৳4,000–5,000) + motors/drivers (৳3,500–4,500) + ESP32/electronics (৳2,000–2,800) summed to ৳9,500–12,300, but a priced reality check for the same scope comes to **৳13,238 likely** (battery ৳1,350, off-road wheels ৳1,700, frame fabrication ~৳3,000, 2× BTS7960 ~৳1,038, 2× 37GB motors ~৳2,298). The base is the fixed cost of the project; the modules are where flexibility lives.
3. **Linear actuators are priced out of the project.** 75–300 mm 12 V actuators run ৳4,295–5,750 in Bangladesh — more than the entire transplanter allocation. The transplanter must be servo-based (winch lift + compliant gripper), which this BOM prices at **৳2,762 likely**, comfortably under its ৳3,000–4,000 allocation.
4. **Camera is the single biggest swing item:** C270 webcam ৳2,300 vs ESP32-CAM ৳1,370 vs existing laptop webcam ৳0. Use ৳0 for the core demo; buy a webcam only if the laptop camera cannot reach the bed.

---

## 2. Priced BOM by section

All prices in BDT. "Likely" = the price we would expect to pay at the cited mainstream shop; min/max = observed range across shops.

### A. Shared base platform

| # | Item | Qty | Min | Likely | Max | Source (BDT) | Notes |
|---|------|-----|-----|--------|-----|--------------|-------|
| A1 | ESP32 DevKit V1 (WROOM-32) | 1 | 490 | 520 | 640 | TechShopBD 490–520; BDTronics 640 | Main controller |
| A2 | BTS7960 43A motor driver | 2 | 490 | 519 | 550 | RoboticsBD 490; Dream RC 519 | One per drive motor |
| A3 | 37GB 12V geared motor, 300 RPM, high torque | 2 | 850 | 1,149 | 1,500 | RoboTechShop 850; Dream RC 1,149; RoboticsBD 1,500 | Full-metal gearbox preferred |
| A4 | Wheel encoder kit (IR/magnetic, pair) | 1 | 150 | 250 | 400 | est (verify) | 37GB has no encoder; needed for odometry |
| A5 | LM2596 buck converter | 2 | 70 | 101 | 240 | ElectroxBD 70; RoboticsBD 101; TechShopBD 240 (display ver.) | 12V→5V logic rail + spare |
| A6 | Emergency stop button 16mm AB6-V | 1 | 99 | 130 | 240 | BDTronics 99; RoboticsBD 130; Mikrowell 22mm 240 | Main e-stop |
| A7 | Blade fuse holder + fuses (15A/10A/5A) | 2 | 80 | 120 | 200 | est (verify locally) | Main + branch fusing |
| A8 | XT60 connector pairs | 3 | 60 | 120 | 150 | est (verify; widely stocked) | Battery + keyed module power |
| A9 | 14AWG silicone wire | 5 (2ft) | 78 | 78 | 100 | Droban 78/2ft | Power runs |
| A10 | 12V 7Ah SLA battery | 1 | 1,273 | 1,350 | 2,550 | Daraz 1,273; TechLand 1,350; Skyland (Long) 2,550 | Pending power budget; jump-starter alternative still unverified (dossier §8.4) |
| A11 | 12V battery charger (SLA) | 1 | 300 | 400 | 500 | est (verify locally) | Charge between demos |
| A12 | Off-road wheel 130×60 mm | 2 | 850 | 850 | 850 | RoboticsBD 850 | Soil traction; budget alt: 100 mm ~৳80 (Tekko) |
| A13 | Caster wheel 50 mm heavy duty | 2 | 280 | 280 | 525 | BDTronics 280; Daraz 525 (3 in) | Front/rear support |
| A14 | Chassis frame: MS sheet / aluminium angle + fabrication | 1 | 2,500 | 3,000 | 3,500 | est (local workshop) | Rigid geometry + tool clearance |
| A15 | Fasteners (M3/M4/M5 assort.), standoffs | 1 | 400 | 500 | 600 | est (local hardware) | Shared across all modules |
| A16 | Perfboard, headers, heat-shrink, zip ties | 1 | 250 | 300 | 400 | est (verify) | Wiring hygiene |

### B. Module interface (quick-change standard)

| # | Item | Qty | Min | Likely | Max | Source (BDT) | Notes |
|---|------|-----|-----|--------|-----|--------------|-------|
| B1 | Aluminium mounting plate/rail + alignment pins | 1 | 400 | 600 | 800 | est (local workshop) | Shared mechanical interface |
| B2 | Keyed connector set (XT60 + ID jumper block) | 1 | 150 | 250 | 350 | est (verify) | Module ID via resistor code (dossier §4.2) |

### C. Transplanter module (highest risk)

| # | Item | Qty | Min | Likely | Max | Source (BDT) | Notes |
|---|------|-----|-----|--------|-----|--------------|-------|
| C1 | MG996R servo (13 kg·cm) | 3 | 349 | 354 | 395 | Dream RC 349; RoboticsBD 354; TechShopBD 395 | 2× gripper fingers + 1× lift winch |
| C2 | Gripper fingers + compliant pads | 1 | 500 | 700 | 900 | est (workshop / 3D print) | Compliant contact for root plug |
| C3 | Brackets, guides, tray holder | 1 | 500 | 700 | 900 | est (local workshop) | Mounting + manual tray index |
| C4 | Seedling tray 105-cell | 2 | 150 | 150 | 580 | myGardenBD 150; Daraz premium 580/6pcs | Uniform plugs for repeatable demo |

### D. Weeding module

| # | Item | Qty | Min | Likely | Max | Source (BDT) | Notes |
|---|------|-----|-----|--------|-----|--------------|-------|
| D1 | Sweep blade / shallow hoe (tool steel, fab) | 1 | 600 | 800 | 1,000 | est (local workshop) | Adjustable depth + width |
| D2 | MG996R servo (blade sweep/lift) | 1 | 349 | 354 | 395 | RoboticsBD 354 | Actuation + safe stow position |
| D3 | Mount, guards, depth stop | 1 | 300 | 450 | 600 | est (local workshop) | Crop protection + finger guard |

### E. Targeted sprayer module (water only)

| # | Item | Qty | Min | Likely | Max | Source (BDT) | Notes |
|---|------|-----|-----|--------|-----|--------------|-------|
| E1 | Peristaltic dosing pump 12V | 1 | 850 | 850 | 855 | RoboticsBD 850; MegaShop 855 | Metered pulses; volume per pulse is measurable |
| E2 | Relay module 1ch 5V | 1 | 79 | 80 | 140 | RoboticsBD 80; Dream RC 79 | Pump/valve switching |
| E3 | Solenoid valve 12V (small 1/4in) | 1 | 639 | 700 | 1,990 | Daraz 639–696; TechShopBD 3/4in 1,990 | **Optional** — can pulse pump directly instead |
| E4 | Nozzle, tubing, small tank, drip tray | 1 | 250 | 300 | 400 | est (verify locally) | Containment + plumbing |

### F. AI / camera integration

| # | Item | Qty | Min | Likely | Max | Source (BDT) | Notes |
|---|------|-----|-----|--------|-----|--------------|-------|
| F1 | Logitech C270 webcam (720p) | 1 | 2,250 | 2,300 | 2,500 | Creatus 2,250; StarTech/TechLand/Ryans 2,300; Daraz 2,500 | **Option A** — buy only if laptop camera unusable |
| F2 | ESP32-CAM module | 1 | 1,370 | 1,370 | 1,370 | TechShopBD 1,370 | **Option B** — secondary streaming cam only; not needed together with F1 |

**Budget note:** the dossier says "use an existing laptop if available" — the cheapest correct choice is ৳0. The C270 price is listed so the decision is informed, not forced.

### G. Fourth module prototype reserve

| # | Item | Qty | Min | Likely | Max | Source (BDT) | Notes |
|---|------|-----|-----|--------|-----|--------------|-------|
| G1 | Vibration probe kit (vibration motor or MG996R tapper + probe) | 1 | 400 | 600 | 900 | est (servo 354 + fab) | Buzz-pollination candidate (see fourth-operation analysis) |
| G2 | Ridger blades pair + mounts | 1 | 900 | 1,200 | 1,500 | est (local workshop) | Earthing-up candidate |
| G3 | Black cards / transparent slides | 1 | 80 | 120 | 200 | est (stationery) | Pollen-capture measurement |

Only one of G1/G2 will be built; both are priced so the proof-of-concept gate can be run before locking the choice. G3 supports the pollination experiment regardless.

### H. Test plot, seedlings, consumables, contingency

| # | Item | Qty | Min | Likely | Max | Source (BDT) | Notes |
|---|------|-----|-----|--------|-----|--------------|-------|
| H1 | Brinjal seedlings (uniform, 25–30 pcs) | 1 | 300 | 400 | 600 | est (local nursery) | Spares for failed picks |
| H2 | Soil + compost for demo bed | 1 | 500 | 650 | 800 | est (local) | Controlled raised-bed plot |
| H3 | Weed seed/plants + test pots | 1 | 100 | 150 | 250 | est (local nursery) | Known weed targets |
| H4 | Food colouring (spray visualisation) | 1 | 80 | 100 | 150 | est (local) | Water + dye only (dossier safety rule) |
| H5 | Spare fuses, wire, fasteners | 1 | 300 | 400 | 500 | est (local) | Demo-day spares |
| H6 | Contingency reserve | 1 | 800 | 1,000 | 1,200 | — | Failures, replacements, reprints |

### Alternatives priced but NOT included in totals

| Item | Price (BDT) | Source | Verdict |
|------|-------------|--------|---------|
| 25GA370 12V encoder motor | 941–980/pcs | KathalTech 941; TechShopBD 980 | Built-in encoder but lower torque than 37GB; use only if drive loads prove light |
| NEMA17 stepper + A4988 | 1,380 + 171–180 | TechShopBD; Daraz | Metering/indexing duty, not drive |
| Linear actuator 75–300 mm | 4,295–5,750 | RoboticsBD 4,295 (75mm); TechShopBD 5,640 (300mm); eeeshopbd 5,500 (200mm) | **Exceeds transplanter allocation — avoid** |
| Brass solenoid valve 1/2in | 2,850 | RoboticsBD | Overpriced for water demo |
| 18650 3S pack route | cells 90–155/pc (RoboTechBD) + ~250–400 pack parts | RoboTechBD; RoboticsBD holder 35 | Lighter than SLA; needs safe BMS + proper charger; revisit in power budget |

---

## 3. Totals and budget scenarios

### Section totals vs dossier allocations

| Section | Min | Likely | Max | Dossier allocation | Verdict |
|---------|-----|--------|-----|--------------------|---------|
| A. Shared base platform | 11,272 | 13,238 | 17,510 | 4,000–5,000 (chassis) + 3,500–4,500 (motors) + 2,000–2,800 (electronics) | **Over — biggest cost centre** |
| B. Module interface | 550 | 850 | 1,150 | (new — not in dossier) | Reasonable |
| C. Transplanter | 2,347 | 2,762 | 4,145 | 3,000–4,000 | Under allocation ✓ |
| D. Weeding | 1,249 | 1,604 | 1,995 | 1,500–2,500 | Fits ✓ |
| E. Sprayer | 1,818 | 1,930 | 3,385 | 1,000–1,800 | Slightly over (valve optional) |
| F. AI / camera | 3,620 | 3,670 | 3,870 | 1,000–2,500 | Over **unless** laptop webcam reused |
| G. Fourth module reserve | 1,380 | 1,920 | 2,600 | 1,500–2,500 | Fits ✓ |
| H. Plot/consumables/contingency | 2,080 | 2,700 | 3,500 | 2,000–3,000 | Fits ✓ |
| **Grand total** | **24,316** | **28,674** | **38,155** | ~25,000 | See scenarios |

### Budget scenarios (from likely totals)

| Scenario | Change | Likely total | Within ৳25,000? |
|----------|--------|--------------|------------------|
| As specced (C270 + 130 mm wheels) | — | 28,674 | No |
| S1 — reuse existing laptop webcam | −2,300 | 26,374 | No |
| S4 — 100 mm wheels on prepared path | −1,540 | 27,134 | No |
| **S1+S4 — webcam reuse + 100 mm wheels** | −3,840 | **24,834** | **Yes** |
| S1+S4+S5 — also drop solenoid valve (pulse pump) | −4,540 | 24,134 | Yes, with margin |
| Spend floor (all minimum prices, as specced) | — | 24,316 | Yes (but no margin for error) |

**Recommended procurement posture:** commit to S1+S4 from day one (saves ৳3,840), buy the solenoid only if pump pulsing gives uneven droplets, and keep the ৳1,000 contingency untouched until demo week.

---

## 4. What this means for the build plan

1. **First purchases (Week 1, ~৳5,000):** ESP32, 1× BTS7960, 1× 37GB motor, wheels, buck converter, e-stop, wire, fuse holder — enough to drive a test chassis and calibrate stall current before buying the second drive motor and battery.
2. **Defer until the power budget is done:** battery + charger (A10, A11). The 37GB stall current and pump inrush decide 7Ah SLA vs 18650 pack.
3. **Fabrication quotes first:** get the chassis frame (A14) and gripper parts (C2, C3) quoted at a local workshop before ordering electronics — the ৳2,500–3,500 frame range is the least certain number in this BOM.
4. **Transplanter stays servo-based.** Do not buy linear actuators (৳4,295+). A servo winch lift with string/belt over a pulley is the cheapest controllable vertical motion and fits the module allocation with margin.
5. **Camera decision is free to defer** — test the team's existing laptop webcam against the bed view first; only then decide C270 (৳2,300) vs ESP32-CAM (৳1,370).
6. **Everything marked est (verify)** — chassis fabrication, gripper fabrication, weeder blade, encoders, XT60, charger, and consumables — needs in-person quotes. Treat the likely column as the planning number and the max column as the risk envelope, not the shopping list.

---

## 5. Sources

Bangladesh retailer listings observed via web search on 26 November 2026 (prices are point-in-time; re-check at purchase):

- TechShopBD — techshopbd.com (ESP32 DevKit V1 490–520; 25GA370 980; L298N 185; NEMA17 1,380; LM2596 w/display 240; solenoid 3/4in 1,990; ESP32-CAM 1,370; MG996R 390–395; linear actuator 300mm 5,640)
- RoboticsBD — store.roboticsbd.com (BTS7960 490; MG996R 354; peristaltic pump 850; LM2596 101; relay 1ch 80; e-stop 16mm 130; 65mm wheel 229; off-road 130×60mm 850; 37GB 300RPM 1,500; mini actuator 75mm 4,295; brass valve 2,850; 18650 holder 35; ESP32-DevKitC UE 2,960)
- Dream RC — dream-rc.com (MG996R 349/399; BTS7960 519; L298N 159; 37GB full-metal 1,149)
- KathalTech — kathaltech.com (25GA370 941)
- RoboTechShop — robotechshop.com (37GB 200RPM 850)
- BDTronics — bdtronics.com (ESP32 640; 37GB-550 1,606; e-stop 99; shaft coupler 252; caster 50mm 280; MG996R premium 730)
- ElectroxBD — electroxbd.com (LM2596 70)
- Daraz — daraz.com.bd (A4988 171–180; SLA 12V7Ah 1,273; solenoid 639–696; C270 2,300–2,500; relay 84–140; caster 3in 525)
- TechLand — techlandbd.com (SLA Marsriva 1,350; C270 2,300)
- Skyland — skyland.com.bd (Long 12V7Ah 2,550)
- Tekko (teamzlab) — 100mm rubber wheel 80
- BigganProject — bigganproject.bd (65mm wheel 75)
- Droban — droban.com (14AWG silicone wire 78/2ft)
- myGardenBD — mygardenbd.com (105-cell seedling tray 150)
- StarTech/Creatus/Ryans — C270 2,250–2,300
- TechBazar — techbazar.com.bd (solenoid 3/4in 1,070)
- eeeshopbd — eeeshopbd.com (linear actuator 200mm 5,500)
- RoboTechBD — robotechbd.com (18650 cells 90–155)

*Prices fluctuate; stock and availability vary. This document supports procurement planning — it is not a quotation.*
