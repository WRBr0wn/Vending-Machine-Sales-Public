# Vending Machine Assortment Optimization
### A "Predict-then-Optimize" Framework for Retail Space Allocation

![Status: Sanitization in Progress](https://img.shields.io/badge/Status-Data_Sanitization_In_Progress-orange)
![Python](https://img.shields.io/badge/Python-3.10%2B-blue)
![Julia](https://img.shields.io/badge/Julia-1.9%2B-purple)

---

## Repository Status: Under Construction
**Please Note:** This project was originally deployed using proprietary sales data from the **University of Minnesota (UMN)** vending fleet. To make this repository public, I am currently performing a full code overhaul to:

1.  **Sanitize Data:** Removing all specific building names and real transaction logs.
2.  **Generate Mock Data:** Creating schema-compliant dummy datasets so the code remains executable without violating privacy agreements.
3.  **Refine Documentation:** Converting academic reporting into open-source documentation.

**The full source code (Python & Julia) will be uploaded shortly.**

---

## Executive Summary
Vending machines are physically constrained retail environments. With limited slots (capacity), every product choice represents an opportunity cost. Traditionally, stocking decisions are made based on human intuition or static historical averages, leading to "squatters" (low-velocity items taking up space) and stockouts of high-demand items.

This project implements a **Predict-then-Optimize** framework to automate assortment optimization. By combining Machine Learning (to predict sales probability) with Integer Programming (to minimize economic regret), this system achieved a **51% reduction in opportunity cost** compared to the status quo.

## How It Works
The system operates in two distinct phases:

### Phase 1: Predictive Engine (Python)
We use historical sales data and location intelligence to predict the "Sales Velocity" of potential products.
* **Technique:** Classification & Regression Trees (CART).
* **Features:** Product Category, Location Type (e.g., "Dorm" vs. "Classroom"), Seasonality, and Price Point.
* **Output:** A probabilistic score ($Y_{hat}$) indicating the likelihood of a product being a "High Seller."

### Phase 2: Prescriptive Engine (Julia)
Using the output from the predictive model, we solve a Knapsack-style optimization problem to generate the optimal machine layout.
* **Technique:** Mixed-Integer Linear Programming (MILP) using `JuMP` and `GLPK`.
* **Objective Function:** Minimize **Economic Regret**, defined as the sum of:
    * **Slot Loss (Type I Error):** The opportunity cost of wasting a slot on a "Poor-Selling" item.
    * **Sales Loss (Type II Error):** The realized revenue loss from failing to stock a "High-Selling" item.

## Project Structure (Coming Soon)
The repository will be organized into two main workflows to demonstrate the evolution of the project:

```text
├── phase_1_poc/           # Proof of Concept (Kaggle Data)
│   ├── predictive_poc.ipynb
│   └── prescriptive_poc.ipynb
│
├── phase_2_deployment/    # Full Scale Application (Mock UMN Data)
│   ├── config.py
│   ├── generate_mock_data.py
│   ├── predictive_engine.ipynb
│   └── prescriptive_optimizer.ipynb (Julia)
│
└── reports/               # Performance Analysis
    └── optimization_results.md
```

## Results & Validation
During the pilot analysis of 239 machines across the UMN campus:
* **Financial Impact:** The optimized assortments demonstrated a projected **23.8% to 51% improvement** in revenue efficiency per machine.
* **Strategic Shift:** The model successfully identified shifting demand patterns, prioritizing coffee products in academic buildings during winter months while prioritizing energy drinks in recreational centers.

## Technologies Used
* **Python:** Pandas, Scikit-Learn (Decision Trees), Matplotlib.
* **Julia:** JuMP (Modeling Language), GLPK (Solver), JSON (Interoperability).

---
*Created by Wyatt Brown & Drew Johnson. This project served as the final project for the IE 5533 course at the University of Minnesota.*
