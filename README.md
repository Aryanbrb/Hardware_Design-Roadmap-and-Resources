# Hardware Design Roadmap and Resources

A practical learning path from circuit fundamentals to designing, assembling, testing, and documenting electronic circuit boards.

This guide grew out of my experience learning hardware design independently. It aims to make useful resources easier to find and connect learning to work you can demonstrate. It is a suggested path, not a universal syllabus or a guarantee of job readiness.

**Scope:** circuit design, component selection, PCB layout, assembly, board bring-up, validation, and manufacturing handoff. Analog and digital circuits are both part of board-level hardware design. IC design is outside this guide's scope.

Related paths: [ASIC design](https://github.com/abdelazeem201/ASIC-Design-Roadmap) · [Embedded engineering](https://github.com/m3y54m/Embedded-Engineering-Roadmap)

## How to use this guide

- Start with the earliest stage whose milestone you cannot yet demonstrate.
- Learn theory alongside simulation, building, and measurement. You do not need to finish an entire mathematics or electromagnetics course before making a first board.
- Choose one PCB tool and one circuit simulator. KiCad with ngspice or LTspice is a practical starting combination.
- Write down requirements and test results. A working demonstration is useful; evidence explaining its behavior is better.
- Revisit earlier stages as projects become more demanding. The stages overlap.

**Resource labels:** **Core** = suggested starting material; **Reference** = consult for a particular design; **Optional** = additional depth or an alternative. Select relevant chapters and modules rather than completing every resource.

## Roadmap

![Six-stage board-level hardware design roadmap with milestones and a recurring engineering workflow](roadmap.svg)

**[Download the editable Excalidraw roadmap](roadmap.excalidraw)** · [Open SVG preview](roadmap.svg)

To edit the diagram, download `roadmap.excalidraw`, open [Excalidraw](https://excalidraw.com), and choose **Open** or drag the file onto the canvas. Shapes, text, and arrows are editable. The text below provides an accessible version of the roadmap.

| Stage | Focus | Milestone |
|---|---|---|
| 1. Foundations and measurement | Circuit analysis, components, instrument use | Predict, simulate, and measure a small circuit. |
| 2. First complete PCB | Schematic, libraries, layout, manufacturing rules | Assemble and test a simple sensor or interface board. |
| 3. Custom MCU board | Power, reset, clocks, boot, debug, interfaces | Bring up the board and verify every intended interface. |
| 4. Analog and power | Signal conditioning, conversion, regulation, protection | Measure performance against written requirements. |
| 5. Product engineering | Reviews, sourcing, DFM/DFA/DFT, validation, release | Deliver a reviewed release package and a documented revision. |
| 6. Specialization | Choose a role and a technical direction | Complete a deeper project with justified constraints and measured results. |

### 1. Foundations and measurement

**Learn**

- Units, algebra, graphs, complex impedance, and basic statistics. Introduce calculus through circuit behavior as needed.
- Ohm's and Kirchhoff's laws, Thevenin/Norton equivalents, RC/RL/RLC behavior, time constants, and frequency response.
- Resistors, capacitors, inductors, diodes, transistor switches, and introductory op-amp circuits.
- Logic levels, pull-ups/pull-downs, loading, and basic timing.
- Multimeters, current-limited bench supplies, oscilloscopes, probe loading, bandwidth, and grounding.

**Build:** an RC filter and a transistor-controlled load. Calculate expected behavior, simulate it, and measure it. Explain differences caused by tolerances, loading, and nonideal components.

**Resources**

- **Core:** [Analog Devices StudentZone activities](https://ez.analog.com/adiacademy/university-program/a/studentzone-articles) — select circuit theory, transistor, filter, and measurement exercises.
- **Core:** [Tektronix: ABCs of Probes](https://www.tek.com/en/documents/whitepaper/abcs-probes-primer) — understand how the probe changes the measurement.
- **Optional:** [Khan Academy electrical engineering playlist](https://youtube.com/playlist?list=PLSQl0a2vh4HCLqA-rhMi_Z_WnBkD3wUka) — foundational review from the original resource collection.

Start with low-voltage, current-limited projects. Learn instrument grounding and ratings before probing unfamiliar circuits; mains and high-energy systems need additional training.

### 2. First complete PCB

**Learn**

- Translate a short specification into a block diagram and schematic.
- Read recommended operating conditions, absolute maximum ratings, package drawings, and application circuits.
- Select exact parts; check ratings, tolerances, availability, and footprints.
- Create and verify symbols and footprints, including pin mapping and package orientation.
- Place connectors, mounting holes, decoupling, and functional blocks before routing.
- Introduce return-current paths, ground planes, stackup choices, trace/via constraints, and thermal paths now.
- Use electrical-rule checks (ERC) and design-rule checks (DRC); review and justify exceptions.
- Check fabrication and assembly capabilities before finalizing the layout.

**Build:** a small sensor/interface board. Review it, order it, assemble it, and compare measured behavior with the specification.

**Resources**

- **Core:** [KiCad documentation](https://docs.kicad.org/) — use documentation matching your installed version.
- **Core:** [Eurocircuits technical guidelines](https://www.eurocircuits.com/technical-guidelines/) — learn fabrication and assembly constraints, then check your chosen supplier's rules.
- **Reference:** [ADI grounding and decoupling tutorial](https://ez.analog.com/adiacademy/university-program/a/studentzone-articles/c/grounding-decoupling/SA1023/grounding-and-decoupling-learn-basics-now-and-save-yourself-much-grief-later-part-3-decoupling-continued) — connect capacitor placement to circuit behavior.

### 3. Custom microcontroller board

**Learn**

- Power budgets, regulators, decoupling, startup, and power sequencing.
- Reset circuits, clock sources, boot configuration, programming, and debug access.
- GPIO voltage compatibility and the electrical behavior of UART, I2C, and SPI.
- Connector pinouts, protection, test points, and basic interface timing.
- Enough firmware to exercise each peripheral and distinguish firmware issues from hardware faults.
- Basic architecture and memory organization as needed; deep CPU design is optional for this path.

**Build:** an MCU board with a sensor, debug connector, and external interface. Before power-up, inspect assembly and check for shorts. Then verify current consumption, rails, reset, clocks, programming, and interfaces in a documented order.

**Resources**

- **Core:** [Hardware design with RP2040](https://datasheets.raspberrypi.com/rp2040/hardware-design-with-rp2040.pdf) — a worked manufacturer guide for a custom MCU board.
- **Reference:** the selected MCU's datasheet, reference manual, errata, hardware design guide, and evaluation-board files — explain any departure from the reference design.
- **Optional:** [Embedded engineering roadmap](https://github.com/m3y54m/Embedded-Engineering-Roadmap) — expand firmware and debugging skills as needed.

### 4. Analog and power design

**Learn**

- Op-amps, comparators, feedback, stability, filtering, noise, and sensor conditioning.
- ADC input drive, references, sampling behavior, and error budgets.
- MOSFET switching and practical input/output protection.
- LDOs and buck converters: losses, startup, load transients, stability, and thermal estimates.
- Component tolerances and derating; distinguish typical performance from guaranteed limits.
- DC, AC, transient, and parameter-sweep simulation. Understand what a model does not represent.

**Build:** choose a sensor acquisition board or a low-voltage buck-converter board. Define numeric targets before selecting parts. Measure accuracy/noise or regulation/efficiency/transient behavior over a stated operating range.

**Resources**

- **Core:** [TI Precision Labs](https://www.ti.com/video/series/precision-labs.html) — choose amplifier and data-converter modules relevant to your circuit.
- **Core:** [TI: PCB layout guidelines to optimize power supply performance](https://www.ti.com/video/6245175641001) — study switching loops, parasitics, grounding, EMI, and thermal behavior.
- **Reference:** [LTspice](https://www.analog.com/en/resources/design-tools-and-calculators/ltspice-simulator.html) — an alternative to ngspice for analog and power simulation.
- **Reference:** the chosen regulator's datasheet and evaluation-board layout — component selection and layout requirements are device-specific.

### 5. Product engineering and manufacturing handoff

Introduce these habits with the first board; deepen them here.

**Learn**

- Requirements traceability, schematic/layout reviews, and version control.
- Design for manufacture (DFM), assembly (DFA), and test (DFT).
- BOM lifecycle, lead times, approved alternatives, cost, and substitution risks.
- Mechanical fit, connector access, mounting, enclosure constraints, and thermal behavior.
- A test plan covering operating limits and relevant fault cases; record setup, instruments, firmware, and board revision.
- EMC awareness and pre-compliance work. Identify product- and market-specific requirements early.
- Test-point access, programming fixtures, production tests, and failure diagnosis.
- Engineering change records, release approval, and reproducible manufacturing outputs.

**Deliver:** a reviewed release package, measured validation report, issue log, and a revision addressing observed problems.

**Resources**

- **Core:** [Eurocircuits PCB assembly guidelines](https://www.eurocircuits.com/technical-guidelines/pcb-assembly-guidelines/) — assembly constraints and error prevention.
- **Reference:** [IPC DFM guidance](https://www.ipc.org/design-manufacturing-confirmed-ipc-standards) and [standards overview](https://www.ipc.org/meet-your-standards) — understand which documents apply.

Standards have different purposes: the IPC-2220 family addresses board design, IPC-6012 addresses rigid-board qualification/performance, IPC-A-600 addresses bare-board acceptability, and IPC-A-610 addresses electronic-assembly acceptability. J-STD-001 addresses soldered-assembly requirements. Confirm the applicable revision, class, customer requirements, and supplier agreement; this guide does not establish compliance. Many full standards require purchase or institutional access.

### 6. Choose a specialization

| Direction | Deeper topics | Example evidence |
|---|---|---|
| High-speed digital | Transmission lines, termination, timing budgets, differential signaling, impedance, SI/PI | Document constraints and validate an interface using appropriate measurements. |
| Precision analog | Noise/error budgets, references, leakage, grounding, calibration | Characterize accuracy, repeatability, and drift. |
| Power electronics | Control loops, magnetics, switching losses, thermal design, EMI | Measure efficiency, transient response, and temperature over operating conditions. |
| RF | Matching, transmission lines, antennas, RF layout, network measurements | Measure and explain relevant RF performance. |
| Advanced PCB layout | Constraint management, stackups, HDI, library quality, manufacturing handoff | Deliver a reviewed layout and documented fabrication/assembly package. |

**Resource:** [FEDEVEL](https://www.fedevel.com/) offers optional guided courses. Check each course's prerequisites, tool requirements, and price before enrolling.

For high-speed work, compare signal edge rate with interconnect propagation delay; clock frequency alone does not determine whether transmission-line effects matter. Derive length and skew constraints from interface requirements instead of matching every trace by habit.

A hardware design engineer path emphasizes architecture, circuits, and validation. A PCB layout designer path emphasizes placement, routing, constraints, libraries, and manufacturing handoff. Both benefit from understanding the complete workflow.

## The workflow to repeat on every project

**Requirements → calculations and simulation → schematic review → layout review → fabrication and assembly → bring-up → validation → revision and release**

Testing should feed back into requirements and design. Plan measurement access and acceptance criteria before ordering a board.

### Suggested portfolio projects

| Project | Set targets for | Evidence to publish |
|---|---|---|
| Sensor interface | Input range, accuracy, noise, supply range, disconnected-sensor behavior | Error budget, measured results, test setup, and limitations. |
| Custom MCU board | Supply current, peripheral operation, startup, programming/debug | Power tree, bring-up log, firmware version, and interface tests. |
| Low-voltage buck converter | Input/output range, load, ripple, efficiency, temperature | Load sweeps, transient captures, probing method, and thermal results. |

Choose numeric limits appropriate to the selected components and instruments. A tutorial reproduction is a good exercise; a portfolio project should also explain your own requirements, decisions, changes, and measurements.

### Release package checklist

- [ ] Requirements and block diagram.
- [ ] Editable schematic/PCB sources and required libraries.
- [ ] Design calculations, simulations, and review notes.
- [ ] BOM with manufacturer part numbers, quantities, and reviewed alternatives.
- [ ] Supplier-compatible fabrication/drill data and stackup information.
- [ ] Assembly drawings, placement data, and programming instructions.
- [ ] Test plan, instrument/setup details, and results against acceptance criteria.
- [ ] Firmware/test-script version and board revision.
- [ ] Known issues, change history, and release identifier.

ERC/DRC results are useful checks, not proof that the circuit functions or meets its requirements.

## Tools: choose a small starting set

| Task | Suggested starting point | When to expand |
|---|---|---|
| Schematic and PCB | KiCad | Learn a commercial tool when a team, role, or project requires it. |
| Circuit simulation | ngspice or LTspice | Add specialized SI/PI, RF, or thermal analysis when justified. |
| Embedded exercises | A development board and simple test firmware | Use Wokwi/Tinkercad as optional learning aids; verify physical behavior on hardware. |
| Measurement | DMM, current-limited supply, suitable oscilloscope access | Add logic analyzer, electronic load, or other instruments to suit the test plan. |
| Documentation | Git, Markdown, and a calculation worksheet | Automate repetitive tests and reports as the project grows. |

Do not treat tool proficiency as a substitute for design reasoning.

## Original resources

The initial collection of videos and the original diagram are preserved in [the original resource archive](resources/original-roadmap.md). They remain available as supplementary material; the stages above provide the recommended structure. Legacy videos have not all been re-audited for current tool versions or coverage.

## Contributing and maintenance

Please suggest resources with a title, author/provider, direct link, intended stage, prerequisites, cost/access requirements, and a short explanation of the learning outcome. Prefer original documentation and resources that include exercises, calculations, or measurements. Report broken links and distinguish tool-version changes from changes in engineering principles.

**Roadmap revision:** 20 October 2026. Resource availability and tool versions can change. This is a living guide; completing it is a foundation for further practice, review, and specialization.
