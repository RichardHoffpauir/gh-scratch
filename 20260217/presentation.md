# Water Forward 2029 Climate and Hydrology Analysis

February 2026

---

## Where Does the CHA Fit in Water Forward?

The Climate and Hydrology Analysis (CHA) is the technical engine that translates global climate science into local water planning tools.

**Climate Projections (GCMs)** → **CHA** → **WAM Inputs** → **Water Availability Model** → **Needs Assessment** → **Strategy Portfolio**

- Global Climate Models (GCMs) project future temperature and precipitation
- The CHA converts those projections into streamflow, evapotranspiration, and lake evaporation for the Colorado River Basin
- These become inputs to the Water Availability Model (WAM), which simulates reservoir operations and water supply reliability
- WAM results identify potential shortfalls across hundreds of climate scenarios
- Shortfall analysis drives evaluation and selection of water management strategies

In WF24, this pipeline produced 126 hydrologic input sets evaluated across 666 modeling scenarios.

---

## What is the Climate and Hydrology Analysis?

### Purpose
Develop Colorado River Basin (CRB) Water Availability Model (WAM) hydrologic inputs representative of future climate change conditions.

### Goals
- Generate climate-adjusted **streamflow** projections at 45 control points across the CRB
- Generate climate-adjusted **evapotranspiration** and **lake evaporation** projections
- Provide robust inputs for evaluating water supply reliability under multiple climate scenarios

### WAM Deliverables
| File Type | Description |
|---|---|
| **flo** | Streamflow at 43 surface water control points + 2 karst springs (Barton Springs, Dove Creek Springs) |
| **eva** | Potential and actual evapotranspiration across the basin |
| **fad** | Flow accumulation and routing data |

---

## Why Are We Updating the CHA for WF29?

### Better Data
- **Higher resolution GCMs**: LOCA2 dataset provides 6 km resolution vs. ~100-110 km in WF24
- **More GCMs**: 27 models available in LOCA2 vs. 5 in WF24
- **Multiple ensemble members** per GCM to assess projection uncertainty

### Better Models
- Transitioning from statistical streamflow models to a **process-based** approach
- WF18: Linear regression | WF24: Neural network | **WF29: GR4J conceptual water balance model**
- Process-based models have physical structure that may generalize better to future conditions outside the historical range

### Addressing Open Questions
- WF24 identified several topics for future investigation
- WF29 is specifically designed to address these topics with improved data and methods

---

## CHA Evolution: WF18 → WF24 → WF29

| Aspect | WF18 | WF24 | WF29 |
|---|---|---|---|
| **Downscaling** | — | Re-gridded to 1° (~100-110 km) | LOCA2 at 6 km |
| **Bias correction** | — | None (simple re-gridding) | LOCA2 localized constructed analogs |
| **Number of GCMs** | — | 5 (selected from 35) | 27 available (8 overlap with WF24) |
| **SSPs** | — | 3 (1-2.6, 2-4.5, 5-8.5) | 3 (2-4.5, 3-7.0, 5-8.5) |
| **Ensemble members** | — | 1 per GCM | Multiple per GCM |
| **Streamflow model** | Linear regression | Neural network | GR4J (process-based) |
| **ETo model** | — | Hargreaves-Samani (unconstrained) | Oudin12b (sensitivity-controlled) |
| **Historical temp/precip** | — | PRISM | Livneh (LOCA2 training data) |
| **Historical streamflow** | — | TCEQ WAM for CRB | TCEQ WAM for CRB |

---

## Investigation Topics: GCM Data

These topics were identified during WF24 for future investigation. WF29 addresses all three.

### A1. Downscaled Spatial Resolution
- WF24 re-gridded raw CMIP6 output to 1° quadrangles (~100-110 km)
- WF29 uses LOCA2 at 6 km — an 18x improvement in linear resolution
- Does higher resolution materially change hydrologic projections?

### A2. Sophistication of Bias Correction
- WF24 applied no bias correction beyond re-gridding
- LOCA2 uses localized constructed analogs to bias-correct GCM outputs against the Livneh observational dataset
- How does bias correction affect projection quality and reliability?

### A3. Signal-to-Noise Ratio (Ensemble Members)
- WF24 used only the first ensemble member per GCM
- WF29 uses multiple members (e.g., ACCESS-CM2 and KACE-1-0-G each have 3 members)
- Is inter-member variability significant relative to inter-model spread?

---

## Investigation Topics: Modeling and Projection Stability

### B. Data-Driven vs. Process-Based Streamflow Modeling
- WF24 used a neural network trained on historical weather-to-flow relationships
- WF29 uses GR4J, a 4-parameter conceptual rainfall-runoff model with explicit water balance accounting
- GR4J's parsimony (only 4 parameters) makes it amenable to exhaustive parameter sampling and robustness screening — an approach that is not feasible with high-dimensional statistical models

### C. Projection Stability Under Non-Stationary Conditions
Both ETo and streamflow models must produce plausible results when driven by future climate inputs that exceed the historical calibration range. Two key design decisions address this:

- **Oudin12b ETo model**: Sensitivity constraint limits ETo response to ~3%/C of warming. **Complete and ready for use.** (Details in later slides.)
- **GR4J calibration strategy**: Cross-regime screening explicitly tests parameter transferability across contrasting climate conditions. **Currently in progress.** (Details in the following two slides.)

---

## The Extrapolation Challenge

Calibrating a model on 20 years of observed history and then driving it with GCM projections through 2100 is fundamentally an **extrapolation problem**. Future temperatures, precipitation patterns, and drought sequences will exceed the range of conditions used during calibration.

### The Problem
- Standard calibration optimizes fit within the historical range
- Parameters that perform well historically can fail under warmer, non-stationary regimes

### The Goal
- Move beyond "good historical fit" to explicitly test for **transferability** across contrasting climate conditions (Klemes, 1986)
- GR4J's 4-parameter structure makes this feasible: we can exhaustively sample the parameter space and screen every candidate against multiple climate regimes

### Consistent Forcing Across Epochs
- **Oudin PET** is used for both historical calibration and GCM projections — same physics in both periods
- **LOCA2** inputs are pre-corrected against Livneh observations — no additional bias correction that would risk "double correction"
- **Historical streamflow** target: TCEQ WAM naturalized flows (1999-2018)

---

## GR4J Calibration: Designing for Robustness

The calibration strategy uses full-period calibration with cross-regime acceptance screening to identify parameter sets that transfer reliably to unseen conditions.

[Conceptual diagram: A horizontal workflow with 5 steps shown as connected arrows or boxes. Step 1: "Forcing Prep" — Oudin PET and LOCA2 quality assurance. Step 2: "Define Regimes" — Split the 1999-2018 calibration period into dry, wet, warm, and cool year groups using terciles, forming a 2x2 grid. Step 3: "LHS Sampling" — Generate 50,000 candidate parameter sets via Latin Hypercube Sampling within physical bounds. Step 4: "Cross-Regime Screening" — Filter: each candidate must achieve KGE >= 0.50 for both raw and log flows, and volume bias <= 15%, in ALL four regimes AND the full period. Step 5: "Projection" — Surviving behavioral parameter sets form an ensemble; each GCM projection is paired with the parameter set that best preserves ensemble flow signatures for that specific future.]

### Key Design Principles
- **Full-period calibration** (1999-2018): Maximizes data availability instead of arbitrary chronological splitting
- **Multi-objective function**: Low flows (KGE of log Q, weight 0.8) + high flows (KGE of raw Q, weight 0.2) + volume balance constraint
- **Ensemble, not single best**: Equifinality is acknowledged — multiple parameter sets can yield similar performance. We retain the full ensemble of behavioral sets that survive screening.
- **Representative Member, not median**: Timestep-wise medians destroy flood peaks and drought durations. A Representative Member is selected via multi-signature matching (mean flow, extremes, variance).
- **Status**: Methodology complete. Calibration implementation in progress for all 45 control points.

---

## Two-Phase Project Structure

### Phase 1 — Current Focus
Generate WAM-ready hydrology files (flo, eva, fad) for the WF29 **Preliminary Needs Analysis (PNA)**.

- Complete streamflow model calibration and projection (Tasks 04-05)
- Conduct climate scenario assessment and GCM selection (Task 07)
- Post-process projections: quantile mapping, stochastic drought sequences (Task 08)
- Deliver WAM input files (Task 09)

### Phase 2 — After PNA Completion
Comparative analysis of WF24 vs. WF29 CHA results.

- Document and understand differences between WF24 and WF29 methodologies and projections
- Conduct sensitivity analyses on all four investigation topics
- Inform future Water Forward updates

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

**Technical Advisory Group (TAG)**: The TAG will be formed in 2026 and will be engaged on WF29 CHA updates. TAG covers broader topics than climate alone. Meeting schedule to be determined.

---

## Spatial Framework

The CHA uses a multi-scale spatial framework covering the Colorado River Basin.

- **21 TWDB quadrangles** (1° x 1°) define the coarse grid (black boundaries)
- **323 quarter-degree grid cells (QDGCs)** at 0.25° resolution provide the climate data framework (magenta grid)
- **43 incremental watersheds** delineated from HUC12 boundaries define the hydrologic modeling units (colored regions)
- Area-weight matrices link QDGCs to watersheds for spatial integration of climate data

![Colorado River Basin spatial grid showing quadrangles and QDGCs](https://raw.githubusercontent.com/RichardHoffpauir/gh-scratch/main/20260217/fig_crb_spatial_grid.png)

![QDGCs and incremental watersheds overlaid on the CRB](https://raw.githubusercontent.com/RichardHoffpauir/gh-scratch/main/20260217/fig_qdgc_watershed_overlay.png)

---

## ETo Model Evaluation: Sensitivity Comparison

Four temperature-based ETo models were calibrated against gridMET reference ETo (1999-2018) and then evaluated for sensitivity when driven by GCM projections.

- **Blaney-Criddle** (~4.4%/C) and **Hamon** (~6%/C) show excessive sensitivity — approaching the Clausius-Clapeyron theoretical ceiling of ~7%/C
- **Hargreaves-Samani** (~3%/C) and **Oudin** (~2.8%/C) cluster near the 3%/C physically defensible target
- Oudin was selected for refinement due to its low sensitivity and reliance on robust inputs (extraterrestrial radiation and mean temperature only)

![ETo sensitivity boxplot comparing four models: Hargreaves-Samani, Oudin, Blaney-Criddle, and Hamon](https://raw.githubusercontent.com/RichardHoffpauir/gh-scratch/main/20260217/fig_eto_sensitivity_4models.png)

---

## Oudin12b: Sensitivity Control Through the Projection Period

The refined Oudin12b variant uses a constraint parameter (c) that actively limits ETo sensitivity as warming increases through 2100. This three-panel view shows the mechanism under SSP3-7.0:

- **Left — c parameter**: Grows increasingly negative over time, applying stronger correction as GCM temperatures diverge further from the historical calibration range
- **Center — Mean ETo**: The constrained model (blue) rises moderately compared to the unconstrained version (orange), with the gap exceeding 1 mm/d by 2100
- **Right — Sensitivity**: Without the constraint, sensitivity remains at ~8%/C (orange). With the constraint, sensitivity converges toward the 3% target (blue) and holds steady through 2100

This design ensures **projection stability** — plausible ETo estimates even under significant warming far outside the historical calibration range.

![Three-panel time series showing Oudin12b sensitivity constraint behavior from 2015 to 2100 under SSP3-7.0](https://raw.githubusercontent.com/RichardHoffpauir/gh-scratch/main/20260217/fig_oudin12b_sensitivity_timeseries.png)

---

## Oudin12b: Calibration Results

### Reference Evapotranspiration (ETo)
Calibrated against gridMET observations (1999-2018). The Oudin12b model accurately captures the seasonal cycle of ETo, with close agreement across all 12 months.

![Monthly mean daily ETo: Oudin12b vs. gridMET observations](https://raw.githubusercontent.com/RichardHoffpauir/gh-scratch/main/20260217/fig_oudin12b_monthly_eto.png)

### Lake Evaporation
Applied to TWDB quadrangle-level lake evaporation data. Annual total bias is only -0.9% (modeled 1,322 mm vs. observed 1,334 mm), with March-October monthly totals agreeing within 1.1%.

![Monthly lake evaporation: Oudin12b vs. TWDB observations](https://raw.githubusercontent.com/RichardHoffpauir/gh-scratch/main/20260217/fig_oudin12b_lake_evap.png)

---

## Next Steps

### Immediate (2026)
- Complete GR4J streamflow model calibration for all 45 control points (Task 04)
- Generate streamflow projections using calibrated models with LOCA2 GCM data (Task 05)
- Form the Technical Advisory Group (TAG) and begin engagement on CHA updates

### Near-Term
- Conduct climate scenario assessment and GCM selection (Task 07)
- Post-process projections: quantile mapping onto historical WAM record, stochastic drought sequence generation (Task 08)
- Deliver WAM input files (flo, eva, fad) for the Preliminary Needs Analysis (Task 09)

### Phase 2
- Comparative analysis of WF24 vs. WF29 CHA results
- Sensitivity analyses on all four investigation topics
- Technical documentation for future Water Forward updates
