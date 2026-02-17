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
- Process-based models have physical structure (soil moisture, routing, storage) that may extrapolate more reliably to conditions not seen during calibration

### C. Projection Stability Under Non-Stationary Conditions
Both ETo and streamflow models must produce plausible results when driven by future climate inputs that exceed the historical calibration range. Two key design decisions address this:

- **Oudin12b ETo model**: 13 calibrated parameters constrain temperature sensitivity to ~3% ETo increase per degree C of warming, avoiding excessive sensitivity seen in unconstrained models (4-6%/C). **Complete and ready for use.**
- **GR4J cross-regime screening**: Parameter sets are tested across dry, wet, warm, and cool year regimes. Acceptance requires KGE >= 0.50 and volume bias <= 15% in all regimes, ensuring robustness across varied conditions. **Currently in progress.**

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

## Data Quality: PRISM vs. Livneh Comparison

WF29 uses the Livneh dataset as the historical reference for temperature and precipitation because it is the training data for LOCA2. A thorough comparison with PRISM (the WF24 reference) confirmed high agreement across 317 QDGCs.

- **Temperature** (tmax, tmin): Daily correlations r > 0.98 with minimal spatial variability
- **Precipitation**: Daily correlation mean r = 0.78 (timing differences at the daily scale), but these cancel at monthly aggregation (r = 0.95)
- **Conclusion**: The two datasets are functionally interchangeable at the monthly scale relevant to WAM inputs

![Daily Pearson correlation between PRISM and Livneh across 317 QDGCs for precipitation, tmax, and tmin](https://raw.githubusercontent.com/RichardHoffpauir/gh-scratch/main/20260217/fig_prism_livneh_correlation.png)

---

## ETo Model Evaluation: Sensitivity Comparison

Four temperature-based ETo models were calibrated against gridMET reference ETo (1999-2018) and then evaluated for sensitivity when driven by GCM projections.

- **Blaney-Criddle** (~4.4%/C) and **Hamon** (~6%/C) show excessive sensitivity — approaching the Clausius-Clapeyron theoretical ceiling of ~7%/C
- **Hargreaves-Samani** (~3%/C) and **Oudin** (~2.8%/C) cluster near the 3%/C physically defensible target
- Oudin was selected for refinement due to its low sensitivity and reliance on robust inputs (extraterrestrial radiation and mean temperature only)

![ETo sensitivity boxplot comparing four models: Hargreaves-Samani, Oudin, Blaney-Criddle, and Hamon](https://raw.githubusercontent.com/RichardHoffpauir/gh-scratch/main/20260217/fig_eto_sensitivity_4models.png)

---

## Oudin12b: Controlling Sensitivity for Projection Stability

The refined Oudin12b variant uses 13 calibrated parameters (12 monthly + 1 annual sensitivity constraint) to control ETo response under warming.

- **Oudin (2-param)**: Original formulation — low sensitivity (~2.8%/C) but limited seasonal flexibility
- **Oudin12b (no limit)**: 12 monthly parameters improve seasonal fit but sensitivity jumps to ~7.5%/C (excessive)
- **Oudin12b (with limit)**: Adding the annual sensitivity constraint brings sensitivity back to ~3%/C while retaining monthly calibration flexibility

This design decision directly addresses **projection stability** — ensuring plausible ETo estimates even under significant warming.

![Oudin12b sensitivity before and after applying the annual constraint parameter](https://raw.githubusercontent.com/RichardHoffpauir/gh-scratch/main/20260217/fig_oudin12b_sensitivity_control.png)

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
