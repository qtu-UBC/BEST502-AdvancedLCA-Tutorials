# ⛽ Fuel Life Cycle Assessment (LCA) Model Tutorial

The Government of Canada’s Fuel Life Cycle Assessment (LCA) Model is a tool that allows users to calculate the life cycle carbon intensity (CI) of fuels and energy sources produced and used in Canada. This tutorial is designed to guide students through the basics of conducting a Fuel LCA in openLCA, using conventional bioethanol as the case study.

**Note**: These tutorial is developed by the [Minister of Environment and Climate Change Canada (2024)](https://www.canada.ca/en/environment-climate-change.html). For the latest updates and documentation, visit the [website](https://www.canada.ca/en/environment-climate-change/services/managing-pollution/fuel-life-cycle-assessment-model.html).


---


## 📺 Step 1: Introductory Videos on openLCA  

Before starting the case study, watch the following videos to become familiar with how the **Government of Canada’s Fuel LCA Model** is implemented in **openLCA**:  

- [**Part 1: Walkthrough of the Model in openLCA**](https://www.youtube.com/watch?v=pamF7GONNXk) **[34.26 min]**. This video provides an overview of the Fuel LCA Model and demonstrates its structure and workflow in the openLCA software.

- [**Part 2: Demonstration of a Carbon Intensity Calculation**](https://www.youtube.com/watch?v=pnod3YNYrro) **[54.13 min]**. This video walks through the process of calculating the carbon intensity (CI) of fuels using the Fuel LCA Model in openLCA.

---

## 🏭 Step 2: Case Study – Conventional Bioethanol Example

Follow the steps below to build and calculate the carbon intensity (CI) of conventional bioethanol using the Fuel LCA Model in openLCA. 

1. **Download and Set Up openLCA**  
   - Install openLCA (v2.0 or higher) from [openLCA.org(https://www.openlca.org/download/).  
   - Download the 'Fuel_LCA_Model_Database_August2024.zip' from the [Website](https://data-donnees.az.ec.gc.ca/data/climate/framework/fuel-life-cycle-assessment-model/English/1-Fuel%20LCA%20Model/Fuel%20LCA%20Model%20(latest%20version)/Fuel%20LCA%20Model%20database?lang=en).  
   - Import the dataset into openLCA.  

2. **Setting up the overall fuel pathway information (optional)**  
   - Follow the guidance of the [tutorial slides](https://github.com/qtu-UBC/BEST502-AdvancedLCA-Tutorials/blob/main/tutorials/FuelLCAModel/02%20-%20CFR%20-%20CI%20Calculation%20Training_Conventional%20Bioethanol%20Example_Nov2024.pdf) to complete the [CFR data worksheet](https://github.com/qtu-UBC/BEST502-AdvancedLCA-Tutorials/blob/main/tutorials/FuelLCAModel/Conventional%20Bioethanol%20Example_CFR%20Data%20Workbook_Nov2024.xlsx).  
   - Provide high-level details such as the identification of the fuel production facility, description of the fuel pathway, the type of fuel(s) produced (e.g., bioethanol), and the reporting period.  

3. **LCA modeling**  
   - Download the [Bioethanol inventory data](https://github.com/qtu-UBC/BEST502-AdvancedLCA-Tutorials/blob/main/tutorials/FuelLCAModel/Bioethanol%20inventory%20data.xlsx).
   - Use the inventory data and the training slides to model the each stage in openLCA, as shown below:

| Process Stage                | Description                                      | Slide Reference |
|-------------------------------|--------------------------------------------------|-----------------|
| Feedstock Production Process and Transportation | Corn (ON/IA) and Wheat (QC) cultivation & transport | Slides 21–24    |
| Bioethanol Production Process | Conversion of feedstock into bioethanol, with inputs (natural gas, electricity, solar, chemicals) and outputs (bioethanol + co-products WDGS/DDGS) | Slides 29–47    |
| Bioethanol Distribution       | Distribution of bioethanol to delivery point and end-user (Leg 1 & Leg 2) | Slides 47–51    |
| Bioethanol Combustion         | End-use combustion of bioethanol at user level | Slide 52        |
       

6. **Calculate Carbon Intensity (CI)**  
   - Create product systems for bioethanol from each feedstock (corn and wheat) - Slide p. 53-61.  
   - Ensure reference flow is set to **1 MJ**.  
   - Run the calculation using the **FuelLCAModelLCIA_AR5 method**.  
   - Record CI results and analyze contributions by process.  

7. **Export the Fuel Pathway**  
   - Export the completed fuel pathway (JSON-LD format) - Slides p. 62.
   - An example result file is here: 'Conventional Bioethanol Example_openLCA_Nov2024.zip' from [database](https://github.com/qtu-UBC/BEST502-AdvancedLCA-Tutorials/tree/main/tutorials/FuelLCAModel/database).  

**Reference materials**:
- [Fuel Life Cycle Assessment Model Website](https://www.canada.ca/en/environment-climate-change/services/managing-pollution/fuel-life-cycle-assessment-model.html)  
  – The official website of the Fuel LCA Model, where can access the Fuel LCA Model Database, Methodology, and User Manual.
- [Fuel Life Cycle Assessment Model User Manual](https://www.canada.ca/en/environment-climate-change/services/managing-pollution/fuel-life-cycle-assessment-model/user-manual.html#toc4)  
  – An official guidance document to help users correctly apply the Fuel LCA Model.

---

## 🎯 Learning Outcomes

By the end of this tutorial, students will:  
- Navigate and build models in **openLCA**.  
- Conduct a **fuel life cycle assessment** using a bioethanol case study.
- Develop skills in interpreting and reporting LCA results.  

---
