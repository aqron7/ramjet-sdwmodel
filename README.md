# Ramjet Design

An analysis-driven ramjet design, taken from first principles through
CAD to a printable model. The geometry is dictated by the flow
calculations, not the other way around.

## Design point

Mach 2.5 at 10 km altitude.

## Status

**Inlet compression complete.** Two 12 degree ramps followed by a
normal shock, 0.849 total pressure recovery.

Roadmap:
- [x] Freestream conditions at design altitude
- [x] Inlet shock structure and ramp count
- [ ] Diffuser sizing
- [ ] Combustor sizing
- [ ] Nozzle throat and exit areas
- [ ] Station table and area distribution
- [ ] SolidWorks model
- [ ] Engineering drawing
- [ ] 3D printed sectioned model

## Station data

**Station 0 — freestream (10 km, US Standard Atmosphere)**

| Property | Value |
|---|---|
| M | 2.5 |
| T | 223.15 K |
| p | 26,436 Pa |
| rho | 0.4127 kg/m^3 |
| a | 299.4 m/s |
| V | 748.6 m/s |

Speed of sound from a = sqrt(gamma * R * T), gamma = 1.4,
R = 287 J/(kg*K).

**Inlet shock structure**

| Station | Event | M | Shock p0 ratio | Cumulative recovery |
|---|---|---|---|---|
| 0 | Freestream | 2.500 | | 1.000 |
| 1 | Oblique shock, 12 deg ramp | 2.001 | 0.960 | 0.960 |
| 2 | Oblique shock, 12 deg ramp | 1.565 | 0.975 | 0.936 |
| 3 | Normal shock | 0.679 | 0.908 | 0.849 |

Ramp 1: beta = 33.77 deg, M1n = 1.390.
Ramp 2: beta = 41.5 deg, M1n = 1.326.

Station 1 static conditions: p = 55,278 Pa, T = 278.71 K,
rho = 0.6904 kg/m^3.

## Why the inlet has two ramps

An oblique shock only processes the velocity component normal to the
shock. The parallel component passes through unchanged, so the shock is
weaker than a normal shock at the same Mach number.

Shock losses also grow steeply with Mach number. Staging the
compression means each shock runs at a lower Mach, and several small
losses beat one large one.

Two inlet configurations were run at the design point:

| Configuration | Final M | Total recovery |
|---|---|---|
| One ramp, then normal shock | 0.577 | 0.692 |
| Two ramps, then normal shock | 0.679 | 0.849 |

The second ramp drops the Mach number ahead of the normal shock from
2.00 to 1.57, which cuts that shock's loss from 28 percent to 9
percent. Net gain is 23 percent more total pressure reaching the
combustor. Two ramps was selected.

This shows two ramps beat one. It does not show two is optimal. Three
would recover more still, at the cost of inlet length, weight, and
complexity. That tradeoff has not been evaluated here.

## Method and sources

Isentropic and shock relations are taken from standard compressible
flow theory. Shock angles and property ratios were obtained from
published theta-beta-M relations and normal shock tables rather than
derived here. Atmospheric properties are from the US Standard
Atmosphere.

At the time of writing I have not taken a gas dynamics course. The
relations used are applied from reference material, and the assumptions
behind them are listed below rather than assumed to be understood.

## Assumptions

- Calorically perfect gas, gamma = 1.4 constant throughout
- Inviscid flow, no boundary layer or friction losses
- Two-dimensional ramp treatment rather than a conical spike
- Sharp leading edges, attached shocks
- Weak shock solution at each oblique shock
- Normal shock sits at the design location, no spillage or unstart
- Steady, adiabatic flow outside the combustor
- No heat transfer through walls
- Ramp angles chosen for simplicity, not optimized

## Tools

SolidWorks for CAD. Hand calculations for all flow analysis. No CFD:
the flow is supersonic with shocks and combustion, and I do not yet
have the background to evaluate whether a CFD result is correct.

## Notes

Working calculations and decisions are in `notes.md`.
