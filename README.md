# Analysis and Optimization of Operator Routing in a Warehouse: Comparing Fixed Policies with Exact and Metaheuristic TSP Algorithms

## 🎓 Master's Thesis in Management Engineering

This repository contains the numerical simulation models and analysis performed for the Master's Thesis in Management Engineering at the Politecnico di Bari. The core area of study is the logistics discipline, focusing specifically on the challenges of internal logistics within a warehouse.

**Candidate:** Alberto Piacquadio
**Academic Year:** 2024-2025

---

## 💡 Overview

Logistics has become a fundamental strategic component in a company's value chain, and inefficiencies in internal flows—such as storage, picking, and material handling—can significantly erode margins and competitiveness. Within this context, the operator routing problem is one of the most critical aspects, directly impacting operational costs and productivity.

This work analyzes and optimizes the phase of **routing a single operator** inside a warehouse by comparing the performance of conventional **fixed policies** (e.g., S-Shape) with advanced **exact and metaheuristic algorithms** based on the Traveling Salesman Problem (TSP). The ultimate goal is to identify the optimal path that minimizes the total travel distance and maximizes efficiency.

### Key Focus Areas:

* **Internal Logistics Criticalities:** Analyzing the traditional and complex interdependencies among batching, scheduling, and routing, which are often treated distinctly leading to sub-optimal global results.
* **Routing Algorithms:** Comparing the performance, robustness, and scalability of different models: **S-Shape (Classic and Centric)**, **TSP Exact (Held-Karp)**, **Tabu Search (TS)**, and **Lin-Kernighan-Helsgaun (LKH)**.
* **Impact of Layout Complexity:** Analyzing algorithm performance across small, medium, and large warehouse layouts.

---

## ⚙️ Methodology and Models

The simulation and comparative analysis were developed using Python across three grid-based warehouse sizes:

| Warehouse Dimensions     | Picking Locations | Layout Feature |
| :-------------------     | :---------------- | :------------- |
| Small ($10 \times 20$)   |      104          | No central cross-aisle |
| Medium ($36 \times 48$)  |      1056         | Includes a central cross-aisle |
| Large ($100 \times 200$) |      12369        | Multiple cross-aisles |

For a robust evaluation, 500 random orders were generated for each size, testing various order batch sizes (from 10 up to 30 picks, and up to 104 picks for detailed analysis of the small warehouse).

### Algorithm Implementation Details:

* **TSP Exact (Held-Karp):** Used only for instances with a very small number of nodes ($N \le 13$) due to its exponential growth in computational time.
* **Metaheuristics (TS and LKH):** These models employ a local search based on the **2-opt swap** operator to find quasi-optimal solutions efficiently, making them scalable for larger instances.

---

## 📈 Key Results

The comparative analysis focused on **Average Distance (m)**, **Variance of Distance**, **Average Runtime (ms)** and **Accuracy (gap %)**.

### Summary of Findings:

1.  **Optimality and Accuracy:** The TSP-based metaheuristics (**Tabu Search** and **LKH**) consistently achieved **quasi-optimal solutions** with an accuracy gap typically less than 1% compared to the theoretical optimum found by TSP Exact (or the best-found heuristic solution). Their distributions were highly concentrated, confirming superior robustness and predictability.
2.  **Performance Trade-off:** The **LKH** algorithm generally provided the **best overall performance**, offering high solution quality with significantly lower average runtime compared to Tabu Search, especially in medium and large warehouse configurations.
3.  **Fixed Policy Performance:** The **S-Shape** policy was proven to be highly **ineffective** in optimizing travel distance (with a gap that could exceed 150% in the largest warehouse), but it remains **unbeatable in terms of runtime** (near $0$ ms).
4.  **S-Shape and Saturation:** A key finding is the inverse relationship between the S-Shape's inefficiency and pick density: as the order batch size approaches the maximum capacity of the warehouse (full saturation), the optimization gap closes significantly (down to 1.92%). This suggests that S-Shape can be competitive with TSP-based algorithms in scenarios where nearly all pick points must be visited, given its superior execution speed.

