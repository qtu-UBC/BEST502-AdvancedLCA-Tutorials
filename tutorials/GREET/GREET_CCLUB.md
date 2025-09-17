# 🌾 GREET CCLUB Tutorial

The **Carbon Calculator for Land Use and Land Management Change from Biofuels Production (CCLUB)** is an integral component of Argonne National Laboratory’s GREET (Greenhouse gases, Regulated Emissions, and Energy use in Technologies) model (Wang et al., 2020a, 2020b). It is specifically designed to evaluate greenhouse gas (GHG) emissions resulting from both **land use change (LUC)** and **land management change (LMC)** within the broader framework of biofuel life cycle assessment (LCA).


**Note**: This tutorial is adapted from the *[CCLUB User Manual (Rev. 6, Sept 2020)](https://greet.anl.gov/publication-cclub-manual-r6-2020)* by Argonne National Laboratory. For more detail, consult the orginal document.


---

## 📚 CCLUB Resources  
- [**CCLUB Website**](https://bioenergymodels.nrel.gov/models/17/)
   The website page providing an overview of the CCLUB model.   

- [**CCLUB User Manual**](https://greet.anl.gov/publication-cclub-manual-r6-2020) 
   A detailed user manual that includes model documentation, methodological explanations, and step-by-step guidance for using CCLUB.    

---

## 📝 Case Study:
This case study examines the GHG emissions arising from land-use change (LUC) associated with different biofuels, focusing on **ethanol production from four biomass feedstocks: corn, corn stover, switchgrass, and Miscanthus**.


Before beginning the tutorial, let's review the concepts of LUC and its impact by reading the 'Introduction' of [**Understanding options for ILUC mitigation**](https://theicct.org/wp-content/uploads/2021/06/ILUC-Mitigation-Options_ICCT_nov2016_0.pdf).

* **Direct land use change (dLUC)**: refers to the situations where the conversion of land use pattern occurs as a result of the demand for feedstock production for biofuel and bioproducts.
* **Indirect land use change (iLUC)**: refers to the scenarios where the land use pattern changes (e.g., grassland converted to crop land) globally to compensate for the commodity supply which is not fulfilled due to the feedstock production for biofuel and bioproducts locally.

---

### Step 1: Set Up & Files

Before we begin, make sure you have:
- The **CCLUB Excel workbook** (macro-enabled, `.xlsm`).
- (Optional) **GREET** installed if you plan to use the **Copy to GREET** button.
- **Macros enabled** in Excel (CCLUB uses buttons and VBA).

**Open the workbook** and locate the **LUC Scenario & Results** sheet. Inputs appear in **rose-colored** cells; dropdown options appear in **yellow** cells.

---

## Step 2: Choose & Configure Your Scenario (LUC)

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

## Step 3: Run & (Optional) Export to GREET

- Click **Run Simulation** to calculate LUC emissions.
- (Optional) Click **Copy to GREET** to export your inputs & results into a live GREET spreadsheet for integration with full fuel LCA.

---



