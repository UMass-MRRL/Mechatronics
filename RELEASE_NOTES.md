# Release notes | 2026-10-21 | Motor torque-speed axis fix

**Problem:** Each motor's torque-speed chart automatically rescaled both
axes on every parameter update, so a large physical change looked like an
identical diagonal curve. This masked educationally important changes.

**Fixes across brushed, coreless and brushless HTML:**

- Initial baseline curve is automatically captured and displayed dotted.
- Conventional torque vs output speed axes default to a common, locked
  range (2.25× the initial speed and torque intercepts).
- Axis controls: **Locked to starting baseline**, **Auto-fit all curves
  and load**, and **Use current design as baseline**.
- The red dashed horizontal line shows the requested torque load, and a
  valid operating point is shown only for achievable speed/torque pairs.
- A zero-speed red cross represents unsatisfied demanded torque under a
  stall, distinct from physically delivered torque.
- Warnings flag clipped curves or loads in locked-axis mode.
- Original manual reference pinning and secondary performance charts remain.
- **No change to motor equations or numerical predictions.**

**MATLAB:** Added v2.4 with the same baseline/locked-axis/auto-fit/load
comparison. The native MATLAB application has not been executed here. The
prior author-verified v2.2 remains included as a fallback.

**Verification:** Chromium UI regression tests passed for all three motor
pages, including voltage changes, fixed and fitted scales, baseline reset,
overload indication, manual reference pinning, preset switching, and
initial numerical output comparison with the previous release.

**Scope:** Teaching/illustration only. No empirical motor calibration.
