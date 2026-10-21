# MIE 443 | Interactive Mechatronics Simulators

**University of Massachusetts Amherst**  
Department of Mechanical and Industrial Engineering  
Frank C. Sup IV

Six interactive, standalone browser-based teaching simulations covering **electric motor design**, **motor dynamics**, and **digital communication protocols**. They help students investigate relationships, interpret equations, and formulate questions for laboratory testing. The motor designers are **first-principles conceptual models**, not reconstructions of specific commercial motors; the bus inspectors are **transaction/timing illustrations**, not hardware emulators.

![Overview of the six MIE 443 simulators](assets/overview.png)

> [!IMPORTANT]
> **Educational use only.** These simulators are idealized instructional models, not validated engineering design software, hardware test instruments, or safety-analysis tools. Do not use their outputs to select or rate components, establish operating limits, design safety-critical systems, or verify electrical connections without independent analysis, current manufacturer documentation, and appropriate testing. See [Model limitations and disclaimer](#model-limitations-and-disclaimer) and [Detailed model and validation notes](MODEL_NOTES.md).

## Explore the simulators

Each simulator is a **standalone HTML file**. Download and open it locally, or enable GitHub Pages to run the suite in a browser. The links below point to the files in this repository.

### Electric motor design and dynamics

| [**Brushed DC Motor**](motor.html) | [**Coreless DC Motor**](coreless.html) | [**Brushless DC Motor**](brushless.html) |
|:--:|:--:|:--:|
| [![Brushed DC motor cross-section and design controls](assets/motor.png)](motor.html) | [![Coreless DC motor geometry and design controls](assets/coreless.png)](coreless.html) | [![Brushless motor winding and rotor visualization](assets/brushless.png)](brushless.html) |
| Winding turns, wire diameter, geometry, magnet selection, load, gearing, torque-speed curves, transient response, and sensitivity. | Ironless winding geometry, rotating copper shell, magnet dimensions, torque and inertia, dynamic response, and thermal trends. | Slotless brushless topology, pole count, stationary phase winding, yoke flux, theoretical iron loss, and commutation visualization. |

### Digital communication and timing

| [**I²C Bus Inspector**](i2c.html) | [**SPI Bus Inspector**](spi.html) | [**UART / Serial Inspector**](uart.html) |
|:--:|:--:|:--:|
| [![I2C bus, controllers, pull-ups, and data lines](assets/i2c.png)](i2c.html) | [![SPI controller, peripherals, and chip-select lines](assets/spi.png)](spi.html) | [![UART transmitter waveform and receiver sampling points](assets/uart.png)](uart.html) |
| Open-drain SDA/SCL, pull-up resistance, clock edges, address selection, ACK/NACK, and register transactions. | SCK, COPI/CIPO (MOSI/MISO), active-low chip select, full-duplex shifting, timing modes, and selected-peripheral behavior. | 8N1 framing, least-significant-bit-first transmission, adjustable transmitter/receiver baud rates, sampling, decoding, and framing errors. |

## Getting started

### Option A: Open locally

1. Download the repository as a ZIP or clone it.
2. Open **`index.html`** in a modern desktop browser, or open any simulator HTML file individually.
3. Use the controls, inspect components and calculated values, and step through the scenarios.

**No installation, build process, MATLAB/Python runtime, or JavaScript framework is required.** The simulation logic runs in the browser. Some pages request optional web fonts; the functional simulations do not depend on those fonts.

### Option B: Publish with GitHub Pages

1. Upload `index.html`, the six simulator `.html` files, `README.md`, and the entire `assets/` directory to the repository root.
2. Open repository **Settings → Pages**.
3. Under **Build and deployment**, select **Deploy from a branch**, choose `main` and `/ (root)`, then save.
4. Once GitHub Pages deploys, use its published site URL to open `index.html` and link to individual simulators.

GitHub's normal source-code preview does **not** run HTML simulations. Use GitHub Pages or download/open the files to interact with them.

### Recommended repository layout

```text
.
├── README.md
├── index.html
├── motor.html
├── coreless.html
├── brushless.html
├── i2c.html
├── spi.html
├── uart.html
└── assets/
    ├── overview.png
    ├── motor.png
    ├── coreless.png
    ├── brushless.png
    ├── i2c.png
    ├── spi.png
    └── uart.png
```

The `assets/` directory contains documentation screenshots, not simulator dependencies. Keep the relative paths intact so the images render in the README.

## Learning objectives

The motor simulators are designed to help students connect electromagnetic and mechanical design choices to behavior:

- Relate winding, magnetic flux, and geometry to motor constants, resistance, speed, torque, and power.
- Separate steady-state operating points from transient response and approximate thermal behavior.
- Compare conventional brushed, ironless coreless, and brushless motor constructions while identifying the assumptions behind the comparison.
- Explore parameter sensitivities and understand why a theoretical maximum is not necessarily a continuous operating rating.

The bus simulators focus on what is happening at the signal and protocol levels:

- Track the sequence of a transaction and which device is driving each line.
- Contrast I²C open-drain signaling with SPI's driven signals and explicit peripheral selection.
- Understand how baud-rate mismatch shifts UART sampling instants without changing the transmitted data bits.
- Connect the waveform to register transactions, received bytes, and possible communication errors.

## Example hardware in the protocol diagrams

The I²C and SPI examples use a **generic teaching bench** with two Arduino UNO R4 Minima boards and an **Adafruit LSM6DS3TR-C breakout**. The breakout's onboard level shifting supports 5 V controller logic; **the bare LSM6DS3TR-C IC is not itself a 5 V logic device**. See the [Adafruit breakout guide](https://learn.adafruit.com/adafruit-lsm6ds3tr-c-6-dof-accel-gyro-imu/pinouts) and the relevant device datasheets before constructing actual circuitry.

The UART example models an idealized asynchronous serial link, not a complete physical-layer noise or clock-recovery system.

## Interpretation guide

| What you see | Appropriate interpretation | Do **not** infer |
|---|---|---|
| Motor speed/torque/power and efficiency | Values of a simplified mathematical model under the chosen parameters | Manufacturer specifications, validated efficiency maps, or continuous ratings |
| Motor temperatures or stall threshold | Outcomes of an approximate two-node thermal calculation | Safe stall time, winding insulation rating, or cooling design approval |
| Dimensioned motor drawings | Schematic drawings with selected dimensions scaled | Manufacturing geometry, tolerances, leakage flux, or complete magnetic construction |
| Coreless/brushless preset names | Illustrative sizes/architectures | Official maxon/FAULHABER simulations or numerical agreement with any product |
| Brushless commutation selector | Visualization of different current/field presentations | Separately solved PWM inverter, three-phase torque ripple, or switching losses |
| I²C/SPI voltage traces | First-order electrical teaching approximation | Passing an actual electrical specification, signal integrity, or 5 V compatibility of arbitrary parts |
| UART receiver result | An ideal fixed-center sampling exercise | Behavior of a particular UART peripheral or a reliable transmission error detector |

**Verification is not validation.** The web pages have been exercised in a browser, and selected equations and transactions were checked, but no systematic benchmark against measured motors or physical bus captures is provided. See [MODEL_NOTES.md](MODEL_NOTES.md) for equations, omissions, illustrative parameters, and a release checklist.

## Model limitations and disclaimer

**FOR EDUCATIONAL AND DEMONSTRATION PURPOSES ONLY.**

These simulations intentionally simplify real electromechanical and digital systems. In particular:

- **Motors:** Geometries, magnetic circuits, winding fill, friction, iron losses, commutation, gearbox behavior, thermal networks, and material properties are simplified. Calculated power, temperature, speed, torque, and any stall-time estimate are theoretical outputs, not rated or validated hardware specifications. Open-loop voltage/current drive and regenerative operation assume idealized electrical behavior. The brushless six-step versus sinusoidal selection affects the illustration, not a separately solved inverter/phase-current model. High-flux or saturated states can fall outside model validity.
- **I²C and SPI:** Signal integrity, rise times, output impedance, clocking, board interconnects, and transaction timing use instructional approximations. Register data values are examples; presented code is conceptual and has not been verified as a standalone hardware sketch. The illustrated bus connections are not substitutes for a wiring diagram, checked pin assignments, or a verified voltage-compatibility analysis. The breakout-level-shifter statement applies to the **Adafruit breakout**, not the bare LSM6DS3TR-C chip.
- **UART:** Receiver sampling illustrates baud mismatch under ideal assumptions (8N1, single start edge, center sampling). Real UARTs commonly employ implementation-dependent oversampling, synchronization and error handling. This page is not a serial transceiver model; a passing stop-bit check does not guarantee correct data.

**No quantitative motor-accuracy claim, hardware-compliance claim, or fitness-for-purpose claim is made.** Before applying any result to real hardware, verify it against primary datasheets, engineering calculations, relevant standards, and physical measurements. The author and university are not providing certification, design approval, or an assurance of safe operation.

## Recommended classroom use

1. **Predict first.** Ask students to record a qualitative or quantitative prediction before moving a slider.
2. **Inspect assumptions.** Have students locate a neglected effect (for example, motor saturation, winding temperature feedback, or UART oversampling) and state how it might change the result.
3. **Calculate independently.** Reproduce at least one equation or timing relationship without relying on the displayed result.
4. **Measure where feasible.** Compare modeled DC motor startup or bus traces with Arduino/oscilloscope observations; report discrepancies rather than forcing agreement.

## Primary references and further reading

- [Adafruit LSM6DS3TR-C breakout pinouts](https://learn.adafruit.com/adafruit-lsm6ds3tr-c-6-dof-accel-gyro-imu/pinouts), including I²C address options, 10 kΩ board pull-ups, and 3–5 V logic-level compatibility of the **breakout**.
- [ST LSM6DS3TR-C datasheet](https://cdn-shop.adafruit.com/product-files/4503/4503_LSM6DS3TR-C_datasheet.pdf), for the bare device register map and electrical limits.
- [NXP UM10204 I²C-bus specification](https://www.nxp.com/docs/en/user-guide/UM10204.pdf), for protocol definitions and standardized timing/electrical requirements.
- [MODEL_NOTES.md](MODEL_NOTES.md), for this software's equations, simplifications, and current validation status.

These are references, not an assertion that every scenario has been checked for compliance with their specifications.

## Authorship, AI assistance, and citation

**Author and course context:** Frank C. Sup IV, Professor, Department of Mechanical and Industrial Engineering, University of Massachusetts Amherst. Developed for MIE 443 Mechatronics.

**AI use disclosure:** Simulation code and explanatory text were developed with assistance from Claude (Anthropic) and subsequently revised with assistance from ChatGPT (OpenAI), under the author's direction. The author is responsible for reviewing, adapting, and maintaining the educational content.

Suggested citation:

> Sup, F. C., IV. (2026). *MIE 443 interactive simulators* [Interactive teaching software]. University of Massachusetts Amherst. Add the repository URL or published site URL when available.

**Licensing:** No software license is included with these files. Consider adding a `LICENSE` file if reuse and redistribution should be permitted; a public repository does not itself grant an open-source license. Brand and product names in the illustrations identify example architectures/components and imply **no manufacturer affiliation, endorsement, or performance equivalence**.

---

*October 2026. Screenshots show simulator-generated interface views, not measurements. Model/documentation labels may differ slightly from an earlier screenshot.*
