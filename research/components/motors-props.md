# Motors and Propellers: Relations, Methods and Decision Space

- **Author:** Kaeden Monroe (research drafted with Claude)
- **Date:** 2026-10-02
- **ClickUp task:** [T-03 — Spec motors and propellers](https://app.clickup.com/t/86bc66b5w)
- **Reviewer:** TBD

## Question

For a small fleet of outdoor, off-the-shelf PX4 multicopters spanning nano to ~550 mm, what relations and methods govern motor and propeller selection, what do typical motor/prop size ladders look like, who publishes usable thrust data, and what does the propulsion choice have to hand to PX4, the simulation, and the downstream ESC (T-04) and battery (T-06) tasks?

## Findings

Citations like [3] refer to the Sources table.

### 1. Governing relations and methods

#### 1.1 Required thrust

- Total thrust $T_{total} = m·g / h²$, where h is hover throttle as a fraction. This uses thrust ∝ throttle² (the AeroEval framework states T/W = 1/θ_hvr²) [8]. Per-motor thrust is T_total / N_rotors.
- Equivalent: TWR = T_total / (m·g). TWR 2 is hover at ~71%, TWR 2.5 at ~63%, TWR 3.3 at ~55%, TWR 4 at 50%.
- PX4 does not map throttle to thrust linearly (see 4.1). The square-law is an estimate, not the firmware's model.

#### 1.2 Hover-throttle and TWR targets (what the sources say)

| Source | Guidance |
|---|---|
| eCalc xcopterCalc help *(secondary, vendor tool)* [7] | TWR ≥ 1.8 good (hover ≤ ~60%); 1.2–1.8 limited maneuverability; < 1.2 cannot hover. Hover-throttle targets: < 70% camera platforms, < 60% aerial photography, < 50% FPV exploration, < 45% FPV race. |
| AeroEval multi-domain MDO paper (arXiv) [8] | Thrust margin by role: imaging 45% (hover 0.55, T/W ~3.3), delivery/agriculture/mapping 40% (0.60, ~2.8), inspection 50% (0.50, ~4.0), racing 80% (0.20, 25.0). Includes a "wall-turbulence gust margin" for inspection but gives no value in the parts read. Explicitly excludes stochastic wind. |
| PX4 docs [5] | Hover throttle below ~20% distorts stick rescaling (MPC_THR_HOVER). No required minimum TWR is stated. |
| X-TEAM, via frame.md *(secondary)* | 2:1 minimum for controllable flight; 1.5–2:1 for cruise/cinematic builds. |

The ranges disagree by design: they come from different mission roles. None are outdoor-gust specific.

#### 1.3 Hover power: momentum theory

- Ideal induced hover power per rotor: P_ideal = √(T³ / (2ρA)), with T per-rotor thrust, $\rho$ air density, A = π r² disc area [3].
- Induced velocity: $v_i = \sqrt{\frac{T}{2ρA})}$ [1].
- Actual mechanical power = P_ideal / FM, where FM is the figure of merit. Bauersfeld and Scaramuzza use FM 0.5–0.7, typically 0.6, for multicopter propellers [1]. Another source reports 0.7–0.8 for most rotors and a low 0.42 for some small UAV props [search summary, not opened].
- Whole vehicle: P_h = (m g)^1.5 / (FM · √(2ρ π N) · r) [1].
- Takeaway: hover efficiency improves with larger disc area (bigger, slower props). eCalc says the same: "low copter weight with maximum disk size" [7].
- Momentum theory ignores friction and assumes an unducted rotor [3].

#### 1.4 Propeller coefficients and rotational speed

- C_T and C_P depend on pitch/diameter and Reynolds number for small propellers [4][search summary]. UIUC tests are wind-tunnel measurements at low Reynolds numbers for off-the-shelf props (Volume 1: ~140 props, 7–19 in, ~3000–7000 rpm, static and advance-ratio runs) [4]. Small multirotor props spin faster than most of that range, so check the rpm overlap before applying the data.
- Empirical C_T/C_P models for small UAV props exist [Springer paper, paywalled, not opened].

#### 1.5 Endurance

- Bauersfeld and Scaramuzza's pen-and-paper estimate: endurance power ≈ 0.914 (± 0.032) × hover power, effective capacity C_eff = C·κ(P_cell) with κ a cubic in per-cell power, endurance = C_eff · 3.7 V · N_S · 3600 / P_motor, accurate to within ~10% for commercial drones [1].
- Rule-of-thumb usable capacity ~80% of rated *(secondary)* [10].


### 2. Size ladders: frame class to propulsion

Frame-class chart (vendor, from frame.md [11]) with additional typical pairings (all *(secondary)* unless noted):

| Class | Typical prop | Stator | KV / cells |
|---|---|---|---|
| Nano (~90 mm) | ~45 mm | coreless | Crazyflie 2.x: 27–29 g, 4–7 min flight [11]; motor/prop details not retrieved |
| ~100–120 mm | 2–3 in | 1102–1106 | 4000–6000+ KV [11] |
| ~210–250 mm | 5–6 in | 2207–2306 | 4S: 2300–2700 KV; 6S: 1700–2000 KV [12] |
| ~350 mm | 7 in | 2506–2808 | 6S: 1300–1600 KV [11][12] |
| ~450–500 mm | 8–10 in | 2216 (X500 v2) to 3508 | X500 v2: 2216 KV920, 1045 props, 4S, 20 A ESCs [6]; 10 in on 4–6S: 700–1000 KV, 3508 stators [12] |
| Large (reference) | 17 in+ | 5212 | Hobbywing V5212 275KV, 12S, 17 in prop, 3.5–4 kg per rotor, 14–16 kg AUW [13] |


Trade-offs (general):
- Larger, lower-KV, higher-S setups are more efficient in hover and lower current at the same power, but heavier motors and slower response.
- Smaller, higher-KV setups respond faster but run higher rpm and higher current per watt.
- Cell count (S) is shared with T-06 and T-04. Higher S lowers current for a given power but raises ESC and battery voltage requirements.

### 3. Vendors and published thrust data

No picks and no prices. This is who publishes data in a form a script could ingest.

| Source | What it offers | Format / access | Class coverage |
|---|---|---|---|
| **Tyto Robotics database** [14] | 900+ tested propulsion systems: 71 motors, 115 props, 35 ESCs. Thrust, torque, RPM, voltage, current, power, efficiencies. | Free online, account to upload; data exportable to their flight-time calculator (Sheets). License not stated. | Mixed. Hobby/FPV brands named (DYS, HQ Prop, Xoar); class coverage not confirmed. |
| **UIUC propeller database** [4] | Wind-tunnel C_T/C_P for ~140 (Vol. 1), 35 (Vol. 2), 17 APC 12–21 in (Vol. 4) props. Static and advance-ratio data. | Text data files per prop, plus plots; public. | Props only, 7–21 in. No motor data. Small multirotor props (< 7 in) mostly absent. |
| **Hobbywing** [13] | Full thrust tables per motor/prop/voltage: throttle, thrust, current, power, rpm, g/W, torque, temperature; tested at 25 °C, sea level. | Product web pages (HTML tables). | Large/industrial motors (V5212, X8, X9, X15). Small FPV classes not covered. |
| **T-Motor store** *(search summary, not opened)* | Test tables with KV, prop, voltage, current, power, rpm, torque, thrust, efficiency. | Product pages. | Mid to large UAV motors. |
| **iFlight** *(search summary, not opened)* | Product pages list peak current and max wattage and mention a "test report". | Test report contents not retrieved. | FPV classes (XING2 1404–3314). |
| **eCalc** [7] | Calculator with motor/prop/battery database and estimated prop constants. | Web tool; methodology partly published. | Wide; closed data. |


### 4. PX4 and simulation requirements

#### 4.1 Motor output and thrust curve

- PX4's thrust model: rel_thrust = THR_MDL_FAC · rel_signal² + (1 − THR_MDL_FAC) · rel_signal. 0 is linear, 1 is quadratic, 0.3–0.5 typical; PX4's basic guide suggests 0.3 for PWM and 1.0 for RPM-based ESCs. Re-tune the rate controller if changed [5].
- PX4 notes the PWM-to-static-thrust mapping depends strongly on battery voltage [5]. A thrust stand with thrust and command data can fit the factor.
- Motors must never stop when armed: set minimum PWM accordingly [5].
- MPC_THR_HOVER defaults the hover point for the throttle stick. Very low hover throttle (< ~20%) distorts rescaling.


#### 4.2 Handoffs to T-04, T-06, T-05

| To | Needs from propulsion |
|---|---|
| T-04 ESC | Peak and sustained per-motor current, supply voltage range, DShot/BDShot support, pole count |
| T-06 Battery | Cell count, hover and peak total current, flight-time target, voltage under load |
| T-05 FC | Number of outputs, DShot/BDShot capable timers |
| T-11 | KV × cell count × prop load, current vs ESC rating, prop diameter vs frame arm spacing |
| Software team | Thrust constant, max rpm, time constants, mass and inertia contributions |


## Sources

| # | Source | Link | Credibility | Date accessed |
|---|---|---|---|---|
| 1 | Bauersfeld & Scaramuzza, Range, Endurance, and Optimal Speed Estimates for Multicopters | https://arxiv.org/abs/2109.04741 (HTML version read) | Peer-reviewed preprint, primary | 2026-10-02 |
| 2 | Deters, Ananda, Selig, Reynolds Number Effects on the Performance of Small-Scale Propellers (AIAA 2014-2151) | https://m-selig.ae.illinois.edu/pubs/DetersAnandaSelig-2014-AIAA-2014-2151.pdf | Primary; PDF could not be read, cited from search summary only | 2026-10-02 |
| 3 | Wikipedia: Momentum theory | https://en.wikipedia.org/wiki/Momentum_theory | Secondary, standard result | 2026-10-02 |
| 4 | UIUC Propeller Database, Volume 1 (and Vols. 2, 4) | https://m-selig.ae.illinois.edu/props/volume-1/propDB-volume-1.html | Primary data (university) | 2026-10-02 |
| 5 | PX4: Multicopter PID Tuning Guide (advanced and basic) | https://docs.px4.io/main/en/config_mc/pid_tuning_guide_multicopter | Primary (official docs) | 2026-10-02 |
| 6 | Holybro: PX4 Development Kit X500 v2 | https://docs.holybro.com/drone-development-kit/px4-development-kit-x500v2 | Manufacturer | 2026-10-02 |
| 7 | eCalc xcopterCalc help | https://www.ecalc.ch/calcinclude/help/xcoptercalchelp.htm | Vendor tool, secondary | 2026-10-02 |
| 8 | Multi-Domain Physics-Based MDO of Multirotor UAVs (AeroEval) | https://arxiv.org/html/2607.22768 | Preprint; framework values, not experiments | 2026-10-02 |
| 9 | PX4 forum: Gazebo SDF file motor parameters definitions | https://discuss.px4.io/t/gazebo-sdf-file-motor-parameters-definitions/34747 | Forum, secondary; search summary only | 2026-10-02 |
| 10 | LiPo voltage / C-rating guides (Zbotic, Hobbyking blog, Grepow) | https://zbotic.in/lipo-battery-guide-voltage-c-rating-safety/ | Vendor/blog, secondary; search summary only | 2026-10-02 |
| 11 | frame.md (T-02), citing LIGPOWER chart and Bitcraze | research/components/frame.md | Internal, secondary sources | 2026-10-02 |
| 12 | UAVMODEL: FPV motor sizing / KV and cell-count guides | https://blog.uavmodel.com/fpv-drone-motor-kv-and-cell-count-matching-voltage-prop-load-and-thrust-optimization-2026-guide/ | Vendor blog, secondary; search summary only | 2026-10-02 |
| 13 | Hobbywing V5212 275KV product page (and X9/X15 pages) | https://www.hobbywing.com/en/products/hv5212275kv | Manufacturer, primary for own products | 2026-10-02 |
| 14 | Tyto Robotics: Database of Drone Motors, Propellers and ESCs | https://www.tytorobotics.com/blogs/articles/how-to-use-the-database-for-drone-motors-propellers-and-escs | Vendor, primary for own data | 2026-10-02 |
| 15 | PX4: DShot | https://docs.px4.io/main/en/peripherals/dshot | Primary (official docs) | 2026-10-02 |