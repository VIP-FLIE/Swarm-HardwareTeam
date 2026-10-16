# Drone Frame: Parameters to Consider

- **Author:** Kaeden Monroe (research drafted with Claude)
- **Date:** 2026-10-01
- **ClickUp task:** [T-02 — Spec drone frame](https://app.clickup.com/t/86bc66b5m)
- **Reviewer:** TBD

## Question

What parameters must the team weigh when choosing a frame for a small fleet (~3) of PX4 drones, and how does each one affect the downstream component choices (T-03 motors/props, T-05 flight controller, T-11 dependency map)?


## Findings

### 1. Parameters

#### 1.1 Payload scenario (drives everything else)

| | Scenario A: companion + vision | Scenario B: minimal / RC-style |
|---|---|---|
| Sensing for no-mocap indoor flight | Visual-inertial odometry (VIO): stereo or tracking camera, IMU, companion computer [5]. Optical flow plus rangefinder is also an option [5][6]. | Optical flow plus a downward rangefinder only [5][6] |
| Compute mass | Raspberry Pi 4 ≈ 46 g, Pi Zero 2W ≈ 10 g *(secondary)* [12]. Holybro Pixhawk + Jetson baseboard assembly ≈ 190 g [10]. ModalAI VOXL 2 module ≈ 16 g [9]. | None beyond the FC |
| Implication | Needs mounting plates and volume for the computer, cameras and cabling. Higher payload headroom is needed. | Small, light frames are viable. |

Notes:
- Optical flow needs a textured floor and enough light. The rangefinder needs about 4 m of range indoors [5][6].
- PX4 states optical flow is cheaper and easier to configure, while VIO is more flexible and enables obstacle avoidance but needs a companion computer and point features to track [5].
- Reference points for scenario A: ModalAI Starling 2 (PX4, indoor VIO) is 280 g with a 220 mm airframe and 120 mm props [9]. The Holybro X500 v2 dev kit has mounting holes for a Raspberry Pi 4 and Jetson-class computers [8].

#### 1.2 All-up weight (AUW) and thrust-to-weight ratio (TWR)

- General rule: 2:1 is the minimum for controllable, safe flight; 1.5–2:1 for cruising or cinematic builds; 4–6:1 for freestyle *(secondary)* [21].
- A common sizing check is hovering near 50–60% throttle so there is headroom for maneuvers *(secondary)* [21].
- Process: sum the mass budget (battery, FC, ESCs, motors, companion computer, sensors, radio, wiring, frame), pick a TWR, and the required thrust follows. Frame size class and T-03's motor/prop choice come from that number.
- Handoff: T-03 needs the AUW range from this document.

#### 1.3 Frame size class (wheelbase / propeller size)

Typical wheelbase-to-prop pairings from one vendor chart *(secondary)* [18]:

| Wheelbase | Prop | Typical motors |
|---|---|---|
| ~100 mm | 2" | 1102–1104, 6000+ KV |
| ~120 mm | 3" | 1104–1106, 4000+ KV |
| ~180 mm | 4" | 1806/2204, 2600–3000 KV |
| ~210 mm | 5" | 2205–2306, 2300–2600 KV |
| ~250 mm | 6" | 2206–2306, 2000–2300 KV |
| ~350 mm | 7" | 2506–2508, 1200–1600 KV |
| ~450 mm | 8–10" | 26XX+, ≤1200 KV |

Reference points across the range:
- **Nano (<100 mm):** Crazyflie 2.x: 92 mm motor-to-motor, 27–29 g, 4–7 min flight, built for indoor swarms (49-vehicle demonstrations) but uses motion capture for localization and has tiny payload [11].
- **~220 mm, ~280 g:** ModalAI Starling 2 [9].
- **500 mm class:** Holybro X500 v2: 500 mm wheelbase, 610 g frame, 144×144 mm body, 28 mm plate spacing; the listing gives payload ≈1 kg or 1.5 kg depending on the source, so the figure is inconsistent [8]. PX4's Gazebo simulation ships an X500 model with camera, depth and lidar variants [7].
- Frame "size" labels usually mean the prop diameter the frame supports *(secondary)* [17].

Trade-offs (general principles, partly secondary):
- Larger frame: more payload and efficiency headroom, but bulkier in a multi-drone room, higher crash energy, more cost per spare.
- Smaller frame: safer around people and cheaper, but limited payload and a harder fit for a companion computer.

#### 1.4 Rotor count and configuration

PX4 supports tri-, quad-, hexa-, octo- and larger multicopters in several geometries (+, X, H, wide, coaxial) [1][2]. Pre-defined airframes include Quadrotor +, X, H, Wide; Hexarotor coaxial; Octorotor coaxial and Octo Coax Wide [2]. Some layouts (e.g., Octo-H coaxial) have no ready airframe and need adaptation [2].

| Option | Pros | Cons / notes |
|---|---|---|
| Quad (X) | Simplest, cheapest, most frames/parts, matches PX4 defaults and the X500 sim model [1][2][7] | A single motor/ESC failure means loss of control *(secondary)* [20] |
| Quad H / wide / + | Different arm geometry, e.g., camera clearance | Different tuning/airframe selection [2] |

#### 1.5 Propeller protection and ducting (indoor safety)

- Ducts or guards are the conventional route for indoor flight near people *(secondary)* [22].
- Efficiency is contested across sources: well-designed ducts can raise static thrust 15–25% at hover, yet other sources report 15–25% thrust loss; ducts add drag at forward speed *(secondary, conflicting)* [22].
- Guards add weight and reduce flight time *(secondary)* [22].
- Open question for the team: guards as bolt-on accessories vs. frame-integrated.

#### 1.6 Frame material

| Material | Strengths | Weaknesses | Source |
|---|---|---|---|
| Carbon fiber (laminate/tubes) | Highest stiffness and strength per weight (density ~1.6 g/cm³). A 5" CF frame ~50–70 g vs ~80–120 g printed PETG | Brittle (shatters in hard crashes), conductive (shorts if a bare wire touches it), GPS/compass should be mounted on a mast ≥10–15 cm away *(secondary)* | [12][13][17] |
| Fiberglass | Cheaper, more flexible | Less stiff, heavier | [12] *(secondary)* |
| Printed nylon (PA6/PA12), PA12-CF | Tough, absorbs impacts, RF-transparent, cheap to reprint. Nylon toughness is ~5–6× PETG | Needs good print settings (≤0.1 mm layers, ≥80% infill, annealing for best results); CF-nylon stiffness still well below woven CF | [12][15][16] *(secondary)* |
| Printed PETG | Easy to print, yields gradually and bends before breaking | Heavier, less stiff, lower heat resistance than ABS/nylon | [14][15] |
| Printed ABS/ASA | Better strength/temperature resistance than PETG | Warping, fumes | [16] *(secondary)* |
| Aluminum (standoffs, plates) | Rigid, machinable, ~2.7 g/cm³ | Heavier than CF, conductive | [12][17] *(secondary)* |

Primary-literature support: two open-access papers cover PETG and composite filaments for drone parts [14][15]. Most other numbers above are from vendor or blog pages.

Hybrid pattern worth knowing: the X500 v2 uses CF twill plates and CF tube arms with fiber-reinforced nylon connectors [8].

#### 1.7 Structural stiffness and vibration

- PX4: more rigid frames are generally better because flex adds delay between motor action and the FC; motor arms should not be shock-mounted; well-designed airframes damp resonance at the autopilot mounting location [4].
- High vibration can cause clipping, estimation failures and flyaways. PX4 advises reducing vibration at the source (balanced props, quality parts, firm mounting) rather than relying on software filters [4].
- Frame implication: arm stiffness and plate rigidity affect tuning effort. Printed frames need design attention to this (min arm thickness, fillets at internal corners) *(secondary)* [16][17].

#### 1.8 Flight-controller mounting (hard handoff to T-05)

- Common patterns: 30.5×30.5 mm (M3) and 20×20 mm (M2), plus 25.5 mm and 16×16 mm; adapters exist between sizes *(secondary)* [23][24].
- PX4 mounting rules: top side up, arrow forward, as close to the center of gravity as possible (otherwise set EKF2_IMU_POS_X/Y/Z), and use the vibration isolation specified for the controller [3].
- Pixhawk-class FCs often use their own mounting patterns, so verify the actual FC's hole pattern before choosing a frame. Not yet checked per FC.

#### 1.9 Enclosure and component layout

Design considerations:
- **Plate spacing and stack height** (X500 v2: 28 mm between plates) must fit the FC stack, ESCs and companion computer [8].
- **Battery:** keep close to the center of gravity; use a strap or tray with adjustable position *(secondary)* [25].
- **FC at the CoG** [3][25].
- **Sensor sightlines:** the rangefinder points down; flow modules sit near the vehicle center or need configured offsets and yaw orientation [6]. Optical flow modules emit EM radiation and should sit away from GPS/other electronics [6].
- **GPS and compass:** carbon structures and motor wires can interfere. Use a mast or keep clear *(secondary)* [12]. Note ModalAI says GPS does not work on the Starling due to EM interference, so it relies on VIO indoors [9].
- **Cable routing, battery-swap access, props clearance, landing gear height.**
- **Mounting options** for scenario A: dedicated companion plate and camera mounts, as on the X500 v2 [8].


### 2. How the parameters interact

| Decision | Constrains |
|---|---|
| Payload scenario (1.1) | AUW (1.2) → size class (1.3) → motor/prop (T-03) → battery/ESC |
| Size class (1.3) | Prop guard options (1.5) |
| Rotor count (1.4) | Motor/ESC count, power distribution, airframe preset in PX4 |
| Material (1.6) | Weight, stiffness/vibration (1.7), GPS/compass placement (1.9), repairability |
| FC mounting pattern (1.8) | T-05 FC choice |
| Layout (1.9) | Sensor performance, CoG, simulation model parameters |

### 3. Decision-matrix criteria (for the team to weight)

Payload headroom (stated top priority), crash durability and spare cost, total cost, ease of build and tuning, indoor safety, repairability and availability, swarm footprint, fit with the PX4/sim model, and alignment with the custom-frame long-term goal.

### 4. Fleet and process considerations
- **Lead times and availability** for the chosen frame family; avoid single-source parts.
- **Simulation alignment:** the software team's ROS 2/PX4 simulation needs mass, inertia and arm length. PX4's Gazebo ships an X500 model and variants [7]; a different frame would need a custom model.
- **Documentation:** record the final choice, print settings (if printed) and assembly photos so knowledge survives turnover.

## Sources

| # | Source | Link | Date accessed |
|---|---|---|---|
| 1 | PX4 User Guide: Multicopter frames | https://docs.px4.io/main/en/frames_multicopter/ | 2026-10-01 |
| 2 | PX4 Airframes Reference (v1.13) | https://docs.px4.io/v1.13/en/airframes/airframe_reference | 2026-10-01 |
| 3 | PX4: Mounting the Flight Controller | https://docs.px4.io/main/en/assembly/mount_and_orient_controller | 2026-10-01 |
| 4 | PX4: Vibration Isolation | https://docs.px4.io/main/en/assembly/vibration_isolation | 2026-10-01 |
| 5 | PX4: Computer Vision (Optical Flow, MoCap, VIO) | https://docs.px4.io/main/en/advanced/computer_vision.html | 2026-10-01 |
| 6 | PX4: PMW3901-Based Flow Sensors | https://docs.px4.io/main/en/sensor/pmw3901 | 2026-10-01 |
| 7 | PX4: Gazebo simulation vehicles | https://docs.px4.io/main/en/sim_gazebo_gz/vehicles.html | 2026-10-01 |
| 8 | Holybro: PX4 Development Kit X500 v2 | https://docs.holybro.com/drone-development-kit/px4-development-kit-x500v2 | 2026-10-01 |
| 9 | PX4: ModalAI Starling 2 (and ModalAI product page) | https://docs.px4.io/main/en/complete_vehicles_mc/modalai_starling | 2026-10-01 |
| 10 | PX4: Holybro Pixhawk Jetson Baseboard | https://docs.px4.io/main/en/companion_computer/holybro_pixhawk_jetson_baseboard | 2026-10-01 |
| 11 | Bitcraze: Exploring the Swarming Potential of the Crazyflie; Crazyswarm paper | https://www.bitcraze.io/2025/06/exploring-the-swarming-potential-of-the-crazyflie/ | 2026-10-01 |
| 12 | Zbotic: Drone Frame Materials: Carbon Fiber vs Nylon vs PCB (also companion-computer weight article) | https://zbotic.in/drone-frame-materials-carbon-fiber-vs-nylon-vs-pcb-frame/ | 2026-10-01 |
| 13 | GetFPV: FPV Frame Materials | https://www.getfpv.com/learn/fpv-essentials/fpv-frame-materials/ | 2026-10-01 |
| 14 | PETG as an Alternative Material for the Production of Drone Spare Parts (PMC) | https://www.ncbi.nlm.nih.gov/pmc/articles/PMC11548261/ | 2026-10-01 |
| 15 | Composite Filament Materials for 3D-Printed Drone Parts (PMC) | https://www.ncbi.nlm.nih.gov/pmc/articles/PMC12155913/ | 2026-10-01 |
| 16 | Siraya Tech: Best Filament for Drone Parts (vendor) | https://siraya.tech/blogs/news/best-filament-for-drone-parts | 2026-10-01 |
| 17 | UAVMODEL: How to Choose an FPV Drone Frame; 3D printed frame design principles | https://blog.uavmodel.com/how-to-choose-an-fpv-drone-frame-geometry-materials-and-layout/ | 2026-10-01 |
| 18 | LIGPOWER: Drone Frame Size Chart (vendor) | https://www.ligpower.com/blog/drone-frame-size-chart.html | 2026-10-01 |
| 19 | Performance of Coaxial Propulsion in Design of Multi-rotor UAVs; Aerodynamic analysis of rotor-to-rotor interactions in octocopter configurations | https://www.researchgate.net/publication/297577792_Performance_of_Coaxial_Propulsion_in_Design_of_Multi-rotor_UAVs | 2026-10-01 |
| 20 | PX4 forum: Can Pixhawk/PX4 survive motor failure on hexacopter | https://discuss.px4.io/t/can-pixhawk-px4-survive-motor-failure-on-hexacopter/14197 | 2026-10-01 |
| 21 | X-TEAM: Thrust-to-Weight Ratio Explained | https://www.x-teamrc.com/thrust-to-weight-ratio-explained-2-1-vs-4-1-rule/ | 2026-10-01 |
| 22 | UAVMODEL: Cinewhoop Build Guide; Zbotic: Cinewhoop Drone Build | https://blog.uavmodel.com/cinewhoop-build-guide-ducted-fpv-drone-design-component-selection-and-tuning-2026/ | 2026-10-01 |
| 23 | RCWithAdam: Flight controller board size adapters | https://www.rcwithadam.com/flight-controller-board-size-adapters-fits-30x30mm-25x25mm-20x20mm-16x16mm | 2026-10-01 |
| 24 | ThinkRobotics: Complete Guide to Building Your First Drone | https://thinkrobotics.com/blogs/tutorials/the-complete-guide-to-building-your-first-drone-essential-components-explained | 2026-10-01 |
| 25 | Unmanned Tech Shop: FPV Centre of Gravity guide | https://www.unmannedtechshop.co.uk/blogs/knowledge-base/fpv-drone-center-of-gravity-balance-guide | 2026-10-01 |

## Confidence and gaps

- **Confident about:** PX4's supported layouts, FC mounting and vibration guidance, and VIO vs. optical-flow requirements (all primary PX4 docs [1]–[7]); the X500 v2 and Starling 2 headline specs (manufacturer docs [8][9]).
- **Unsure about / unverified:**
  - Material strength numbers, TWR rules of thumb and the size chart come from vendor or blog pages and are not verified against datasheets or tests [12][13][16][17][18][21].
  - Duct efficiency claims conflict between sources [22].
  - X500 v2 payload figures are inconsistent between listings [8].
  - The coaxial penalty figures come from a handful of papers I read only as search summaries, not full texts [19].
  - Companion-computer weights are from a blog and vendor pages, not datasheets [10][12].
- **Couldn't find / not yet researched:**
  - Current frame prices and availability for any candidate (no cost comparison).
  - Hole patterns of specific PX4-compatible FCs (input for T-05).
  - Existing open-source swarm frame designs (depends on T-01).
  - The team's room dimensions and fabrication equipment access.
  - T-01's conclusions, which may narrow the size class.
- Search-result summaries stood in for full reads of most pages. Open each cited page before relying on a number.

## Next actions

- [ ] Fix the task's doc reference: it cites `docs/output-standard.md`, the file is `docs/research-output-standard.md`.
- [ ] Assign a reviewer and assignee on T-02.
- [ ] Team decides weights for the decision matrix (section 3) and chooses candidate scenario(s) A/B.
- [ ] Collect candidate frames with price, weight, FC pattern and availability (new ClickUp task).
- [ ] Establish room size and fabrication access (printer, laser cutter).
- [ ] After T-01 lands, revisit coordination-model and size assumptions.
- [ ] Hand AUW range and FC mounting pattern to T-03 and T-05 once the frame is chosen.

## Change log

- 2026-10-01: initial version: parameter survey, no recommendation.
