# Comparative Analysis of Particle Swarm Optimization and Genetic Algorithm for Solving Vehicle Routing Problem with Time Windows and Capacity Constraints

This repository contains Python/Jupyter Notebook implementations of **Particle Swarm Optimization (PSO)** and **Genetic Algorithm (GA)** to solve a **Vehicle Routing Problem with Time Windows (VRPTW)** and capacity constraints, based on a **real footwear distribution case in Dhaka, Bangladesh**.

The goal is to design cost-efficient vehicle routes that:
- Respect **vehicle capacity**
- Respect **customer time windows**
- Minimize **total logistics cost** (fixed vehicle cost + transport cost + penalties)

---

## 📂 Repository Contents

- `PSO_Code_Optimized.ipynb`  
  Implementation of **Particle Swarm Optimization** for VRPTW.
  - Encodes customer sequences as particles
  - Uses a decoding heuristic to form feasible routes
  - Computes total cost (fixed + distance-based + penalties)
  - Visualizes optimized routes

- `Optimization_VRP_Genetic_Algorithm_.ipynb`  
  Implementation of **Genetic Algorithm** for the same VRPTW instance.
  - Chromosomes represent customer visit permutations
  - Uses selection, crossover, and mutation operators
  - Applies penalty-based fitness for time-window and capacity violations
  - Visualizes resulting routes


---

## 🚚 Problem Overview

We consider a **single-depot VRPTW**:

- **Depot**: 1 central warehouse
- **Customers**: 24 retail outlets in Dhaka
- **Fleet**: 5 identical vehicles
- **Vehicle capacity**: e.g., 1200 units per vehicle
- **Planning horizon**: 06:00–21:00 (time windows in minutes)
- **Cost structure (example as used in code)**:
  - Fixed cost per vehicle, e.g., 2000 BDT
  - Transport cost per km, e.g., 5 BDT/km
  - Penalty costs for:
    - Time-window violations (late service)
    - Capacity violations (overload)

**Objective**

> Minimize  
> **Total Logistics Cost = Fixed Vehicle Cost + Transport Cost + Penalty Cost**  
> subject to:
> - Each customer is visited exactly once  
> - Vehicle capacity is not exceeded  
> - Service starts within the specified time windows  

---

## 🧠 Algorithms

### 1️⃣ Particle Swarm Optimization (PSO)

- Each **particle** is a candidate solution (permutation of customers).
- A **decoding heuristic** splits the permutation into vehicle routes respecting:
  - Capacity constraints
  - Time-window constraints (with penalties if violated)
- The **fitness function**:
  - Fixed cost per used vehicle
  - Distance-based transport cost
  - Penalty cost for time-window and capacity violations
- PSO updates particle positions/velocities based on:
  - Personal best position
  - Global best position

You can tune:
- Number of particles
- Number of iterations
- Inertia weight, cognitive/social coefficients
- Penalty coefficients

### 2️⃣ Genetic Algorithm (GA)

- Each **chromosome** is a permutation of customer IDs.
- A route-building heuristic converts a chromosome into multiple vehicle routes.
- **Operators**:
  - Selection: roulette-wheel or fitness-proportional
  - Crossover: order/position-preserving crossover for permutations
  - Mutation: swap and inversion to maintain diversity
- Fitness = total cost (fixed + transport + penalties)

You can tune:
- Population size
- Number of generations
- Crossover probability
- Mutation probability
- Penalty weights

---

## 📊 Results (High-Level Summary)

On the footwear distribution dataset used in this project:

- **PSO**:
  - Found lower total logistics cost
  - Achieved **zero** time-window penalty in the best solution
  - Converged faster (stabilized earlier in iterations)
  - Produced more balanced loads across vehicles

- **GA**:
  - Higher total cost for the same instance
  - Some time-window violations (non-zero penalty)
  - Longer routes on average and less balanced vehicle utilization

> In this case study, PSO outperforms GA in both **cost-efficiency** and **time-window compliance**, making it more suitable for highly constrained, penalty-heavy urban routing scenarios.

---

### Example: PSO vs GA Route Visualizations

```markdown
![PSO Optimized Route](c:\Users\ASUS\comparative-analysis-of-PSO-and-GA\images\PSO Optimized Route.png)
*Figure 1: PSO-optimized vehicle routes*

![GA Optimized Route](c:\Users\ASUS\comparative-analysis-of-PSO-and-GA\images\GA Optimized Route.png)
*Figure 2: GA-optimized vehicle routes*
