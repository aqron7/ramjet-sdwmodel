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

## Next

Still at Mach 2.0. Combustor needs roughly Mach 0.2 to 0.3. Run two
options and compare total pressure recovery: a second ramp followed by
a normal shock, or a normal shock now.
