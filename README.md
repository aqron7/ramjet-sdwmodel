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
- [x] Diffuser sizing
- [x] Combustor sizing
- [x] Nozzle throat and exit areas
- [x] Station table and area distribution
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


**Diffuser and Station 4 — combustor entrance**

Subsonic diffusion from M = 0.679 to M = 0.2 in a diverging duct. No
shocks, so the process is treated as isentropic and total pressure is
unchanged through this section.

Area ratio from isentropic A/A* values: 2.9635 / 1.1097 = **2.67**.
The combustor entrance flow area is 2.67 times the diffuser inlet area.

| Property | Value |
|---|---|
| M | 0.200 |
| T | 498.1 K |
| p | 373.1 kPa |
| T0 | 502.1 K |
| p0 | 383.7 kPa |
| Diffuser area ratio | 2.67 |

Total temperature is constant from freestream through the diffuser:
T0 = T * (1 + 0.2 * M^2) = 502.1 K at Station 0, unchanged by shocks.
Total pressure at freestream is 451.9 kPa, of which 0.849 survives the
inlet, giving 383.7 kPa at the combustor.

**What the inlet accomplishes**

Ambient air at 223 K and 26.4 kPa arrives at the combustor at 498 K and
373 kPa. Static pressure rises by a factor of 14 and temperature more
than doubles, with no moving parts. That compression ratio is
comparable to a turbojet compressor stage, and it is the reason a
ramjet works without turbomachinery.

The 502 K total temperature is also worth noting on its own. Nothing
has burned yet. That heating comes entirely from bringing Mach 2.5 air
to rest, which is why thermal limits become a design driver as the
design Mach number rises.
## Method and sources

Isentropic and shock relations are taken from standard compressible
flow theory. Shock angles and property ratios were obtained from
published theta-beta-M relations and normal shock tables rather than
derived here. Atmospheric properties are from the US Standard
Atmosphere.

At the time of writing I have not taken a gas dynamics course. The
relations used are applied from reference material, and the assumptions
behind them are listed below rather than assumed to be understood.

**Combustor and Station 5 — combustor exit**

Constant-area combustor with heat addition, treated as Rayleigh flow.
Exit total temperature set to 2000 K, chosen as representative of
liquid-fueled ramjets: below the stoichiometric flame temperature for
hydrocarbon fuel in air, and lean enough to leave margin on wall
cooling.

**Thermal choking check.** Adding heat to subsonic flow drives it
toward Mach 1. At the combustor entrance M = 0.2, the Rayleigh table
gives T0/T0* = 0.1736, so the choking total temperature is

T0* = 502.1 / 0.1736 = **2892 K**

The 2000 K design target sits well below this, so the flow does not
choke and the design is feasible in a constant-area duct.

| Property | Value |
|---|---|
| M | 0.500 |
| T0 | 2000 K |
| p0 | 346 kPa |
| Combustor p0 ratio | 0.902 |
| Choking limit T0* | 2892 K |
| Area change | none (constant area) |

Exit Mach found by working back through the Rayleigh table:
T0/T0* at exit = 2000 / 2892 = 0.6916, which corresponds to M = 0.50.
Total pressure ratio across the combustor = 1.1141 / 1.2346 = 0.902.

The flow accelerates from M 0.2 to M 0.5 with no area change at all.
Heat addition alone does that, and it costs 9.8 percent of total
pressure in the process.

**Total pressure budget**

| Section | p0 ratio | Cumulative |
|---|---|---|
| Inlet (2 ramps + normal shock) | 0.849 | 0.849 |
| Combustor (Rayleigh) | 0.902 | 0.766 |

Every loss in the engine is accounted for here. The diffuser and nozzle
are treated as isentropic, so 76.6 percent of freestream total pressure
reaches the nozzle.

**Nozzle and Station 6 — exit**

Converging-diverging nozzle, treated as isentropic. The flow enters at
M = 0.50, accelerates to sonic at the throat, then expands
supersonically.

**Throat.** A/A* at M = 0.50 is 1.3398, so the throat area is
1 / 1.3398 = 0.746 of the combustor area. Converging section, as
expected for subsonic flow reaching Mach 1.

**Exit.** Sized for perfect expansion at the design altitude, meaning
exit static pressure matches ambient. Required pressure ratio is
26,436 / 346,000 = 0.0764, which corresponds to M = 2.32 and
A/A* = 2.233.

| Property | Value |
|---|---|
| M | 2.32 |
| T | 963.2 K |
| p | 26,436 Pa (= ambient) |
| a | 622.1 m/s |
| V | 1443.3 m/s |
| Throat contraction from combustor | 0.746 |
| Expansion ratio, throat to exit | 2.233 |

Static temperature from T = 0.4816 * T0 at M = 2.32, then
a = sqrt(gamma * R * T) and V = M * a.

## Performance summary

| Station | M | Note |
|---|---|---|
| 0 Freestream | 2.50 | 749 m/s, 26.4 kPa, 223 K |
| 1 After ramp 1 | 2.00 | p0 recovery 0.960 |
| 2 After ramp 2 | 1.57 | cumulative 0.936 |
| 3 After normal shock | 0.68 | cumulative 0.849 |
| 4 Combustor entrance | 0.20 | 498 K, 373 kPa |
| 5 Combustor exit | 0.50 | 2000 K, cumulative 0.766 |
| 6 Nozzle exit | 2.32 | 1443 m/s, ambient pressure |

**Specific thrust.** With the nozzle perfectly expanded there is no
pressure thrust term, so thrust per unit mass flow is simply the
velocity difference:

V_exit - V_inlet = 1443.3 - 748.6 = **694.7 N per kg/s of air**

The engine nearly doubles the flow velocity. That difference is the
entire thrust mechanism, and it comes from heat addition alone: no
turbomachinery, no moving parts anywhere in the flowpath.

**Where the losses are.** 15.1 percent of freestream total pressure is
lost in the inlet shocks and 9.8 percent in the combustor. The diffuser
and nozzle are treated as isentropic, so 76.6 percent survives to the
nozzle. The single largest loss in the engine is the normal shock at
the end of the inlet, at 9.2 percent on its own.

## Geometry

The analysis gives area ratios. Converting those to a drawable part
requires fixing one physical dimension and resolving the sonic
reference areas, both covered below.

**Sonic reference areas.** A* is the area at which a given flow would
reach Mach 1. It depends on total temperature, so heat addition in the
combustor changes it: the hot gas needs a larger throat to go sonic
than the cold gas did. The inlet-side stations therefore share one A*
and the nozzle-side stations share a different one, and the two cannot
be compared directly.

The link between them is the combustor itself. It is a constant-area
duct, so Station 4 and Station 5 have the same physical area even
though their A/A* values differ (2.9635 at M = 0.20, 1.3398 at
M = 0.50). Expressing every station relative to the combustor area A_c
cancels the reference and makes the set consistent.

**Size.** Combustor diameter fixed at 60 mm, chosen to keep the printed
model small enough for a desk and for a Makerspace printer bed when
split into segments.

| Station | A / A_c | Diameter ratio | Diameter |
|---|---|---|---|
| 3 Diffuser inlet | 0.374 | 0.612 | 36.7 mm |
| 4 Combustor entrance | 1.000 | 1.000 | 60.0 mm |
| 5 Combustor exit | 1.000 | 1.000 | 60.0 mm |
| Nozzle throat | 0.746 | 0.864 | 51.8 mm |
| 6 Nozzle exit | 1.666 | 1.291 | 77.4 mm |

Diameter ratios are the square root of the area ratios.

**Axial lengths.** Each conical section is sized from a chosen wall
half-angle, with L = (R_out - R_in) / tan(half-angle). Angles were
chosen from typical practice, not optimized.

| Section | Half-angle | Length | Start dia | End dia |
|---|---|---|---|---|
| Diffuser | 6 deg | 110.8 mm | 36.7 | 60.0 |
| Combustor | n/a | 150.0 mm | 60.0 | 60.0 |
| Nozzle convergence | 15 deg | 15.3 mm | 60.0 | 51.8 |
| Nozzle divergence | 13 deg | 55.4 mm | 51.8 | 77.4 |

Combustor length set at 2.5 combustor diameters. Total internal duct
length is 331.6 mm, excluding the external inlet ramps.

The flowpath dimensions above are the analysis result. Outer geometry,
wall thickness, cowl and mounting are modeling choices made separately
and do not feed back into the flow numbers.

**Inlet spike.** The centerbody is positioned by shock-on-lip: at the
design Mach the shock from the tip should land exactly on the cowl lip.
Further forward and air spills around the inlet, further back and the
shock enters the duct.

With beta = 33.77 deg and a cowl lip radius of 18.35 mm, the tip sits

L = 18.35 / tan(33.77) = 27.44 mm ahead of the lip plane.

Applying the same condition to the second shock, which runs at
12 + 41.5 = 53.5 deg from the axis, places the ramp corner 16.45 mm aft
of the tip at a radius of 3.50 mm. The spike radius at the lip plane is
then 8.39 mm.

| Point | x from lip plane (mm) | r (mm) |
|---|---|---|
| Tip | -27.44 | 0 |
| Ramp corner | -10.99 | 3.50 |
| Lip plane | 0 | 8.39 |
| Spike end | +25 | 0 |

A spike of radius 8.39 mm inside a cowl of radius 18.35 mm blocks about
21 percent of the inlet area, while the diffuser analysis treated that
station as a full circle. The spike is therefore tapered back to the
centerline over 25 mm so the duct is fully circular before the diffuser
begins its area change. Real inlets do not do this, and it is listed
below as a simplification.

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
