# 🌾 GREET CCLUB Tutorial

The **Carbon Calculator for Land Use and Land Management Change from Biofuels Production (CCLUB)** is an integral component of Argonne National Laboratory’s GREET (Greenhouse gases, Regulated Emissions, and Energy use in Technologies) model. It is specifically designed to evaluate greenhouse gas (GHG) emissions resulting from both **land use change (LUC)** and **land management change (LMC)** within the broader framework of biofuel life cycle assessment (LCA).


**Note**: This tutorial is adapted from the *[CCLUB User Manual (Rev. 6, Sept 2020)](https://greet.anl.gov/publication-cclub-manual-r6-2020)* by Argonne National Laboratory. For more detail, consult the orginal document.


---

## 📚 CCLUB Resources  
- [**CCLUB Website**](https://bioenergymodels.nrel.gov/models/17/)
   The website page providing an overview of the CCLUB model.   

- [**CCLUB User Manual**](https://greet.anl.gov/publication-cclub-manual-r6-2020) 
   A detailed user manual that includes model documentation, methodological explanations, and step-by-step guidance for using CCLUB.    

---

## 📝 Case Study:
This case study explores the GHG emissions arising from LUC across different **bioethanol production pathway**, focusing on ethanol derived from **four biomass feedstocks: corn, corn stover, switchgrass, and Miscanthus**.


### Background Reading
1. Before starting the tutorial, let's review the concepts of LUC and their impacts by reading the *'Introduction'* section of [**Understanding options for ILUC mitigation**](https://theicct.org/wp-content/uploads/2021/06/ILUC-Mitigation-Options_ICCT_nov2016_0.pdf). To summarize, **direct land use change (dLUC)** refers to the situations where the conversion of land use pattern occurs as a result of the demand for feedstock production for biofuel and bioproducts.**Indirect land use change (iLUC)** refers to the scenarios where the land use pattern changes (e.g., grassland converted to crop land) globally to compensate for the commodity supply which is not fulfilled due to the feedstock production for biofuel and bioproducts locally.

2. Next, read the *'Introduction'* section of the [**CCLUB User Manual**](https://greet.anl.gov/publication-cclub-manual-r6-2020). This section provides background on the purpose of the CCLUB model and explain how CCLUB uses **Global Trade Analysis Project (GTAP)** outputs with emission factors (EF) to estimate GHG emissions of LUC. 

---

### Step 1: Set Up & Files

Before you begin, make sure you have:
- `CCLUB_2024_Rev1.xlsm` saved in your GREET download folder (e.g., **R&D GREET_2024 Rev1**) from the *1_GREET_tutorial*.


Open the Excel workbook. Here is an overview of the CCLUB worksheets:
| Worksheet                  | Description |
|----------------------------|-------------|
| Overview                   | Information on CCLUB-related documentation. |
| Scenario & Results         | Enables selection of data sources, key assumptions, and biofuel production scenarios, and displays results. Includes two worksheets for LUC and LMC scenarios. |
| Modeling                   | Computes carbon, N₂O, and CH₄ emissions from LUC. |
| Domestic C-Factors         | Derives carbon and N₂O emission factors for domestic LUC. |
| International C-Factors    | Derives carbon, N₂O, and CH₄ emission factors for international LUC. |
| GTAP Data                  | Lists and summarizes GTAP source data. |
| C-Database                 | Contains soil carbon emission factors from a parameterized CENTURY model and forest aboveground carbon data from COLE at county level for domestic LUC and LMC. |
| Forest Land Area           | Computes forest correction factor for shrubland transitions. |
| International Conversion   | Source data for international land conversions. |
| International Reversion    | Source data for international land reversions. |
| Saved Results              | LUC and LMC results to be used in GREET. |


- Locate the **LUC Scenario & Results** sheet — this is where we will calculate the GHG emissions associated with LUC for bioethanol production pathways.

---

## Step 2: Choose & Configure Your Scenario (LUC)

Follow the inputs **top → bottom** on the **LUC Scenario & Results** sheet, then review the results at the end. Users select input values in the **rose-colored** cells. All options are visible in the **yellow** cells in each section.

### 2.1 Select Feedstock to Fuel Pathway — *Input 1*
The first user input (Input 1) is the feedstock-to-fuel pathway. The user can choose from among the biofuel production scenarios, which include options for corn and cellulosic ethanol feedstock (corn stover, switchgrass, or Miscanthus), and soy biodiesel. Each scenario reflects a shock to the economy in response to an increase in demand for a particular biofuel modeling by **GTAP**. In this case study, we will focus on the following ethanol production scenarios:
| # | Ethanol Pathway       | GTAP Case Description                                                                 |
|---|------------------------|---------------------------------------------------------------------------------|
| 1 | Corn Ethanol 2011      | Increase in corn ethanol production from its 2004 level (3.41 BG) to 15 BG      |
| 2 | Stover Ethanol         | Increase of ethanol from corn stover by 9 BG, on top of 15 BG corn ethanol (continuous corn) |
| 3 | Switchgrass Ethanol    | Increase of ethanol from switchgrass by 7 BG, on top of 15 BG corn ethanol      |
| 4 | Miscanthus Ethanol     | Increase of ethanol from miscanthus by 7 BG, on top of 15 BG corn ethanol       |

**Note**: For more details on GTAP modeling, see *Section 2* of the **CCLUB User Manual**.

### 2.2 Select an SOC & N₂O Modeling Scenario — *Input 2*
User input 2 allows the user to specify how soil organic carbon (SOC) and nitrous oxide (N₂O) emissions are modeled for both domestic and international LUC. These options determine which datasets and emission factors are applied in the calculations.

Here’s what each option means:
| Option | Name             | Domestic SOC & N₂O Source | International SOC & N₂O Source | Characteristics |
|--------|-----------------------------|----------------------------|--------------------------------|-------------------------------------|
| 1      | DayCent & Winrock          | **DayCent** (process-based SOC at daily timestep) + **COLE** for forest aboveground carbon | **Winrock dataset** country-/administrative-level EFs for forest, grassland, and cropland pasture conversions. Key assumptions: (1) Includes CH₄ and N₂O emissions from biomass burning during land clearing; (2) No carbon storage in harvested wood products (HWP); and (3) Includes foregone sequestration | Provides empirically derived, country-level LUC emission factors and serves as the EPA default conservative baseline, often resulting in higher emissions (e.g., due to exclude HWP carbon storage.) |
| 2      | DayCent & AEZ-EF           | **DayCent** + **COLE**    | **AEZ-EF** (Agro-Ecological Zone emission factors) | Hybrid approach combining U.S. process-based SOC modeling with AEZ-level international carbon/N₂O factors:contentReference[oaicite:1]{index=1}. |
| 3      | AEZ-EF                     | **AEZ-EF** (applied domestically with COLE for forest) | **AEZ-EF** | Simplified and consistent option; uses spatially explicit AEZ-level emission factors for both domestic and international LUC. |
| 4      | Century & Winrock          | **CENTURY** (parameterized SOC model, inverse modeling) + **COLE** | **Winrock dataset** | Uses CENTURY-based SOC estimates at county/AEZ level; combined with Winrock’s empirical international dataset:contentReference[oaicite:3]{index=3}. |
| 5      | Other methods (Sec. 3–5)   | Alternatives: CENTURY/COLE, Woods Hole | Alternatives: Winrock or Woods Hole, IPCC factors | Allows use of alternative datasets (e.g., Woods Hole biome-level EFs, IPCC defaults) for advanced or comparative analysis:contentReference[oaicite:4]{index=4}. |


| **Name**       | **Domestic SOC & N₂O Source** | **International SOC & N₂O Source** | **Main Assumptions** | **Characteristics** |
|----------------|--------------------------------|-------------------------------------|-----------------------|----------------------|
| **DayCent**    | ✔️ Process-based SOC at daily timestep; paired with COLE for forest aboveground carbon | – | Daily time-step SOC modeling; calibrated for U.S. conditions | High-resolution, process-based SOC modeling for the U.S.; captures daily dynamics of soil carbon and N₂O. |
| **CENTURY**    | ✔️ Parameterized SOC model (inverse modeling) at county/AEZ level; paired with COLE | – | Inverse modeling approach; county/AEZ averages | Provides county- or AEZ-level SOC estimates; less dynamic than DayCent but widely applied in U.S. LCA studies. |
| **AEZ-EF**     | ✔️ Can be applied domestically (with COLE for forest carbon) | ✔️ AEZ-level global EFs for forest, grassland, cropland | Biome-/AEZ-level averages; includes peatland-specific factors (e.g., palm expansion in SE Asia) | Spatially explicit, zone-level factors; consistent across domestic and international use; used by CARB for LCFS. |
| **Winrock**    | – (optional for U.S. if selected instead of process models) | ✔️ Country-/administrative-level EFs for forest, grassland, cropland pasture conversions | (1) Includes CH₄ & N₂O from burning; (2) No HWP carbon storage; (3) Includes foregone sequestration | Empirically derived, globally consistent; often yields higher emissions due to conservative assumptions; aligned with EPA RFS analysis. |
| **Woods Hole** | ✔️ Alternative U.S. biome-level EFs (forest/grassland conversion) | ✔️ Alternative biome-level global EFs | Biome-level averages; includes partial HWP storage assumptions | Biome-scale (e.g., temperate evergreen forest); simpler than Winrock; often used for sensitivity or comparison. |
| **Other / IPCC defaults** | Optional | Optional | IPCC Tier 1 or other published defaults | Provides flexibility for sensitivity or comparative analysis. |



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



