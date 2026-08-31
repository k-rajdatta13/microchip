# Robust Microchip Production Planning

This repository contains the implementation of a **robust optimization model** for microchip production under uncertainty in copper consumption. The project explores different uncertainty sets (box, budgeted/cardinality, and ball/ellipsoidal) and demonstrates how to obtain production plans that are resilient to variations in raw material requirements.

---

## Problem Description

The company **BIM (Best International Machines)** produces two types of microchips:

- **Logic chips:** 1 g silicon, 1 g plastic, 4 g copper  
- **Memory chips:** 1 g germanium, 1 g plastic, 2 g copper  

Each chip generates profit:

- Logic chip: €12  
- Memory chip: €9  

Available raw materials:

- Silicon: 1000 g  
- Germanium: 1500 g  
- Plastic: 1750 g  
- Copper: 4800 g  

The goal is to **maximize profit** while respecting raw material availability. Copper consumption may vary due to external factors, motivating **robust optimization**.

---

## Objectives

- Formulate the **nominal LP** for maximizing microchip profit.  
- Implement **robust optimization** using:
  - Box uncertainty (empirical bounds)  
  - Budgeted/cardinality uncertainty (limited number of deviations)  
  - Ball (ellipsoidal) uncertainty  
- Analyze how uncertainty impacts the optimal production plan.

---

## Methodology

1. **Nominal Model:**  
   - Implemented using **AMPL + Python**, solved with the `highs` solver.  

2. **Box Uncertainty:**  
   - Empirical bounds derived from 2000 simulated copper consumption scenarios.  
   - Linear duality used to reformulate robust constraints.  

3. **Budgeted Uncertainty:**  
   - Limited number of deviations (\(\Gamma\)) modeled.  
   - Solved using both **robust counterpart** and **adversarial scenario generation** to find worst-case scenarios.  

4. **Ball (Ellipsoidal) Uncertainty:**  
   - Reformulated as a **second-order cone program (SOCP)**.  
   - Captures continuous deviations in copper consumption within a radius \(r\).  
   - Solved using nonlinear solvers (`ipopt`) and mixed-integer conic solvers (`bonmin`, `cplex`, `gurobi`).  

---

## Key Features

- Simulation of material uncertainty to define realistic bounds.  
- Robust counterpart formulations for different uncertainty sets.  
- Adversarial scenario generation for worst-case robustness.  
- Visualization of optimal production plan changes under varying uncertainty.  

---

## Results

- Nominal LP solution maximizes profit without considering variability.  
- Robust solutions **ensure production feasibility under uncertainty**, slightly reducing profit but improving resilience.  
- Ball uncertainty formulation captures ellipsoidal variations in copper consumption efficiently.  

*(Optional: Include example optimal values, e.g., `Profit ~ €17,700 for nominal, €17,586 under robust box uncertainty`.)*  

---

## Requirements

- Python ≥ 3.8  
- AMPL Python API (`amplpy`)  
- Solvers: `highs` (LP/MILP), `ipopt` (SOCP), optional: `bonmin`, `cplex`, `gurobi`  
