# Water Forward 2029 Climate and Hydrology Analysis

February 2026

---

## Where Does the CHA Fit in Water Forward?

**Climate Projections (GCMs)** → **CHA** → **WAM Inputs** → **Water Availability Model** → **Needs Assessment** → **Strategy Portfolio**

- GCMs project future temperature and precipitation
- CHA converts projections into streamflow, evapotranspiration, and lake evaporation for the Colorado River Basin (CRB)
- The Water Availability Model (WAM) uses these inputs to simulate reservoir operations and water supply reliability across hundreds of climate scenarios
- Results drive evaluation of water management strategies

In WF24, this pipeline produced 126 hydrologic input sets evaluated across 666 modeling scenarios.

---

## What is the Climate and Hydrology Analysis?

### Purpose
Develop CRB WAM hydrologic inputs representative of future climate change conditions.

### Goals
- Climate-adjusted **streamflow** projections at 45 control points
- Climate-adjusted **evapotranspiration** and **lake evaporation** projections
- Robust inputs for evaluating water supply reliability under multiple climate scenarios

### WAM Deliverables
| File Type | Description |
|---|---|
| **flo** | Streamflow at 43 surface water control points + 2 karst springs (Barton Springs, Dove Creek Springs) |
| **eva** | Evapotranspiration across the basin |
| **fad** | Flow accumulation and routing data |

---

## Why Are We Updating the CHA for WF29?

### Better Data
- **Higher resolution**: LOCA2 at 6 km vs. ~100-110 km in WF24
- **More GCMs**: 27 in LOCA2 vs. 5 in WF24
- **Multiple ensemble members** per GCM for uncertainty assessment

### Better Models
- Transitioning from statistical to **process-based** streamflow modeling
- WF18: Linear regression | WF24: Neural network | **WF29: GR4J water balance model**

### Addressing Open Questions
- WF24 identified several topics for future investigation
- WF29 addresses these with improved data and methods

---

## CHA Evolution: WF18 → WF24 → WF29

| Aspect | WF18 | WF24 | WF29 |
|---|---|---|---|
| **Downscaling** | Statistical | Re-gridded to 1° (~100-110 km) | LOCA2 at 6 km |
| **Bias correction** | — | Mean and variance | LOCA2 localized constructed analogs |
| **Number of GCMs** | 20 | 5 (selected from 35) | 27 available (8 overlap with WF24) |
| **SSPs** | 2 (RCP 4.5 and 8.5) | 3 (1-2.6, 2-4.5, 5-8.5) | 3 (2-4.5, 3-7.0, 5-8.5) |
| **Ensemble members** | 1 per GCM | 1 per GCM | Multiple per GCM |
| **Streamflow model** | Linear regression | Neural network | GR4J (process-based) |
| **ETo model** | not used | Hargreaves-Samani (unconstrained) | Oudin12b (sensitivity-controlled) |
| **Historical temp/precip** | weather stations | PRISM | Livneh (LOCA2 training data) |
| **Historical streamflow** | TCEQ WAM for CRB | TCEQ WAM for CRB | TCEQ WAM for CRB |

---

## Investigation Topics: GCM Data

Topics identified during WF24 for future investigation.

### A1. Downscaled Spatial Resolution
- WF24: 1° quadrangles (~100-110 km). WF29: LOCA2 at 6 km (18x finer).
- Does higher resolution materially change hydrologic projections?

### A2. Sophistication of Bias Correction
- WF24: simple re-gridding, no bias correction. WF29: LOCA2 localized constructed analogs against Livneh observations.
- How does bias correction affect projection quality?

### A3. Signal-to-Noise Ratio (Ensemble Members)
- WF24: 1 ensemble member per GCM. WF29: multiple members available.
- Is inter-member variability significant relative to inter-model spread?

---

## Investigation Topics: Modeling and Projection Stability

### B. Data-Driven vs. Process-Based Streamflow Modeling
- WF24: neural network (statistical, many parameters)
- WF29: GR4J, a 4-parameter conceptual rainfall-runoff model
- GR4J's parsimony enables exhaustive parameter sampling and robustness screening — not feasible with high-dimensional statistical models

### C. Projection Stability Under Non-Stationary Conditions
Models must produce plausible results when driven by climate inputs outside the historical calibration range. Two design decisions address this:

- **Oudin12b ETo**: Sensitivity constrained to ~3%/C. **Complete.**
- **GR4J calibration**: Cross-regime screening tests parameter transferability. **In progress.**

---

## Schedule and Progress

| Task | Description | Status |
|---|---|---|
| 01 | Data Acquisition (LOCA2, PRISM, gridMET, Livneh, TWDB, GIS) | **Complete** |
| 02 | Data Pre-Processing (subsetting, QDGC aggregation, watershed delineation, QA/QC) | **Complete** |
| 03 | ETo Model Calibration (Oudin12b selected, calibrated, applied to lake evaporation) | **Complete** |
| 04 | Streamflow Model Calibration (GR4J methodology documented; calibration in progress) | **In Progress** |
| 05 | Streamflow Projections | Not Started |
| 06 | TAG Engagement | Not Started |
| 07 | Climate Scenario Assessment and GCM Selection | Not Started |
| 08 | Post-Processing (quantile mapping, stochastic sequences) | Not Started |
| 09 | WAM Input Generation (flo, eva, fad files) | Not Started |

**TAG**: The Technical Advisory Group will be formed in 2026. Meeting schedule TBD.

---

## Spatial Framework

- **21 TWDB quadrangles** (1° x 1°) — coarse grid (black boundaries)
- **323 quarter-degree grid cells (QDGCs)** at 0.25° — climate data framework (magenta grid)
- **43 incremental watersheds** from HUC12 boundaries — hydrologic modeling units (colored regions)
- Area-weight matrices link QDGCs to watersheds for spatial integration

![Colorado River Basin spatial grid showing quadrangles and QDGCs](https://raw.githubusercontent.com/RichardHoffpauir/gh-scratch/main/20260217/fig_crb_spatial_grid.png)

![QDGCs and incremental watersheds overlaid on the CRB](https://raw.githubusercontent.com/RichardHoffpauir/gh-scratch/main/20260217/fig_qdgc_watershed_overlay.png)

---

## ETo Model Evaluation: Sensitivity Comparison

Four temperature-based ETo models calibrated against gridMET (1999-2018), then evaluated for sensitivity under GCM projections.

- **Blaney-Criddle** (~4.4%/C) and **Hamon** (~6%/C): excessive — approaching the ~7%/C Clausius-Clapeyron ceiling
- **Hargreaves-Samani** (~3%/C) and **Oudin** (~2.8%/C): near the 3%/C physically defensible target
- Oudin selected for refinement — low sensitivity, robust inputs (extraterrestrial radiation + mean temperature)

![ETo sensitivity boxplot comparing four models](https://raw.githubusercontent.com/RichardHoffpauir/gh-scratch/main/20260217/fig_eto_sensitivity_4models.png)

---

## Oudin12b: Sensitivity Control Through the Projection Period

Oudin12b uses a constraint parameter (c) that actively limits ETo sensitivity as warming increases. Three-panel view under SSP3-7.0:

- **Left — c parameter**: Grows more negative over time as GCM temperatures diverge from the calibration range
- **Center — Mean ETo**: Constrained (blue) rises moderately vs. unconstrained (orange); gap exceeds 1 mm/d by 2100
- **Right — Sensitivity**: Constrained converges to 3% target and holds steady; unconstrained stays at ~8%/C

![Oudin12b sensitivity constraint behavior from 2015 to 2100 under SSP3-7.0](https://raw.githubusercontent.com/RichardHoffpauir/gh-scratch/main/20260217/fig_oudin12b_sensitivity_timeseries.png)

---

## Oudin12b: Calibration Results

### Reference ETo
Calibrated against gridMET (1999-2018). Close agreement across all 12 months.

![Monthly mean daily ETo: Oudin12b vs. gridMET observations](https://raw.githubusercontent.com/RichardHoffpauir/gh-scratch/main/20260217/fig_oudin12b_monthly_eto.png)

### Lake Evaporation
Calibrated against TWDB data. Annual bias: -0.9%. March-October monthly totals within 1.1%.

![Monthly lake evaporation: Oudin12b vs. TWDB observations](https://raw.githubusercontent.com/RichardHoffpauir/gh-scratch/main/20260217/fig_oudin12b_lake_evap.png)

---

## The Extrapolation Challenge

Calibrating on 20 years of history and projecting through 2100 is an **extrapolation problem**. Future conditions will exceed the calibration range.

### Problem and Goal
- Standard calibration optimizes historical fit — but parameters can fail under non-stationary regimes
- Goal: explicitly test **transferability** across contrasting climate conditions (Klemes, 1986)
- GR4J's 4-parameter structure makes this feasible — we can exhaustively sample and screen the full parameter space

### Consistent Forcing Across Epochs
- **Oudin PET** used for both calibration and projection — same physics in both periods
- **LOCA2** inputs pre-corrected against Livneh — no "double correction"
- **Streamflow target**: TCEQ WAM naturalized flows (1999-2018)

---

## GR4J Calibration: Designing for Robustness

Full-period calibration with cross-regime acceptance screening identifies parameter sets that transfer to unseen conditions.

[Conceptual diagram: A horizontal workflow with 5 connected steps. Step 1: "Forcing Prep" — Oudin PET and LOCA2 quality assurance. Step 2: "Define Regimes" — Split 1999-2018 into dry, wet, warm, and cool year groups using terciles (2x2 grid). Step 3: "LHS Sampling" — 50,000 candidate parameter sets via Latin Hypercube Sampling. Step 4: "Cross-Regime Screening" — Each candidate must achieve KGE >= 0.50 (raw and log flows) and volume bias <= 15% in ALL four regimes AND the full period. Step 5: "Projection" — Surviving behavioral sets form an ensemble; each GCM projection paired with the parameter set that best preserves ensemble flow signatures.]

### Key Design Principles
- **Full-period calibration** (1999-2018) instead of arbitrary split-sample
- **Multi-objective**: Low flows (KGE of log Q, weight 0.8) + high flows (KGE of raw Q, weight 0.2) + volume constraint
- **Ensemble, not single best**: Retain all behavioral parameter sets that survive screening
- **Representative Member, not median**: Selected via multi-signature matching (mean flow, extremes, variance) — timestep medians destroy flood peaks and drought durations
- **Status**: Methodology complete. Calibration in progress for 45 control points.

---

## Next Steps

### Immediate (2026)
- Complete GR4J calibration for all 45 control points (Task 04)
- Generate streamflow projections with LOCA2 GCM data (Task 05)
- Form TAG and begin engagement on CHA updates

### Near-Term
- Climate scenario assessment and GCM selection (Task 07)
- Post-processing: quantile mapping, stochastic drought sequences (Task 08)
- Deliver WAM input files for Preliminary Needs Analysis (Task 09)

### Future
- WF24 vs. WF29 comparative analysis
- Sensitivity analyses on all four investigation topics
