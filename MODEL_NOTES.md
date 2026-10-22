# Model assumptions and validation status

This document accompanies the six HTML teaching simulations for MIE 443 Mechatronics. It describes **what is actually represented**, not what a commercial motor, peripheral, or development board is guaranteed to do. Page and code comments are part of the teaching documentation.

## Status, scope, and definitions

- **Educational only.** No model or interface has been calibrated or qualified as an engineering design or hardware safety tool.
- **Software checks:** Prior development exercises included Chromium page loads, representative control/state interactions, transaction byte inspection, and selected analytical motor equation checks. For this documentation revision, page loads and controls are checked again. These checks do not establish comprehensive absence of defects.
- **Experimental validation:** Not performed for these release files. No systematic comparison to an identified motor's measured speed, torque, current, or temperature; no oscilloscope/logic-analyzer capture proving bus timing; no tolerance or uncertainty characterization.
- **Presets:** Illustrative parameter sets and form factors, not vendor-provided motor data or certified ratings. Brands mentioned to explain topology are not vendors of these simulations.
- **Visuals:** Scale bars/selected dimension ratios support intuition. Winding patterns, magnetic flux, internal structure, commutators, pole fields, and board layout remain conceptual drawings.

A checked equation can still provide a poor prediction when its assumptions are inappropriate. Conversely, a believable-looking curve does not establish that the underlying equations are correct.

## Brushed DC motor (`motor.html`)

Representative state equations in voltage-drive mode:

```text
L di/dt = V - R i - k_e omega
J d(omega)/dt = k_T i - b omega - tau_load,motor
```

In SI units, the model takes `k_e = k_T`. Wire length/resistance, an idealized magnet/air-gap circuit, lumped inertia, gearbox efficiency, and viscous friction determine the coefficients. The voltage-drive transient permits signed current. A simplified current-mode source saturates at a selected voltage; it is not a real current regulator or PWM/H-bridge model.

Not included: detailed armature winding/commutator waveforms, local pole saturation, magnetic leakage and armature reaction, brush voltage drop and sparking, bearing nonlinearities, gearbox backlash and individual mesh losses, supply sag, manufacturing tolerances, winding hot spots, and fully coupled electrothermal dynamics. Maximum output power is a **modeled** maximum on a calculated curve, not a continuous rating. Illustrative thermal thresholds are not safe-stall specifications.

## Coreless DC motor (`coreless.html`)

The simplified rotating-shell topology emphasizes magnet size, copper fill, winding turn count/style, inertia, and absence of iron rotor cogging. Winding volume, length, resistance, mass and inertia use the simulator's selected geometric idealizations rather than complete manufacturable winding construction. Differences between a skewed/rhombic and straight winding are model-dependent.

The modeled shell does not reproduce all self-supporting coil adhesives, end turns, commutator geometry, flux nonuniformity or assembly details. Manufacturer series and part-family names indicate **similar architectures**, not a validated simulation of a specific maxon or FAULHABER product.

## Brushless DC motor (`brushless.html`)

The simulator uses a lumped equivalent motor and an idealized slotless magnetic circuit. Poles, winding dimensions and yoke thickness affect calculated constants and an illustrative iron-loss term. The saturation indicator warns when the unsaturated model may no longer apply.

**Critical distinction:** The commutation selector visually contrasts block/six-step and sinusoidal patterns; the simulator does **not** independently solve distinct switching, phase currents, torque ripple, inverter losses, field-oriented control or sensorless estimation. Local linearized iron loss is neither a universal Steinmetz fit nor a valid zero-speed breakaway torque. Numerical outputs outside the saturation assumption remain visible for discussion, not design.

## I²C (`i2c.html`)

The page illustrates addressed transfers, START/STOP, bit order, ACK/NACK, repeated START, example MCU/peripheral behavior and example IMU registers. Rise-time intuition is based on a first-order pull-up/line-capacitance model. Example traffic is deterministic; bus arbitration, clock stretching, glitches, SMBus features, controller-specific delays and real device firmware behavior are not comprehensive.

The example Adafruit LSM6DS3TR-C **breakout** supports 3–5 V controller logic because it has a regulator and level shifting. The **bare sensor IC is not 5 V tolerant**. The breakout includes 10 kΩ I²C pull-ups. Check all other board pull-ups, the chosen supply voltage, device operating modes and actual bus speed before wiring. Example addresses and registers are grounded in the component references, but example measurement bytes are intentionally illustrative.

## SPI (`spi.html`)

The page illustrates independent active-low CS lines, clock phases/polarities, simultaneous data shifting, register exchange, and conflicting peripheral outputs. Its output-impedance and capacitance model is intended for first-order edge-rate intuition only. It does not certify clock frequency, timing margins, setup/hold times, chip-select requirements, line ringing, crosstalk, or specific microcontroller peripheral behavior. Conceptual code snippets are not independently compiled/tested Arduino library examples.

## UART (`uart.html`)

An ideal transmitter sends repeated 8N1 frames, least-significant bit first. The modeled receiver detects the first start edge and samples eight data centers and a stop-bit center at its own selected baud rate. Changing the transmitter rate changes bit duration, not the bit pattern; baud mismatch can shift samples to different transmitted bits.

The receiver does not model real oversampling, jitter, noise, false-start rejection, resynchronization, FIFO overruns, parity, baud generators or physical transceiver voltage levels. A HIGH stop sample does not prove correct data.

## Suggested student reporting language

> “The simulator predicted **X** under its assumed parameters. This is not a rated specification. Our independent calculation/measurement was **Y**, and the discrepancy may be explained by **Z**.”

Do not report the simulator's temperature threshold as a safe stall time, compare different preset motors as if all other factors were controlled, or cite model-derived maximum mechanical power as nameplate continuous power.

## Relevant primary documentation

- Adafruit LSM6DS3TR-C breakout: https://learn.adafruit.com/adafruit-lsm6ds3tr-c-6-dof-accel-gyro-imu/pinouts
- ST LSM6DS3TR-C datasheet: https://cdn-shop.adafruit.com/product-files/4503/4503_LSM6DS3TR-C_datasheet.pdf
- NXP I²C-bus specification (UM10204): https://www.nxp.com/docs/en/user-guide/UM10204.pdf

## Change history

**2026-10-21 publication-documentation revision:** Clarified scope in every simulator; renamed motor drawing headings; removed vendor-like descriptions from example preset labels; qualified output panels and thermal plots; inserted modeling comments adjacent to implementation; expanded README with interpretation guide, references, model notes, and experimental-validation status. The mathematical and protocol simulation algorithms were intentionally left unchanged; numerical equivalence should still be independently tested before formal classroom release.


## Conventional motor torque-speed chart (2026-10-21 update)

The three motor designs expose the theoretical steady-state **available torque**
(mN·m) against **output speed** (rpm), with the conventional axis orientation:
speed on X and torque on Y. The plotted stall intercept is the model's
instantaneous available output torque at zero speed, not a safe sustained
stall rating. The no-load intercept is calculated with modeled viscous losses,
not necessarily a measured datasheet no-load speed. The selected operating
point indicates the equilibrium under the user-specified constant load;
when this load exceeds stall capability, the motor is marked stalled at its
available stall torque instead of falsely plotting an impossible operating torque.

For voltage drive and positive constant coefficients, the plot is linear.
For current drive, an ideal instantaneous current ceiling can produce a
piecewise-linear characteristic, limited ultimately by the modeled supply
voltage. Brushless magnetics and commutation remain averaged/idealized.
Motor performance curves must not be used as continuous operating envelopes.
