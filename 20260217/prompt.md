# Session Prompt: Generate presentation.md for WF29 Climate and Hydrology Analysis

## Task Overview

Create `presentation.md` in `gh-scratch/20260217/`. This markdown file will contain the full text, structure, and figure references for a 10–20 slide presentation titled **"Water Forward 2029 Climate and Hydrology Analysis"**. The presentation is dated **February 2026**.

After `presentation.md` is complete, it will be passed to [Gamma](https://gamma.app/) for conversion to a **16:9 PPTX** file. The final deliverable is the PPTX export from Gamma.

---

## Deliverables

1. **`presentation.md`** — Markdown file containing all slide content, figure references, and structure.
2. **Figures** — Copy (do NOT move) selected PNG/JPG figures from the WF29-CHA repository into `gh-scratch/20260217/`. The originals must remain in place.
3. **Commit and push** — After writing `presentation.md` and copying figures, stage all new files in `gh-scratch/20260217/`, commit, and push to `origin/main`.
4. **Image URLs** — All image references in `presentation.md` must use raw GitHub URLs in the format:
   ```
   ![description](https://raw.githubusercontent.com/RichardHoffpauir/gh-scratch/main/20260217/filename.png)
   ```

---

## Presentation Specifications

### Audience
- Peers, stakeholders, and upper management at Austin Water and partner organizations.
- The audience is familiar with Water Forward from previous iterations (WF18 and WF24) but may have forgotten the details of the Climate and Hydrology Analysis (CHA) from several years ago.
- Tone: informational, professional. This is a progress update — what CHA is, why we are updating it, what is new, and where the work stands.

### Slide Count
- Minimum 10, maximum 20 slides.

### Formatting
- Use clean, well-structured markdown with headings, bullet lists, and tables where appropriate.
- Use `---` (three dashes on a line by itself) to separate slides.
- Keep text concise and slide-appropriate — avoid dense paragraphs. Use bullets, short sentences, and visual callouts.
- Figures should be referenced using standard markdown image syntax with raw GitHub URLs (see Deliverables above).

### Presentation Structure

The presentation must cover the following topics in this order:

#### 1. Title Slide
- Title: "Water Forward 2029 Climate and Hydrology Analysis"
- Date: February 2026
- Presenter attribution as appropriate (consult with user if needed).

#### 2. Refresher: Where CHA Fits in Water Forward
- A brief slide showing how CHA connects to the overall Water Forward planning process.
- The chain: **Climate Projections (GCMs) → CHA (hydrology modeling) → WAM Inputs (flo, eva, fad) → Water Availability Model → Needs Assessment → Strategy Portfolio**.
- Remind the audience that CHA is the technical engine that stress-tests Austin's water supply against future climate scenarios.
- The CHA produces the hydrologic inputs that drive the WAM, which in turn evaluates water supply reliability under hundreds of scenarios.

#### 3. What is the Climate and Hydrology Analysis
- **Purpose/Role**: Develop Colorado River Basin (CRB) Water Availability Model (WAM) hydrologic inputs representative of future climate change conditions.
- **Goals**: Generate climate-adjusted streamflow, evapotranspiration, and lake evaporation projections for the CRB under multiple climate scenarios.
- **Deliverables**: Three WAM input file types:
  - **flo** — streamflow at 45 control points (43 surface watersheds + 2 karst springs: Barton Springs and Dove Creek Springs)
  - **eva** — evapotranspiration (potential and actual ET)
  - **fad** — flow accumulation/routing data

#### 4. Why Are We Updating the CHA for WF29
- Higher resolution GCM data available (LOCA2 at 6 km vs. WF24's 1-degree re-gridding at ~100–110 km).
- More data: 27 GCMs in LOCA2 (vs. 5 in WF24), and multiple ensemble members per GCM.
- Different streamflow modeling framework, progressing across WF iterations:
  - **WF18**: Linear regression model (statistical)
  - **WF24**: Neural network (statistical/data-driven)
  - **WF29**: GR4J conceptual water balance model (process-based)
- Both WF18 and WF24 used essentially statistical models; WF29 transitions to a physically-based approach.
- Addressing topics of future investigation that arose during WF24.

#### 5. WF18 → WF24 → WF29 Evolution
- Show progression across all three iterations of Water Forward CHA.
- Key comparison table:

| Aspect | WF18 | WF24 | WF29 |
|---|---|---|---|
| Downscaling resolution | — | 1° × 1° (~100–110 km) re-gridded | LOCA2 at 6 km |
| Number of GCMs | — | 5 (selected from 35) | 27 available (8 overlap with WF24) |
| SSPs | — | 3 (1-2.6, 2-4.5, 5-8.5) | 3 (2-4.5, 3-7.0, 5-8.5) |
| Ensemble members per GCM | — | 1 | Multiple |
| Streamflow model | Linear regression | Neural network | GR4J (process-based) |
| ETo model | — | Hargreaves-Samani (unconstrained) | Oudin12b (sensitivity-controlled) |
| Historical temp/precip reference | — | PRISM | Livneh (LOCA2 training data) |
| Historical streamflow reference | — | TCEQ WAM for CRB | TCEQ WAM for CRB |

- Note: WF18 details are limited; fill in what is known and use "—" for unknown fields. Consult with the user if more WF18 detail is needed.

#### 6–8. Investigation Topics from WF24 (may span multiple slides)

These are topics identified during WF24 that WF29 is specifically designed to address. Present them in two groups:

**A. GCM Data Topics**

- **Downscaled Spatial Resolution**: Investigating the impact of higher-resolution data. WF24 used 1-degree (~100–110 km) resolution via simple re-gridding of raw CMIP6 output. WF29 uses the LOCA2 dataset at 6 km resolution, which applies localized constructed analogs for downscaling.
- **Sophistication of Bias Correction**: WF24 re-gridded raw GCM output without sophisticated bias correction. LOCA2 uses localized constructed analogs that bias-correct GCM outputs against the Livneh observational dataset.
- **Signal-to-Noise Ratio (Ensemble Members)**: WF24 used only the first ensemble member per GCM. WF29 will use multiple ensemble members available in LOCA2 (e.g., ACCESS-CM2 has 3, EC-Earth3 has multiple) to evaluate whether inter-member variability is significant relative to inter-model spread.

**B. Streamflow Modeling Topic**

- **Data-Driven vs. Process-Based Modeling**: WF24 used a neural network (data-driven). WF29 uses GR4J, a 4-parameter conceptual rainfall-runoff model (process-based water balance). Process-based models have a physical structure that may generalize better to conditions outside the historical calibration range.

**C. Projection Stability**

- **Generating plausible projections under non-stationary conditions**: Both ETo and streamflow models must produce credible results when driven by future climate inputs that exceed the historical range used for calibration.
- Frame the following as design decisions that directly address projection stability:
  - **Oudin12b ETo model**: 13 calibrated parameters (12 monthly + 1 annual offset) constrain temperature sensitivity to ~3% ETo increase per °C warming, avoiding the excessive sensitivity (4–6%/°C) seen in unconstrained models like Blaney-Criddle and Hamon. The Oudin12b model is **complete and ready for use**.
  - **GR4J cross-regime screening**: Behavioral parameter sets are tested across dry, wet, warm, and cool year regimes plus the full calibration period. Acceptance requires KGE ≥ 0.50 for both raw and log flows, and volume bias ≤ 15% in all regimes. This ensures parameter sets that work across varied conditions. The GR4J calibration is **currently in progress**.

#### 9. Two-Phase Project Structure
- **Phase 1 (current focus)**: Generate WAM-ready hydrology files (flo, eva, fad) for the WF29 Preliminary Needs Analysis (PNA).
- **Phase 2 (after PNA)**: Comparative analysis of WF24 vs. WF29 CHA results. Document and understand differences. Sensitivity analysis on the four investigation topics.
- Both phases should be presented; emphasize Phase 1 as the current focus.

#### 10. Schedule and Timeline
- Present an **updated timeline based on actual progress**, not the original June 2025 task schedule.
- Task status as of February 2026:

| Task | Description | Status |
|---|---|---|
| 01 | Data Acquisition (LOCA2, PRISM, gridMET, Livneh, TWDB, GIS) | **COMPLETE** |
| 02 | Data Pre-Processing (subsetting, QDGC aggregation, watershed delineation, QA/QC) | **COMPLETE** |
| 03 | ETo Model Calibration (Oudin12b selected, calibrated, and applied to lake evaporation) | **COMPLETE** |
| 04 | Streamflow Model Calibration (GR4J methodology documented; calibration implementation in progress) | **IN PROGRESS** |
| 05 | Streamflow Projections | Not started |
| 06 | TAG Engagement | Not started |
| 07 | Climate Scenario Assessment & GCM Selection | Not started |
| 08 | Post-Processing (quantile mapping, stochastic sequences) | Not started |
| 09 | WAM Input Generation (flo, eva, fad files) | Not started |

- **TAG note**: The Technical Advisory Group (TAG) — previously referred to as CTAG in earlier planning documents — will be formed in 2026. TAG covers broader topics than climate alone. A meeting schedule has not yet been established; acknowledge that TAG will be formed this year and will be engaged on WF29 CHA updates.
- Show the full timeline through project completion (~2027), sourced from the original schedule but updated with actual completion dates for Tasks 01–03.

#### 11–15 (approximate). Examples of Work Completed
- Select the **best examples** from the completed work in Tasks 01–03 (and the Task 04 methodology document) to illustrate progress.
- These slides should include figures, tables, or bulleted descriptions.
- **You must read the WF29-CHA repository** to identify and select the most compelling and presentation-appropriate figures. Look in:
  - `02_610_PRISM_Livneh_Compare/` — Contains 6 analysis figures comparing PRISM and Livneh datasets (temperature correlations, precipitation comparisons, etc.). These demonstrate data quality assurance.
  - `03_100_Calibrate_ETo_Models/` through `03_400_Lake_Evap/` — Contains ETo calibration results, model comparison figures, sensitivity analysis plots. These demonstrate the ETo methodology.
  - `04_000_GR4J_Calibration_Method/` — Contains the GR4J calibration methodology document. May have useful diagrams or could be summarized in a slide.
- Choose figures that are visually clear, self-explanatory, and relevant to the presentation narrative.
- Copy selected figures into `gh-scratch/20260217/` and reference them via raw GitHub URLs.

#### 16 (approximate). Next Steps
- Closing slide summarizing immediate next steps:
  - Complete GR4J streamflow calibration (Task 04)
  - Generate streamflow projections (Task 05)
  - Form TAG and begin engagement
  - Proceed toward WAM input delivery for PNA

---

## Clarifying Questions Protocol

Before writing `presentation.md`, you may need to ask the user clarifying questions. All questions must follow this format:

- All questions must be numbered sequentially.
- Only one question per number.
- Each question must be structured as one of:
  - **(a) Yes/No/Confirm**
  - **(b) Multiple choice with lettered choices**
  - **(c) Explanation** (ask the user to explain or provide detail)

Example:
> 1. Should the title slide include a subtitle? Yes/No?
> 2. Which figure best represents the ETo calibration work?
>    - (a) Monthly KGE comparison across 4 models
>    - (b) Sensitivity plot (% ETo change per °C)
>    - (c) Calibrated vs. observed ETo time series

---

## Background Information: Water Forward and the Climate and Hydrology Analysis

The following sections provide comprehensive context. Read this material carefully before beginning work.

### What is Water Forward?

Water Forward is the City of Austin's long-range integrated water resource plan (IWRP). It is a 100-year strategic roadmap (planning horizon to 2120) designed to ensure water security for Austin's growing population under climate change uncertainty. The plan is updated on a roughly five-year cycle:

- **WF18** — Water Forward 2018 (the original plan)
- **WF24** — Water Forward 2024 (first update)
- **WF29** — Water Forward 2029 (current update, to be completed in 2029)

Water Forward is built on seven guiding principles: Resiliency, Diversity of Strategy, Holistic & Inclusive Approach, Equity & Affordability, Environmental Protection, Risk Mitigation, and Local Focus.

Austin Water's primary supply comes from the Colorado River and Highland Lakes system. The plan addresses compounding pressures of population growth (service population projected to reach 3.2M) and climate-driven changes in streamflow, evaporation, and drought frequency. Key historical droughts (2008–2016, 2022–2023) confirmed that historical records are insufficient for future planning, leading to the "Droughts Worse than the Drought of Record" (DWDR) planning paradigm.

### Role of the Climate and Hydrology Analysis (CHA) in Water Forward

The CHA is the technical foundation that translates global climate science into local water planning tools. Its role in the Water Forward process:

1. **Climate Projections**: Acquire and process Global Climate Model (GCM) projections of temperature and precipitation.
2. **Hydrologic Modeling**: Convert climate projections into streamflow, evapotranspiration, and lake evaporation estimates for the Colorado River Basin (CRB).
3. **WAM Inputs**: Produce three types of input files for the Water Availability Model:
   - **flo** — streamflow at control points
   - **eva** — evapotranspiration
   - **fad** — flow accumulation data
4. **WAM Simulation**: The WAM uses these inputs to simulate reservoir operations and water supply reliability under hundreds of climate scenarios.
5. **Needs Assessment**: WAM results identify unmet water demand (shortfalls) across scenarios.
6. **Strategy Portfolio**: The needs assessment drives selection and evaluation of water management strategies (conservation, reuse, storage, supply augmentation).

In WF24, the CHA process generated 126 hydrologic input sets that were stress-tested across 666 modeling scenarios. The WF29 CHA will follow the same conceptual pipeline with improved data, methods, and resolution.

### WF24 CHA Methodology

The WF24 CHA was a collaboration between Austin Water, University of Texas researchers, and the Climate Technical Advisory Group (CTAG). Key methodological details:

- **GCM Selection**: 5 GCMs selected from 35 CMIP6 models based on ability to reproduce historical weather patterns in the CRB.
- **Emission Scenarios**: 3 SSPs — SSP1-2.6 (sustainable), SSP2-4.5 (intermediate), SSP5-8.5 (high warming).
- **Downscaling**: Raw CMIP6 GCM outputs were re-gridded to 1° × 1° quadrangles (~100–110 km resolution). No sophisticated bias correction was applied.
- **Historical Reference (temp/precip)**: PRISM dataset.
- **Historical Reference (streamflow)**: TCEQ WAM for the CRB.
- **ETo Model**: Hargreaves-Samani, unconstrained for sensitivity.
- **Streamflow Model**: Neural network (multivariate flow model) trained on historical data (1983–2016) to learn the nonlinear relationship between weather and naturalized river flow.
- **Ensemble Members**: Only the first ensemble member per GCM was used.
- **Post-Processing**: Quantile mapping projected flows onto the historical WAM record (1940–2022). Markov chain simulation generated 10,000-year stochastic hydrology sequences to identify droughts worse than the drought of record.
- **Output**: 126 sets of hydrologic inputs evaluated across 666 modeling scenarios combining climate futures, population growth rates, and regional supply assumptions.

### WF29 CHA Methodology and Advances

The WF29 CHA uses newer CMIP6 data and improved methods. Key details:

- **GCM Data**: LOCA2 dataset — 27 GCMs, 3 SSPs (2-4.5, 3-7.0, 5-8.5), multiple ensemble members per GCM, 6 km resolution, 1950–2100. LOCA2 uses localized constructed analogs for downscaling and bias correction against the Livneh observational dataset.
- **Historical Reference (temp/precip)**: Livneh dataset (1915–2018, 6 km). Livneh is the training data for LOCA2, ensuring consistency between historical calibration and projected forcing.
- **Historical Reference (streamflow)**: TCEQ WAM for the CRB (same as WF24).
- **ETo Model**: Oudin12b — a refined variant of the Oudin model with 13 calibrated parameters (12 monthly + 1 annual offset). Sensitivity is controlled to ~3% ETo increase per °C warming. Calibrated against gridMET reference ETo (1999–2018) and validated (1979–1998). Also applied to TWDB lake evaporation quadrangles. **Complete and ready for use.**
- **Streamflow Model**: GR4J — a 4-parameter daily conceptual rainfall-runoff model. Calibration uses 50,000 Latin Hypercube Samples screened across dry/wet/warm/cool regimes. Acceptance: KGE ≥ 0.50 (raw and log flows) and volume bias ≤ 15% in all regimes. **Methodology complete; calibration implementation in progress.**
- **Control Points**: 43 surface water incremental watersheds + 2 karst springs (Barton Springs, Dove Creek Springs with widened X1 parameter bounds for aquifer storage).
- **Spatial Framework**: 21 TWDB quadrangles × 16 quarter-degree grid cells (QDGCs) per quadrangle = 323 total QDGCs. Area-weight matrices link QDGCs to incremental watersheds.
- **Total Data Volume**: ~3.7 TB across LOCA2, gridMET, PRISM, and Livneh datasets.

### Four Investigation Topics (WF24 → WF29)

These topics were identified during WF24 as areas for future investigation:

**A. GCM Data Topics**
1. **Downscaled Spatial Resolution**: WF24 used 1° re-gridding (~100–110 km). WF29 uses LOCA2 at 6 km. Does higher resolution materially change the hydrologic projections?
2. **Bias Correction Sophistication**: WF24 applied simple re-gridding without bias correction. LOCA2 applies localized constructed analogs. How does this affect projection quality?
3. **Signal-to-Noise Ratio (Ensemble Members)**: WF24 used 1 ensemble member per GCM. WF29 uses multiple. Is inter-member variability significant relative to inter-model spread?

**B. Streamflow Modeling**
4. **Data-Driven vs. Process-Based**: WF24 used a neural network (data-driven). WF29 uses GR4J (process-based). How do the two approaches differ in projection behavior, especially under non-stationary conditions?

**C. Projection Stability**
5. **Non-Stationary Performance**: Can the calibrated models produce plausible projections when driven by climate inputs outside the historical calibration range? The Oudin12b sensitivity control and GR4J cross-regime screening are design decisions that directly address this concern.

### Two-Phase Project Structure

- **Phase 1**: Generate WAM-ready hydrology files (flo, eva, fad) for the WF29 Preliminary Needs Analysis (PNA). This is the current focus.
- **Phase 2**: After PNA completion, conduct a comparative analysis of WF24 vs. WF29 CHA results. Sensitivity analysis on the four investigation topics. Document differences to inform future updates.

### Technical Advisory Group (TAG)

The TAG (Technical Advisory Group) — previously referred to as CTAG (Climate Technical Advisory Group) in earlier planning documents — will cover broader topics than climate alone. TAG will be formed in 2026. A meeting schedule has not yet been established. The presentation should acknowledge TAG formation and planned engagement on WF29 CHA updates.

---

## Source Material Locations

All paths are on the local machine. Read these materials to inform slide content and figure selection.

### Primary Working Repository (WF29-CHA)

**Root**: `D:\Hoffpauir Consulting Dropbox\Richard Hoffpauir\Dropbox-Docs\Consulting\Austin - WF29\Climate and Hydrology Analysis\WF29-CHA\`

Key files and folders:

| Path | Description |
|---|---|
| `README.md` | Project overview, task status table, two-phase strategy |
| `CLAUDE.md` | Project instructions and conventions |
| `.claude/INSTRUCTIONS.md` | Task delegation framework |
| **Task 01 — Data Acquisition** | |
| `01_100_Download_LOCA2/` | LOCA2 GCM download scripts and manifests (27 GCMs) |
| `01_200_Download_PRISM/` | PRISM climate data download script |
| `01_300_Download_gridMET/` | gridMET reference ETo download script |
| `01_400_Download_TWDB_Lake_Evap/` | TWDB monthly lake evaporation data |
| `01_500_Astronomical_Data/` | Solar radiation and photoperiod calculations |
| `01_600_Download_GIS_Files/` | Watershed and QDGC shapefiles |
| **Task 02 — Data Pre-Processing** | |
| `02_100_Subset_LOCA2/` | Subset LOCA2 to CRB extent |
| `02_200_Subset_gridMET/` | Subset gridMET to CRB extent |
| `02_300_Subset_PRISM/` | Subset PRISM to CRB extent |
| `02_400_QDGC_LOCA2/` | Aggregate LOCA2 to QDGCs |
| `02_500_QDGC_gridMET/` | Aggregate gridMET to QDGCs |
| `02_600_QDGC_PRISM/` | Aggregate PRISM to QDGCs |
| `02_610_PRISM_Livneh_Compare/` | **6 analysis figures** — PRISM vs. Livneh dataset comparison (correlations, biases, seasonal patterns). Key QA/QC evidence. |
| `02_700_Incremental_Watersheds/` | Watershed delineation (43 shapefiles) |
| `02_800_Intersect_QDGC_and_Watersheds/` | Area-weight matrices |
| **Task 03 — ETo Models** | |
| `03_100_Calibrate_ETo_Models/` | Calibration of 4 ETo methods (Hargreaves-Samani, Oudin, Blaney-Criddle, Hamon) |
| `03_200_Evaluate_ETo_Calibration_Results/` | Model evaluation with GCM forcing; sensitivity analysis |
| `03_300_Select_and_Refine_ETo_Method/` | Oudin12b variant refinement |
| `03_400_Lake_Evap/` | Lake evaporation using Oudin12b |
| **Task 04 — Streamflow Model** | |
| `04_000_GR4J_Calibration_Method/` | `Calibration_Method.md` (200+ page methodology document) + 34 reference PDFs |

### Older Planning Documents

**Root**: `D:\Hoffpauir Consulting Dropbox\Richard Hoffpauir\Dropbox-Docs\Consulting\Austin - WF29\CHA Schedule\`

| File | Description |
|---|---|
| `WF29 Climate and Hydrology Analysis_20250617.docx` | Project overview (June 2025), two-phase structure, four investigation topics, data/model requirements |
| `WF29 CHA Task Topics.docx` | 8 work packages breakdown |
| `TaskSchedule_20250617.xlsx` | Gantt-style schedule, June 2025 through December 2027 |

**Note**: These documents are from June 2025 and may be outdated in some details. The WF29-CHA README.md reflects the most current project status.

### WF24 Context Document

**Path**: `D:\Hoffpauir Consulting Dropbox\Richard Hoffpauir\Dropbox-Docs\Consulting\Austin - WF29\Climate and Hydrology Analysis\gh-scratch\20260217\wf24_overview.md`

Contains four reports summarizing the WF24 plan, CHA methodology, and how streamflow projections drove the WAM. Useful for understanding the WF24 baseline and framing WF24 → WF29 differences.

### Output Location

**Path**: `D:\Hoffpauir Consulting Dropbox\Richard Hoffpauir\Dropbox-Docs\Consulting\Austin - WF29\Climate and Hydrology Analysis\gh-scratch\20260217\`

- Write `presentation.md` here.
- Copy selected figures (PNG/JPG) here.
- Commit and push all new files to `origin/main`.
- GitHub repo: `https://github.com/RichardHoffpauir/gh-scratch` (public).
- Raw URL base for image references: `https://raw.githubusercontent.com/RichardHoffpauir/gh-scratch/main/20260217/`

---

## Workflow Summary

1. Read the source materials listed above to understand the project deeply.
2. Ask the user clarifying questions (using the numbered format described above) if anything is ambiguous.
3. Browse the WF29-CHA repository for the best figures to include (look in `02_610_*`, `03_*`, `04_000_*`).
4. Write `presentation.md` with 10–20 slides separated by `---`, using raw GitHub URLs for all images.
5. Copy selected figure files (PNG/JPG only) from their source locations into `gh-scratch/20260217/`. Do NOT remove originals.
6. Stage all new files, commit with a descriptive message, and push to `origin/main`.
7. Report the list of figures used and their source locations to the user for verification.
