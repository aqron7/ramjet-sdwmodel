# Ramjet Design

An analysis-driven ramjet design, taken from first principles through
CAD to a printable model. The geometry is dictated by the flow
calculations, not the other way around.

## Design point

Mach 2.5 at 10 km altitude.

## Status

**Inlet analysis in progress.** Station 0 and Station 1 complete.

Roadmap:
- [x] Freestream conditions at design altitude
- [x] First oblique shock (12 degree ramp)
- [ ] Remaining inlet compression to subsonic
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

Speed of sound from a = sqrt(gamma * R * T), with gamma = 1.4 and
R = 287 J/(kg*K).

**Station 1 — behind first oblique shock (12 degree ramp)**

| Property | Value |
|---|---|
| theta (deflection) | 12 deg |
| beta (shock angle, weak solution) | 33.77 deg |
| M1n (normal component) | 1.390 |
| M | 2.001 |
| p | 55,278 Pa |
| T | 278.71 K |
| rho | 0.6904 kg/m^3 |
| p0 recovery | 0.96 |

Ratios across the shock: p2/p1 = 2.091, T2/T1 = 1.249,
rho2/rho1 = 1.673.

## Why a ramp instead of a flat inlet

An oblique shock only processes the velocity component normal to the
shock. The parallel component passes through unchanged, so the shock is
much weaker than a normal shock at the same freestream Mach number.

At the design point, this 12 degree ramp costs 4 percent of total
pressure while more than doubling static pressure. A single normal
shock at Mach 2.5 would reach subsonic flow in one step but destroy
roughly half the total pressure. That difference is why supersonic
inlets stage several weak oblique shocks ahead of a final normal shock.

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
- Two-dimensional wedge treatment rather than a conical spike
- Sharp leading edge, attached shock
- Weak shock solution selected at each oblique shock
- Steady, adiabatic flow outside the combustor
- No heat transfer through walls

## Tools

SolidWorks for CAD. Hand calculations for all flow analysis. No CFD:
the flow is supersonic with shocks and combustion, and I do not yet
have the background to evaluate whether a CFD result is correct.

## Notes

Working calculations and decisions are in `notes.md`.
