# Working Notes

## 2026-09-17 — Design point and Station 0

Picked Mach 2.5 at 10 km. Supersonic enough that the inlet physics is
interesting, low enough that a simple inlet is reasonable.

Atmospheric values from a US Standard Atmosphere table: T = 223.15 K,
p = 26,436 Pa, rho = 0.4127 kg/m^3. Sources round these slightly
differently, noting which one I used.

a = sqrt(gamma*R*T) = 299.4 m/s, V = M*a = 748.6 m/s.
Sanity check: sea level is about 340 m/s and drops with temperature, so
a lower value at 223 K is expected.

## 2026-09-17 — Area-velocity relation

dA/A = (M^2 - 1) * dV/V

Below Mach 1 the factor is negative, so narrowing speeds flow up. Above
Mach 1 it is positive, so narrowing slows flow down. Reason is density:
accelerating supersonic flow thins out faster than it speeds up, and
mass flow (rho * A * V) has to stay constant, so area grows.

At Mach 1 the factor is zero, so dA = 0. That is why a throat exists.
Sonic flow only occurs where area is at a minimum.

This sets the shape of the engine. The inlet converges because it is
slowing supersonic flow. The nozzle converges then diverges because it
accelerates subsonic flow to sonic, then supersonic past the throat.

## 2026-09-17 — Station 1, first oblique shock

Chose a 12 degree ramp. Picked for simplicity, well inside the
attached-shock range at Mach 2.5.

From the theta-beta-M relation, beta = 33.77 degrees (weak solution).

An oblique shock only processes the velocity component normal to the
shock, so M1n = M1 * sin(beta) = 1.390. That value goes into normal
shock tables as if it were a normal shock. The parallel component
passes through unchanged.

Results: M2 = 2.001, p2/p1 = 2.091, T2/T1 = 1.249, rho2/rho1 = 1.673,
total pressure recovery 0.96.

## Observation worth keeping

The 12 degree ramp cost 4 percent of total pressure. A single normal
shock at Mach 2.5 would have cost roughly 50 percent.

That is the argument for ramp inlets, and it is not obvious from the
geometry. The ramp looks like it is just redirecting air. What it is
actually doing is splitting one violent compression into several gentle
ones.

## 2026-09-17 — Resolving A* between cold and hot sections

Ran into a bookkeeping problem converting area ratios into diameters.
The diffuser ratio of 2.67 and the nozzle contraction of 0.746 are not
measured against the same reference. A* depends on total temperature,
and the combustor took T0 from 502 K to 2000 K, so the sonic reference
area is different before and after.

The fix is that the combustor is constant area. Station 4 and Station 5
are the same physical duct, so expressing everything relative to the
combustor area cancels whichever A* applies and the table closes.

Worth remembering as a general point: A* is a reference, not a location.
There is no requirement that the flow ever actually reaches Mach 1 at
that area, and the value changes whenever total temperature does.

## 2026-09-17 — Sizing

Picked 60 mm combustor diameter. Driven by printing and desk space
rather than by anything aerodynamic. Total internal duct comes out at
331.6 mm, roughly 5.5 combustor diameters, which is in the normal range
for a ramjet.

Angles were taken from typical practice: 6 degree diffuser divergence
to avoid boundary layer separation, 2.5 diameters of combustor length
for the flame to complete, 15 and 13 degree nozzle half-angles. None of
these were optimized.

The nozzle convergence came out at only 15.3 mm, which is very short.
That follows from the throat being barely narrower than the combustor,
which in turn follows from the combustor exit sitting at M = 0.5. If it
looks abrupt once sketched, dropping the convergence half-angle to 10
degrees stretches it to about 23 mm without changing any areas.

At roughly 420 to 450 mm overall with the ramps included, the part will
not fit a single printer bed. Plan is to split it lengthwise for a
sectioned view of the flowpath and again axially into segments with
alignment pins.

## 2026-09-25 - CAD model

Built the flowpath as a single revolve from the five station diameters,
then shelled outward 3 mm so the inner surface stays at the calculated
dimensions and material is added outside. Shelling inward would have
invalidated every area in the analysis.

Spike is a second revolve on the same axis, created as a separate solid
body since it does not touch the duct walls.

The nozzle convergence is visibly abrupt in the model, close to a step.
That follows from the throat sitting only slightly below the combustor
diameter, which follows from the combustor exiting at M = 0.5. Dropping
the convergence half-angle from 15 to 10 degrees would stretch it from
15.3 mm to about 23 mm without changing any areas. Not changed yet.
