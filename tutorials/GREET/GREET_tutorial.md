# ⛽ CCLUB (Carbon Calculator for LUC/LMC) Excel Tutorial

The **Carbon Calculator for Land Use and Land Management Change from Biofuels Production (CCLUB)** is an Excel-based tool developed by Argonne National Laboratory to estimate **land-use change (LUC)** and **land-management change (LMC)** greenhouse gas (GHG) emissions associated with biofuels. This tutorial guides students through running CCLUB step by step, using the **LUC Scenario & Results** worksheet.

**Note**: This tutorial is adapted from the *CCLUB User Manual (Rev. 6, Sept 2020)* by Argonne National Laboratory. For full details, consult the official manual included with the CCLUB package.

---

## 📥 Step 1: Set Up & Files

Before you begin, make sure you have:
- The **CCLUB Excel workbook** (macro-enabled, `.xlsm`).
- (Optional) **GREET** installed if you plan to use the **Copy to GREET** button.
- **Macros enabled** in Excel (CCLUB uses buttons and VBA).

**Open the workbook** and locate the **LUC Scenario & Results** sheet. Inputs appear in **rose-colored** cells; dropdown options appear in **yellow** cells.

---

## 🧭 Step 2: Choose & Configure Your Scenario (LUC)

Follow the inputs **top → bottom** on the **LUC Scenario & Results** sheet, then run the model.

### 2.1 Select the Fuel Pathway
Pick a pathway from the dropdown (e.g., *Corn Ethanol*, *Switchgrass Ethanol*, *Soy Biodiesel*, *HEFA SAF*, *ATJ/ETJ/FT SAF* variants). This determines which **GTAP** land-use-change matrix (vintage/case) CCLUB will use.

### 2.2 Set Domestic (U.S.) SOC & N₂O Modeling — *Input 2*
These settings affect **U.S. (domestic)** emissions only:
- **2a — Domestic carbon EF basis**: choose the U.S. dataset/method for belowground & aboveground carbon.
- **2b — Yield assumption (if SOC modeling)**: specify whether SOC modeling assumes yield increases.
- **2c — Tillage (corn/corn-stover pathways)**: choose CT/RT/NT or U.S. average.
- **2d — Soil depth**: 30 cm or 100 cm for soil-organic-carbon (SOC) calculations.
- **2e — Domestic N₂O method**: select the U.S. N₂O estimation approach.

> **Definitions**
> - **Belowground carbon**: soil and root carbon pools (SOC), modeled at U.S. county level (parameterized **CENTURY**).
> - **Aboveground carbon**: forest biomass carbon (trees, litter, debris), characterized for U.S. forests via **COLE** (Carbon Online Estimator).

### 2.3 Set International Dataset — *Input 3*
- **3a — International dataset**: choose **Winrock** (country/state-level) or **Woods Hole/AEZ-EF** (biome/AEZ-level) for **non-U.S.** carbon, CH₄, and N₂O emission factors (EFs).
- **3b — Palm expansion on peat (Winrock only)**: percent of palm expansion on peat in SE Asia (commonly **0%** or **22%**).

> **Tip (Canada-focused analysis):** Canada is **international** in CCLUB. Select **Winrock** to use **country-level** EFs for Canada.

### 2.4 Configure Forest Products Assumption (U.S.) — *Input 4*
Choose **HWP (Harvested Wood Products)** handling for U.S. forests when converted:
- **Heath et al. (1996)** assumptions, or
- **All aboveground C emitted** (no product credit).

### 2.5 Biomass Burning in International Clearing — *Input 5*
- With **Winrock**: “Yes” applies burning only in countries where it is common (per Winrock); “No” disables it.
- With **CENTURY/Woods Hole**: “Yes” applies burning in all international countries; “No” disables it.

### 2.6 U.S. Forest Adjustment (Proration) — *Input 6*
Toggle **Yes** to apply CCLUB’s adjustment that splits GTAP “forest” conversions into **mature forest** vs **young-forest/shrub** (to better match U.S. inventories); **No** keeps raw GTAP.

### 2.7 Spatial Averaging Method — *Input 7*
Choose how EFs are aggregated spatially (e.g., **area-weighted**). Applies to both domestic and international EF aggregation.

### 2.8 Foregone Sequestration Period — *Input 8*
Use **30 years** to align with underlying EF time horizons (consistent with CENTURY/Winrock modeling). Large deviations can lead to inconsistent results.

### 2.9 Amortization Period — *Input 9*
Set the policy analysis horizon (e.g., **30 years**) over which total LUC emissions are annualized.

---

## ▶️ Step 3: Run & (Optional) Export to GREET

- Click **Run Simulation** to calculate LUC emissions.
- (Optional) Click **Copy to GREET** to export your inputs & results into a live GREET spreadsheet for integration with full fuel LCA.

---

## 📊 Step 4: Read the Results (What to Report)

The **results table** on the right reports **Domestic (U.S.)** and **International (non-U.S.)** contributions, each split by land type:
- Forest, grassland, cropland-pasture, and (for some datasets) young forest–shrub.

For each side (domestic/international), CCLUB reports:
- **Emissions (Mg C)** and **Emissions (Mg CO₂e)** (using **3.67 g CO₂e/g C**),
- **Annualized emissions (Mg CO₂e/yr)** (divides by your amortization period),
- **Fuel-basis metrics**: **g CO₂e/gal** and **g CO₂e/MJ** (using LHV ≈ **80.53 MJ/gal** ethanol or **126.13 MJ/gal** biodiesel),
- A **red box** with **total g CO₂e/MJ** (sum of carbon, N₂O, and CH₄).

> **Reminder:** “Domestic” = U.S. only. Canada and all other countries are part of the **International** totals.

---

## 🔎 Step 5: Traceability — Where Numbers Come From

Use these tabs to audit any run:
1. **GTAP Data** — Land-use-change areas by **region** and **AEZ** for the selected pathway (bottom = raw GTAP; middle/top = summaries used in modeling).
2. **Domestic C-Factors / International C-Factors** — Emission factors (EFs) for U.S. vs non-U.S. transitions.
3. **Modeling** — Where **areas × EFs** are combined; color-coded to distinguish soil/non-soil/growth; applies U.S. forest proration where selected.
4. **Saved Results** — Store scenario outputs for later reference or for GREET ingestion.

---

## 🧪 Step 6: Two Quick Case Recipes

### A. Canada-focused ethanol/biodiesel
- **Input 1**: pick a Canada-relevant pathway (e.g., *Corn Ethanol (GTAP 2017)* or *Canola Biodiesel (GTAP 2017)* if available in your build).
- **Input 2**: any option (affects U.S. only; no impact on Canada).
- **Input 3a**: **Winrock** (country-level international EFs); **3b**: 0% (peat expansion applies to SE Asia).
- **Inputs 4–9**: set as needed; keep **Input 8 = 30 years**; choose amortization (e.g., 30 years).
- **Run** and read **International** columns; Canada’s contribution is within the international totals (trace details in **GTAP Data** and **International C-Factors**).

### B. U.S. forestry sensitivity
- Toggle **Input 4** (HWP) and **Input 6** (forest proration) to see effects on aboveground forest carbon handling and GTAP forest allocation.

---

## 🧠 Learning Outcomes

By the end of this tutorial, you will be able to:
- Configure and run **CCLUB** for different biofuel pathways and GTAP vintages.
- Interpret **LUC GHG results** (g CO₂e/MJ) by domestic vs international contributions and by land type.
- Trace results back to **GTAP** area changes and **EF** sources (CENTURY/COLE for U.S.; Winrock/Woods Hole for international).
- Export LUC results to **GREET** for integration with full fuel life cycle modeling.

---

## 📚 Reference Materials

- *CCLUB User Manual* (Rev. 6, Sept 2020), Argonne National Laboratory — full documentation of data sources, worksheets, and methodology.
- GREET documentation — for integrating CCLUB outputs into full LCA workflows.