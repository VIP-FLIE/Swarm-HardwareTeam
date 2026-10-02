# Drone Club: Hardware Team Problem Statement

*Status: Draft v1, 2026-09-18. Living document; revise as open questions are resolved.*

## 1. Background

The club has historically used a small number of DJI drones to capture video of the campus and turn it into 3D reconstructions (Structure-from-Motion, now Gaussian splatting). That work used commercial drones as black-box data-collection tools. The club is now pivoting from *using* drones to *understanding and building* them.

The club has two sub-teams:

| Team | Responsibility |
|---|---|
| **Software** | Model the drone in ROS 2 (simulation), with a focus on multi-drone coordination / swarming |
| **Hardware** | Design and build the physical drones |

## 2. Problem Statement

> The hardware team must build a small fleet of custom-assembled drones that can serve as a physical testbed for the software team's swarm-coordination research, but the team does not yet share a working understanding of how drones work, has no defined requirements or interface with the software team, and has no documentation to onboard current or future members. Without that foundation, we risk buying incompatible parts, building drones that don't match the simulation, and losing knowledge each time members graduate.

## 3. Goals

**Near term (MVP)**
1. A shared baseline of drone knowledge across the hardware team (components, function, flight physics, power).
2. A written objective and set of requirements for a swarm-capable drone platform.
3. A defined hardware/software interface so the simulation model and the real vehicle agree.

**Long term**
- Move from off-the-shelf parts toward a custom frame, custom PCB, and custom flight controller.
- Extend the platform to other missions: mapping / photogrammetry (returning to the original campus-capture work), competitions, research, etc.

## 4. Scope

| In scope (now) | Out of scope (for now) |
|---|---|
| Research and documentation of drone fundamentals | Custom flight controller / PCB design |
| Requirements for a swarm-capable platform | Competition-specific builds |
| Component selection for an off-the-shelf PX4 build | Mapping-grade payloads (camera gimbals, RTK GPS) |
| Hardware needed to simulate flight, power, and thrust | Large outdoor / long-endurance platforms |
| Defining the hardware/software interface | |
| A first small fleet of ~3 drones | |

## 4. Constraints

| Constraint | Detail |
|---|---|
| **Autopilot** | PX4 (drives flight-controller and companion-computer choices) |
| **Build approach** | Off-the-shelf parts for MVP; custom hardware is a later phase |
| **Experience** | Team is new to drones; onboarding material is a deliverable, not a nice-to-have |
| **Longevity** | Multi-semester; documentation must survive member turnover |
 find it.