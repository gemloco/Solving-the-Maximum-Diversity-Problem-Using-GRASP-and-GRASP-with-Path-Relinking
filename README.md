# Solving the Maximum Diversity Problem Using GRASP and GRASP with Path Relinking

This repository contains the mathematical formulation, **Python** implementation, and computational evaluation of metaheuristic approaches applied to the **Maximum Diversity Problem (MDP)**, an NP-hard combinatorial optimization challenge with practical applications in portfolio selection, facility location, and genetic engineering[cite: 64, 65].

---

## 📌 Project Overview & Methodology

1. **Greedy Randomized Adaptive Search Procedure (GRASP):**
   - **Construction Phase:** Feasible solutions are built incrementally by evaluating the marginal contribution of unselected elements using $c(e) := \sum_{s \in S} \text{dist}(e,s)$[cite: 65]. Candidate elements are chosen adaptively from a Restricted Candidate List (RCL) regulated by a randomness threshold parameter $\alpha \in [0,1]$[cite: 65, 66].
   - **Local Search Phase:** Neighborhood exploration based on 1-to-1 swap operations ($S' := (S \setminus \{s\}) \cup \{e\}$), iteratively executing improving moves until a local optimum is reached[cite: 66].

2. **Intensification via Path Relinking (GRASP+PR):**
   - **Elite Set Management ($E$):** Maintains a fixed-size pool of diverse, high-quality solutions obtained across GRASP iterations, preventing duplicates and keeping them sorted by objective value[cite: 66, 68].
   - **Path Relinking Procedure:** Explores trajectory paths between pairs of elite solutions (initiating solution $S_I$ and guiding solution $S_G$) by greedily swapping elements between $A := S_G \setminus S_I$ and $B := S_I \setminus S_G$ to uncover superior local optima[cite: 67].

3. **Hyperparameter Calibration:**
   - Numerical sensitivity evaluation across 15 benchmark problem instances under a fixed pseudo-random seed[cite: 68].
   - Systematic exploration of $\alpha \in \{0.1, 0.2, \ldots, 0.9\}$ and elite pool sizes $\vert{}E\vert{} \in \{5, 10, 15\}$, calibrating $\alpha = 0.4$ and $\vert{}E\vert{} = 10$ to strike an effective balance between greediness, population diversity, and computational overhead[cite: 68].

4. **Comparative Analysis & Experimental Results:**
   - Performance benchmark comparing standard GRASP and GRASP+PR on small (100 elements) and large (500 elements) instances under strict computational runtime limits (30s and 60s)[cite: 68, 69, 70].
   - Algorithmic analysis of convergence and computational bottlenecks: basic GRASP delivers competitive solutions rapidly on smaller instances, whereas GRASP+PR requires extended runtimes to adequately populate the elite pool and complete relinking trajectories on larger instances[cite: 70].

---

## 📂 Repository Structure

- `instance.py`: Parser and data structure for problem instances and distance matrices[cite: 67].
- `solution.py`: Data structure representing candidate partial and complete solutions[cite: 67].
- `cgrasp.py`: Randomized constructive heuristic module (RCL construction)[cite: 67].
- `lsbestimp.py`: Local search
