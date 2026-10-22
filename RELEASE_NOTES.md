# Release notes | 2026-10-21 | Shared speed-axis motor performance plots (v2.5)

- Brushed DC, coreless DC, and brushless DC HTML motor simulators now use **output speed (rpm)** for the horizontal axes of all four supporting performance graphs. This replaces the redundant speed-vs-torque chart with a detailed torque-vs-speed view. The remaining graphs show motor current (A), mechanical output power (W), and efficiency (%).
- All five steady-state graphs in each web simulator use the same RPM limits and respect the **Locked / Auto-fit** selection. A dotted starting baseline and any pinned dashed reference appear throughout.
- A marker identifies the attainable operating speed on every supporting graph. A second marker identifies the modeled maximum power or efficiency, which must not be confused with a continuous rating. Stalled loads do not receive fictitious operating points.
- MATLAB v2.5 has the same speed-axis convention and comparison behavior in its brushed DC performance graphs. The MATLAB GUI remains **not natively runtime tested** for v2.5; v2.2 is the author-confirmed working version.
- Updated README, MODEL_NOTES, GitHub Pages link parameters, and optional MATLAB ZIP name. No motor physics equations were changed. All results remain educational, idealized predictions.

---

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
