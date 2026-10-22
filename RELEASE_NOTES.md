# Release notes | 2026-10-21 | Classic motor torque-speed characteristic

- Added a prominent conventional **torque versus speed** graph to the brushed,
  coreless, and brushless web motor designers. X: output speed (rpm). Y:
  available output torque (mN·m).
- Marked stall torque, no-load speed, and the selected load operating point.
  Overload/stall cases mark the available stall torque, not impossible load torque.
- Pinned reference curves are shown dashed, and graph hover reports torque
  at the selected output speed. Original four torque-indexed performance
  curves remain unchanged beneath the new chart.
- Updated optional MATLAB GUI from v2.2 to v2.3: its primary chart uses the
  classic torque-speed orientation, spanning the top performance row.
  Current, power, and efficiency plots remain beneath it.
- Updated README and MODEL_NOTES. All six HTML tools remain standalone.
- Educational, theoretical use only. Plots do not establish rated torque,
  safe stall duration, or continuous-duty envelopes.
- Browser simulations have been regression-tested. MATLAB v2.3 still needs a
  native runtime check; the user previously verified that v2.2 opens.
