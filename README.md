# OPEN-ENV: OpenFlexure Operating Envelope Engineering and Validation

*Precision Characterization, Fabrication, and Environmental Compensation*

OPEN-ENV investigates how reliably an OpenFlexure microscope performs as environmental conditions change, and whether targeted hardware modifications and empirical compensation can extend its useful operating range. The project combines precision metrology, mechanical fabrication, sensor integration, and reproducible experimental analysis on a motorized three-axis microscope.

Developed as a Robotics MSE research project at the Integrated Imaging Center, this repository is intended to hold the engineering record: code, CAD, raw data, calibration protocols, design decisions, and operating documentation.

**Project status:** This README describes the scope and planned deliverables established in the course agreement. It does not assert that experiments, modifications, or performance targets have been completed. The selected endpoint, implementation details, and measured results are to be recorded as the work progresses.

## Project objective

Measure the stock microscope's performance, identify its dominant limitations, and design and validate at least one Z-axis mechanical or sensing intervention. Integrate temperature monitoring and a correction model, then evaluate the complete instrument through automated imaging.

The central question is: **Over what range of temperature and vibration does the microscope continue to meet its performance targets, and how do the interventions change that range?**

Success is demonstrated through comparable before-and-after measurements, stated uncertainty, and a reproducible archive, including an honest account of improvements, failures, and remaining limitations.

## The operating-envelope concept

The operating envelope is the range of tested conditions in which the microscope meets a defined performance budget. That budget includes position return error, focus error relative to the objective's depth of field, and successful automated scanning. Each acceptance threshold must be justified by the imaging task and optics in the relevant deliverable.

Temperature, temperature rate of change, and vibration are the environmental stress axes. Where the selected endpoint and equipment permit, stress is increased until a performance threshold is crossed. Comparing the stock and modified instruments shows whether an intervention moves that boundary. If a boundary is not reached, results should state the tested range rather than imply an unmeasured limit.

Published climate ranges and OpenFlexure field reports provide context for interpreting the measured envelope; they are not substitute design targets. Dust, humidity, and unreliable power are outside the agreement's experimental envelope. Results apply to the tested instrument and conditions and do not establish universal field readiness.

## Engineering phases and deliverables

### ID-1 — Baseline characterization

Characterize the stock X, Y, and Z motion system. Measure XY return-to-position repeatability and direction-dependent backlash; compare image-sharpness measures for Z-axis focusing; and calibrate the relationships among motor steps, physical displacement, and image pixels.

The Minimum endpoint includes 30 randomized target positions at one site and two sharpness measures, including Laplacian variance, at three sites across two slides. Expanded endpoints add sites, cross-axis checks, additional sharpness measures, between-day checks, and independent Z-position validation. The Maximum endpoint includes a complete image-based breakdown of position scatter into backlash, drift, and vibration using frame-to-frame cross-correlation.

**Outputs:** Baseline technical report, performance comparison table, raw CSV data, analysis code, and coordinate-conversion calibration records.

### ID-2 — Focused Z-axis intervention

Use ID-1 evidence to select and fabricate a mechanical intervention, a position-sensing intervention, or a combination. Candidate approaches include anti-backlash preload, a counterbalance, and an encoder for independent Z-position measurement.

Repeat the baseline Z-axis protocol on the modified instrument using matching sites and methods. Where multiple modifications are combined, the Target and Maximum endpoints add ablation tests to isolate their contributions. Changes that alter mass or stiffness also call for a before-and-after vibration comparison. The Maximum endpoint combines mechanical and sensor interventions and adds accelerometer-based resonance and settling-time measurements.

**Outputs:** Design report, editable CAD and STL files, bill of materials, assembly instructions, applicable wiring diagrams and sensor code, and paired before-and-after data.

### ID-3 — Thermal monitoring, compensation, and integration

Fabricate temperature-sensor mounts, calibrate the sensors, and log temperature alongside stage drift. Fit an empirical correction model and compare residual drift with and without correction. Document objective exchange and demonstrate an end-to-end automated scan.

The Minimum endpoint uses two temperature sensors, one 60-minute monitoring session, an offline correction model, and one full scan. Target adds a third sensor, multiple conditions and scans, a multivariable model, and objective-swap validation over at least five cycles. Maximum adds a controlled heater test point, live compensation, and an independent-user handoff test.

**Outputs:** Thermal characterization report, sensor-mount CAD and STL files, synchronized temperature/drift CSV data, compensation code, objective-swap procedure, and operating notes.

### Final report — Integrated engineering evidence

Combine the baseline findings, intervention rationale, validation results, and environmental limits into one account of the stock and modified operating envelopes. Include the final operating manual and an archive sufficient to reproduce the analysis and rebuild the modifications.

The agreement provides three cumulative endpoints: **Minimum**, **Target**, and **Maximum**. The final report is required at every endpoint. **Selected endpoint: TBD with the advisors.** Planned submission milestones are the ends of Weeks 5, 9, 11, and 12 for ID-1, ID-2, ID-3, and the final report, respectively; these are course milestones, not completion claims.

## Key performance measures

Numerical acceptance limits are **TBD**: the agreement requires justified targets but does not provide a finalized numerical performance budget. Experimental settings, such as sample counts and monitoring duration, are not acceptance thresholds.

| Measure | Evidence to record |
| --- | --- |
| XY repeatability and accuracy | Return-position scatter and error against a calibrated spatial reference; direction of approach and repeated-run variability |
| Backlash and cross-axis effects | Direction-dependent displacement error and any coupling between axes |
| Z-axis focus performance | Focus convergence error, repeatability, capture range, and sharpness-metric comparison; independent Z measurement at Maximum |
| Coordinate calibration | Motor-step-to-distance and distance-to-pixel conversion factors, coordinate conventions, and calibration uncertainty |
| Vibration | Image-derived position jitter; resonance and settling-time measurements where accelerometer instrumentation is included |
| Thermal drift and compensation | Displacement versus temperature and time, uncompensated drift, and residual error after correction |
| System integration | Automated-scan completion and failures; objective-swap repeatability and handoff outcomes where included |
| Envelope boundary | Tested stress conditions at which a justified target is crossed, or the tested range when no crossing is observed |

Keep accuracy, precision, repeatability, and resolution distinct. Report units, trial counts, test conditions, and appropriate uncertainty measures alongside results. Use randomized order and repeated trials where specified, and preserve comparable procedures for stock-versus-modified tests.

## Repository structure

The following is the planned organization, consistent with the agreement. Directories and files are populated as the corresponding work is completed.

```text
OPEN-ENV/
├── README.md
├── code/
│   ├── acquisition/          # Microscope control and synchronized logging
│   ├── analysis/             # Repeatability, autofocus, vibration, and plots
│   ├── compensation/         # Thermal model fitting and correction
│   └── firmware/             # Microcontroller and sensor code, if used
├── CAD/
│   ├── source/               # Editable designs for interventions and mounts
│   └── STL/                  # Printable exports
├── data/
│   ├── raw/                  # Original measurements and acquisition metadata
│   ├── processed/            # Derived tables and analysis-ready data
│   └── results/              # Figures and performance comparisons
├── calibration_protocols/
│   ├── procedures/           # Calibration and repeatable test methods
│   └── records/              # Conversion factors, sensor checks, uncertainty
└── documentation/
    ├── reports/              # ID-1, ID-2, ID-3, and final report
    ├── hardware/             # BOM, assembly instructions, wiring diagrams
    ├── operating_manual/     # Setup, objective swap, maintenance, recovery
    └── references/           # Bibliography and source/version records
```

## Hardware and software

The agreement identifies the following equipment and options. Example components are candidates, not a finalized bill of materials.

| Area | Planned equipment or dependency | Details to confirm |
| --- | --- | --- |
| Microscope | Motorized OpenFlexure with Raspberry Pi controller and camera | Build revision, controller, camera, objectives, and installed software versions: TBD |
| Calibration and samples | USAF 1951 target, stage micrometer or calibrated fiducial grid, non-clinical teaching slides, blank slides and coverslips | Models, calibration specifications, and sample identifiers: TBD |
| Z-axis intervention | Springs, brackets, fasteners, counterbalance and/or magnetic linear encoder; AS5311 is an example | Selected intervention, dimensions, sensor, and interface: TBD after ID-1 |
| Sensor interface | Arduino or equivalent, with controller communication | Board, firmware dependencies, wiring, and protocol: TBD |
| Thermal monitoring | Two or three sensors; DS18B20 or thermistors are options | Sensor choice, calibration, placement, and sampling interval: TBD |
| Maximum-endpoint additions | MEMS accelerometer and controlled heater | Accelerometer model, heater design, and control implementation: TBD |
| Fabrication | 3D printing using PLA/PETG or a print service | Material, printer, print settings, and tolerances: TBD |
| Analysis and control | Python, analysis notebooks, and microcontroller code as needed | Runtime versions, libraries, installation steps, and entry points: TBD |
| CAD | Fusion 360, Onshape, FreeCAD, or OpenSCAD are listed options | Selected tool, version, and editable source format: TBD |

## Setup and reproducibility

Installation and execution commands will be added once the hardware and software stack is confirmed. For each released experiment or analysis:

1. Record the instrument configuration, intervention revision, software versions, and selected endpoint.
2. Follow the applicable calibration procedure and save its conversion factors, units, date, and uncertainty.
3. Preserve raw data with sample/site identifiers, timestamps, environmental conditions, approach direction, and trial counts.
4. Document the exact commands, inputs, parameters, and dependencies needed to regenerate each result from raw data.
5. Compare stock and modified results using matched procedures and report uncertainty, failures, and tested limits.

The completed archive should include editable CAD, printable exports, a parts list, wiring details where applicable, calibration procedures, and an operating manual covering maintenance, known limitations, and recovery. The agreement calls for a `v1.0` repository tag at the final archive milestone; its creation is pending project completion.

## Contributors and roles

| Contributor | Role in the course agreement |
| --- | --- |
| Ogedi Asimama-Duruaku | Robotics MSE student; project engineering, experiments, analysis, and authored course deliverables |
| Dr. Samson Jarso | Research advisor |
| Dr. Peter Kazanzides | Academic advisor |
| Dr. Ian Dobbie | Additional personnel; specific responsibilities not stated |

Work is planned at the Integrated Imaging Center alongside Dr. Jarso. The course agreement permits AI assistance with research, code, CAD, analysis, and experimental planning; the interim deliverable reports and final report are to be written by Ogedi.

## License

**TBD — project license(s) have not been specified in the course agreement.** Add the selected license text and clarify its coverage of original code, hardware designs, documentation, and data before a licensed release. Record the applicable upstream licenses and attribution for incorporated third-party materials.

## Citation and acknowledgments

Formal citation metadata and any archival DOI are **TBD**. Once a release is available, add a `CITATION.cff` containing confirmed authors, release version, date, repository URL, and DOI if assigned.

Suggested citation fields to complete:

```text
[Confirmed authors]. [Year].
OPEN-ENV: OpenFlexure Operating Envelope Engineering and Validation.
Version [release]. [Repository or archival URL]. [DOI, if assigned].
```

OPEN-ENV builds on the OpenFlexure microscope platform. Record the specific upstream hardware and software versions and their recommended citations in `documentation/references/`.

**Scope source:** Robotics MSE Research Course Agreement for Ogedi Asimama-Duruaku, revised May 23 and edited May 28, 2026, version V7. The project identity used here is the finalized OPEN-ENV name; the technical scope follows that agreement.
