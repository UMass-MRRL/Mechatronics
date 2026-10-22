# Model notes

These notes describe the **assumptions and limits** of the MIE 443 simulators. The goal is to understand cause and effect, not to reproduce a particular manufacturer's hardware.

## Motor models

The simplified motor dynamics are:

```text
L di/dt = V - R i - k_e omega
J d(omega)/dt = k_T i - b omega - tau_load
```

The models calculate winding resistance and motor constants from idealized construction choices. Gearboxes, friction, iron loss, and two-node thermal behavior use lumped approximations. Current-source operation assumes an idealized regulator with a voltage ceiling; motor electronics are not simulated in detail.

- **Brushed DC:** idealized windings and magnet circuit; no brush switching waveforms, armature reaction, or detailed saturation.
- **Coreless DC:** simplified self-supporting winding shell; actual end turns, adhesives, commutator, and manufacturability are not modeled.
- **Brushless DC:** equivalent averaged motor model. Switching between six-step and sinusoidal commutation changes the *illustration*, not the calculated inverter currents or torque ripple. Saturation flags indicate where the magnetic model is unreliable.

The motor plots show **model-predicted** torque, current, output power, efficiency, temperature, and transient response. Stall torque and maximum mechanical power are **not continuous-duty ratings**. Presets illustrate architectures, not calibrated maxon/FAULHABER products.

### Flywheel and gearing

The optional flywheel is a **solid steel disk** on the gearbox output shaft, using density `rho = 7,850 kg/m^3`:

```text
m = rho*pi*r^2*t
J_output = (1/2)*m*r^2
J_reflected_to_motor = J_output/N^2
N = motor speed / output speed
```

Thus a 10:1 reduction makes the motor see 1/100 of the flywheel inertia. The models omit gear-train inertia, disk hubs, and acceleration-related gearbox losses. The gear-efficiency input affects the opposing external load torque, not the reflected inertia calculation.

## Bus models

- **I²C:** example transactions, register values, pull-up RC behavior, and ACK/NACK. The trace omits arbitration, clock stretching, and detailed board timing.
- **SPI:** clock edges, active-low selection, and full-duplex transfers. The RC edge model does not validate a device's maximum clock rate or signal integrity.
- **UART:** ideal 8N1 transmission and fixed-center sampling. No oversampling, noise, jitter, or actual UART hardware implementation.

The I²C/SPI example uses the **Adafruit LSM6DS3TR-C breakout**. Its onboard level shifting makes the breakout suitable for 5 V controller logic; the bare LSM6DS3TR-C IC is **not** 5 V tolerant. Example measurement bytes and sample code are instructional, not hardware-tested.

## Verification status

Browser page loads and selected interactions and equations were tested during development. The simulations have **not** been calibrated against measured motors or verified with logic-analyzer captures.

Before using any result for actual hardware, consult primary documentation and make appropriate measurements.

**References:** [Adafruit breakout guide](https://learn.adafruit.com/adafruit-lsm6ds3tr-c-6-dof-accel-gyro-imu/pinouts) · [ST LSM6DS3TR-C datasheet](https://cdn-shop.adafruit.com/product-files/4503/4503_LSM6DS3TR-C_datasheet.pdf) · [NXP I²C-bus specification](https://www.nxp.com/docs/en/user-guide/UM10204.pdf)
