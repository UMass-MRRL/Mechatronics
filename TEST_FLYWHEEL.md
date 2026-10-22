# Flywheel regression tests (v2.6)

- Steel disk rho = 7850 kg/m^3. With radius 8 mm and thickness 1 mm, mass is ~1.578 g, JL is ~0.5052 g cm^2.
- Gear 1:1: reflected inertia ~0.5052 g cm^2. Gear 10:1: ~0.005052 g cm^2. Gear 100:1: ~0.00005052 g cm^2.
- Cross-check zero radius/thickness => zero mass/inertia; doubling radius multiplies disk mass by four and inertia by sixteen.
- Compare numerical motor predictions to v2.5; they must match to floating-point rounding.
- MATLAB v2.6 native runtime not available in this environment.
