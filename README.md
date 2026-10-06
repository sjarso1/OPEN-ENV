[README.md](https://github.com/user-attachments/files/29226004/README.md)
# OPEN-ENV: OpenFlexure Operating Envelope Engineering and Validation
Precision Characterization, Fabrication, and Environmental Compensation
**Robotics Engineering for a Field-Deployable Open-Source Microscope: Precision Diagnostics and Mechanical Fabrication on the OpenFlexure Platform**

A robotics-engineering research project that measures the *operating envelope* of a low-cost, 3D-printed open-source microscope — the range of temperature and vibration over which it still meets its performance targets — and builds and tests targeted fabrication that pushes that boundary outward.

> Because the field conditions are not known, this project measures the operating envelope of the OpenFlexure microscope — the range of temperature and vibration over which it still meets its targets — and shows how targeted fabrication widens that envelope.

---

## Project website

This repository includes a single-page project site (`docs/index.html`) built to be served by **GitHub Pages**.

**To publish it:**

1. Place `index.html` in the `docs/` folder and commit it (along with `.nojekyll`).
2. Push to GitHub.
3. Go to **Settings → Pages → Build and deployment**.
4. Set **Source** to *Deploy from a branch*, choose your branch (e.g. `main`) and the **`/docs`** folder, then **Save**.
5. The site publishes at `https://<username>.github.io/<repo>/` within a minute or two.

> The filename must stay `index.html` — that is what Pages serves as the landing page. The `.nojekyll` file tells Pages to skip Jekyll processing so nothing is filtered out unexpectedly.

To preview locally, just open `docs/index.html` in a browser, or run a static server from the repo root:

```bash
python3 -m http.server --directory docs 8000
# then visit http://localhost:8000
```

---

## The engineering loop

Three interim deliverables follow one loop — diagnose, fix, then make it hold up — and a final report ties them into a single engineering story.

| Deliverable | Focus | Due | Weight |
| --- | --- | --- | --- |
| **ID-1** | Baseline performance of the stock microscope (repeatability, backlash, focus accuracy, coordinate mapping) | End of Wk 5 | 10% |
| **ID-2** | Focused fabrication intervention on the Z-axis (mechanical fix, sensor, or both) with before/after results | End of Wk 9 | 10% |
| **ID-3** | Thermal monitoring, empirical compensation, and full-system integration | End of Wk 11 | 10% |
| **Final report** | Synthesis of ID-1 → ID-2 → ID-3 into one engineering narrative + operating manual | End of Wk 12 | 70% |

Each interim deliverable is judged on the same six-part rubric: engineering rationale, technical execution, quantitative analysis, evidence-based outcomes, documentation & reproducibility, and integration & engineering judgment.

## Project endpoints

The project has three acceptable finish lines. Target includes everything in Minimum and adds to it; Maximum includes everything in Target and adds more. The final report is required at all three.

- **Minimum** — diagnose and fix once: 30-position repeatability, one Z-axis fix, two temperature sensors with a post-hoc correction and one full scan.
- **Target** — add rigour and ablation: multi-site repeatability, statistical tests with error bars, third sensor, multi-input model, objective-swap checks.
- **Maximum** — independent and live: an independent Z measurement, combined mechanical + sensor fix, accelerometer vibration readout, a heater-driven test point, live in-scan compensation, and an independent-user handoff test.

---

## Suggested repository structure

```
.
├── docs/
│   ├── index.html        # project website (served by GitHub Pages)
│   └── .nojekyll
├── code/                 # stage control, analysis, microcontroller code
├── cad/                  # editable CAD sources + exported STL
├── data/                 # raw measurement data (CSV)
├── calibration/          # calibration protocols and records
├── reports/              # ID-1, ID-2, ID-3, and the final report (PDF)
└── README.md
```

> Tag the repository `v1.0` at the end of the project once the complete archive — data, code, CAD, BOM, calibration steps, and operating manual — is committed.

## Materials

Roughly **$590** in parts (estimates only; excludes shipping, taxes, and fees). Key items: the OpenFlexure motorised kit ($250), calibration targets and slides, a magnetic linear encoder and Arduino for the ID-2 sensor path, DS18B20 temperature sensors for ID-3, an optional MEMS accelerometer for the ID-2 Maximum endpoint, plus springs, fasteners, and 3D-printer filament. See the website's *Materials* section for the full bill of materials.

---

## Built on the OpenFlexure platform

- **Microscope handbook (v7):** https://openflexure.gitlab.io/microscope-handbook/
- **Documentation:** https://openflexure.org/projects/microscope/documentation
- **Community forum:** https://openflexure.discourse.group/
- **GitLab repository:** https://gitlab.com/openflexure
- **Build instructions:** https://openflexure.org/projects/microscope/build

## Project details

- **Student:** Ogedi Asimama-Duruaku
- **Academic advisor:** Dr. Peter Kazanzides
- **Research advisor:** Dr. Samson Jarso
- **Additional personnel:** Dr. Ian Dobbie
- **Programme:** Robotics MSE · 3 credits · letter grade
- **Term:** May 18 – August 13, 2026 · Integrated Imaging Center

## License

Add a license of your choice (for example, an open-source license for code and CAD, and an open license such as CC BY for documentation and data). Until a license file is added, default copyright applies and reuse rights are limited.
