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
- `CCLUB_2024_Rev1.xlsm` (macro-enable) saved in your GREET download folder (e.g., **R&D GREET_2024 Rev1**) from the *1_GREET_tutorial*.


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

Follow the inputs **top → bottom** on the **LUC Scenario & Results** sheet, then review the results at the end. Users select input values in the **rose-colored** cells, while **grey** cell cannot be selected or modified. All options are visible in the **yellow** cells in each section.

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
Input 2 allows the user to specify how soil organic carbon (SOC) and nitrous oxide (N₂O) emissions are modeled for both domestic and international LUC. These options combine domestic and international modeling scenarios to determine which datasets and emission factors are used in the calculations.

Here is a summary of the domestic & international emissions modeling scenarios:
| **Name**       | **Domestic SOC & N₂O Source** | **International SOC & N₂O Source** | **Main Assumptions** | **Characteristics** |
|----------------|--------------------------------|-------------------------------------|-----------------------|----------------------|
| **DayCent**    | ✔️ Process-based SOC at daily timestep; paired with COLE for forest aboveground carbon | – | Daily time-step SOC modeling; calibrated for U.S. conditions | High-resolution, process-based SOC modeling for the U.S.; captures daily dynamics of soil carbon and N₂O. |
| **CENTURY**    | ✔️ Parameterized SOC model (inverse modeling) at county/AEZ level; paired with COLE | – | Inverse modeling approach; county/AEZ averages | Provides county- or AEZ-level SOC estimates; less dynamic than DayCent but widely applied in U.S. LCA studies. |
| **AEZ-EF**     | ✔️ Can be applied domestically (with COLE for forest carbon) | ✔️ AEZ-level global EFs for forest, grassland, cropland | Biome-/AEZ-level averages; includes peatland-specific factors (e.g., palm expansion in SE Asia) | Spatially explicit, zone-level factors; consistent across domestic and international use. |
| **Winrock**    | – (optional for U.S. if selected instead of process models) | ✔️ Country-/administrative-level EFs for forest, grassland, cropland pasture conversions | (1) Includes CH₄ & N₂O from burning; (2) No HWP carbon storage; (3) Includes foregone sequestration | Empirically derived, globally consistent; often yields higher emissions due to conservative assumptions; aligned with EPA RFS analysis. |
| **Woods Hole** | ✔️ Alternative U.S. biome-level EFs (forest/grassland conversion) | ✔️ Alternative biome-level global EFs | Biome-level averages; includes partial HWP storage assumptions | Biome-scale (e.g., temperate evergreen forest); simpler than Winrock; often used for sensitivity or comparison. |
| **Other / IPCC defaults** | Optional | Optional | IPCC Tier 1 or other published defaults | Provides flexibility for sensitivity or comparative analysis. |

For this tutorial, we will select the **3 - AEZ-EF option**, since it provides a consistent baseline for both domestic and international SOC and N₂O modeling. Selecting the Input 2 will update the choices in Input 3a, Input 3b, and Input 5 automatically.

**Note**: For more details on domestic & international carbon emissions scenarios, see *Section 3-5* of the **CCLUB User Manual**.

### 2.3 Harvested Wood Product (HWP) Scenario — *Input 7*
Users can select an HWP scenario for Input 4, either using the assumptions of Heath et al. (1996) or assuming all forest aboveground carbon is emitted when forests are converted to biofuel feedstock production.

In this case study, we will select the default **HEATH Scenario**.

### 2.4 Select International Initial Land Clearing - Bimoass Burning — *Input 8*
In Input 8, users can indicate whether to include biomass burning for initial land clearing in international LUC. Answer “No” indicates no burning for all countries, and “Yes” for burning in all international countries only when “CENTURY SOC” or “Woods Hole” is selected in Input 2. If Input 2 selects “Winrock,” then “Yes” indicates burning in countries in which biomass burning is a common practice based on Winrock estimates (Harrison et al. 1996).

In this case study, we will select the **No**, since we select the AEZ-EF option in Input 2, rather than Winrock, CENTURY SOC, or Woods Hole.

### 2.5 Forest Prorating Factor — *Input 9*
Input 9 allows users to adopt adjustments to converted forest lands by selecting “Yes” or to use raw GTAP data by selecting “No.”

In this case study, we will select the default **Yes**.

**Note**: For details on modification of GTAP data for area of converted forest, see *Section 2* of the **CCLUB User Manual**.

### 2.6 Average Approach for domestic SOC and international emissions — *Input 10*
Input 10 allows users to choose an approach for spatial average in both domestic and international LUC factors.

We will select the default **Area Weighted Mean**.

### 2.7 Emissions Amortization Period — *Input 12*
Users can alter the amortization period in Input 12. Use with Caution Since Emissions Factors are Only Valid for 25-35 Year Time Horizon. Choosing values outside that time window may produce inaccurate results.

Use the default **30-year**. 

### 2.8 Summarize all steps:

| **Step** | **Input** | **Operations** |
|----------|-----------|----------------|
| 2.1 | Input 1 – Feedstock-to-Fuel Pathway | Select **ethanol pathway (Corn Ethanol 2011, Stover Ethanol, Switchgrass Ethanol, Miscanthus Ethanol)**. |
| 2.2 | Input 2 – SOC & N₂O Modeling Scenario | Select **3 – AEZ-EF** for consistent domestic & international SOC/N₂O modeling. |
| 2.3 | Input 4 – Harvested Wood Product (HWP) Scenario | Select **HEATH Scenario** (default). |
| 2.4 | Input 8 – International Initial Land Clearing (Biomass Burning) | Select **No**. |
| 2.5 | Input 9 – Forest Prorating Factor | Select **Yes** (default). |
| 2.6 | Input 10 – Average Approach | Select **Area Weighted Mean** (default). |
| 2.7 | Input 12 – Emissions Amortization Period | Select **30 years** (default). |

## Step 3: View the result
Once all inputs are selected, the user can view results within CCLUB as described in the following paragraph. The red-highlighted box in the results section contains the total carbon, N2O & CH4 or total GHG emissions associated with the selected scenario in units of g CO2e/MJ.

**Note**: The sections 'ILUC Emissions - Belowground Crop Biomass C change' and 'Other Indirect Effect Emissions' are available onlt for the pathways of GTAP 2014 and 2017 data.

---



