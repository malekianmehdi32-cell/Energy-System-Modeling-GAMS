# 🏢 Local Energy System Optimization 

**Course:** Energy Systems Modeling  
**University:** Sharif University of Technology (SUT)[cite: 6]  
**Author:** Erfan Malekian

---

## 📝 Overview
This repository contains a Capacity Expansion and Economic Dispatch model written in GAMS (Linear Programming). The project involves designing an optimal local multi-carrier energy system for a 10-story mountain building[cite: 6]. Initially off-grid, the building can connect to the national electricity and gas networks by paying a one-time subscription fee ($2000 for electricity, $3000 for gas)[cite: 6]. 

The model optimizes the technology mix to meet dynamic diurnal and seasonal demands for electricity, heating, and cooling while minimizing the total annualized cost under various long-term planning horizons and climate policies.

## ⚙️ Technologies Evaluated
The model evaluates the following technologies to meet the building's energy demands[cite: 6]:
*   **Solar PV (Photovoltaic):** Zero-fuel renewable generation[cite: 6].
*   **CHP (Combined Heat and Power):** Natural gas-fueled cogeneration unit with strict thermal-electrical operating boundaries[cite: 6].
*   **Gas Boiler:** Dedicated natural gas heating[cite: 6].
*   **Electric Water Heater (EWH):** Power-to-heat technology[cite: 6].

## 📊 Key Scenarios & Results

### 1. Long-Term Planning (10 & 15-Year Horizons)
Due to GAMS demo limitations, a multi-stage forecasting approach was used to model beyond 7 years[cite: 3].
*   **PV Capacity:** Consistently maxes out at the 100 kW limit across all horizons, proving its high economic viability[cite: 3].
*   **CHP as the Backbone:** CHP serves as the primary base-load provider, stabilizing at an optimal capacity of ~198 kW[cite: 3, 7]. Expanding CHP further is economically inefficient due to excess heat dumping in the summer[cite: 3].
*   **The Heating Bottleneck:** By Year 10, the system reaches its thermal capacity limit. The marginal cost (shadow price) of supplying winter heat rises drastically (reaching 98.7 by year 15), making it the primary system bottleneck[cite: 3]. 

### 2. Technology Exclusion (The Value of CHP)
To calculate the Levelized Avoided Cost of Energy (LCOE), the model was run forcing the CHP capacity to zero (`Cap.fx("CHP") = 0`)[cite: 6, 7].
*   **Base Cost:** $963,926.7[cite: 3]
*   **No-CHP Cost:** $1,116,800.0[cite: 3, 7]
*   **Impact:** Removing CHP increases the total system cost by approximately 16% ($152,873) over a 7-year period[cite: 3]. The system is forced to dramatically increase boiler capacity (to 198.13 kW) and EWH capacity (to 25.34 kW) while grid electricity purchases jump by 256%[cite: 3, 7].

### 3. Energy Efficiency Investment 
We evaluated a hypothetical technology that reduces cooling and heating demand by 20% starting from Year 6[cite: 3, 6].
*   **Findings:** The Net Present Value (NPV) of the total savings from reduced grid gas and electricity purchases from Year 6 to Year 10 is **$35,014**[cite: 3]. This technology should only be adopted if its cost is lower than or equal to this threshold[cite: 3].

### 4. Environmental Policies (Carbon Tax & Emission Caps)
*   **Carbon Tax:** A carbon tax of $84/ton ($80 + ID digit 4) was applied to grid imports[cite: 6]. This penalty increases the total system cost by 56% to **$1,493,611**[cite: 3]. Despite the tax, CHP remains dominant because grid electricity is highly expensive and carries its own carbon penalty[cite: 3].
*   **30% Emission Cap:** Applying a hard constraint to reduce CO2 emissions by 30% renders the model **infeasible**[cite: 3, 6]. The maximum achievable emission reduction without crashing the system is only around 3%[cite: 3].

## 🚀 Repository Structure
*   `modelasli.gms`: The primary GAMS script containing the base LP optimization model.
*   `chpno.gms`: The modified script evaluating the system without CHP capability.
*   `Report.pdf`: The detailed comprehensive technical report containing marginal value analysis and economic breakdowns[cite: 3].

---
*Developed as part of the Energy Systems Modeling curriculum.*
