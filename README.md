# Travelling Salesman Problem 
Francesco Liaci - s349552

This project solves the **Travelling Salesman Problem (TSP)** using **evolutionary algorithms** together with **local search** and **adaptive parameters**, balancing between **exploration** and **exploitation** 

___
### Representation
- **Permutation encoding** of cities (each tour is a valid permutation) 
- Fitness = total tour distance (closed loop) using numpy

### Population Initialization
- Random permutations of all cities
- Population sorted by fitness (best individual always first)

### Selection Strategy
- **Tournament selection** as default:  
  - `k` controls selective pressure (higher `k` → faster convergence, lower diversity)
- **Rank-based selection** also available 

### Operators
- **Crossover:** *Order Crossover (OX)* and *Inver-Over* (better for symmetric TSP)
- **Mutation:** three operators for diversity:
  - Swap (exchange two cities)
  - Insertion (move a city somewhere else)
  - Inversion (reverse a segment, more effective for symmetric TSP)

### Local Search
- additional local search (like hill climbing) for fine-tuning best individuals
- it's very heavy computationally (hence applied only on a fraction of offspring or after stagnation)

### Evolution Strategies
1. **Steady-State:** replaces worst individual only if new one is better 
2. **Generational:** replaces the whole population (+ some elitism) 
3. **Hybrid (v2):** first produces a batch of offsprings, before adding to the population:
   - elitism (preserve top individuals)
   - adaptive mutation rate and tournament size (k)
   - some 2-opt local search
   - stagnation for early stoppage

### Adaptive Parameters
- Mutation rate and tournament size `k` adjust automatically:
  - No improvement -> more diversity 
  - Improvement -> more exploitation 

---

## Best Results Summary

| Instance | 10 cities | 20 cities | 50 cities | 100 cities | 200 cities | 500 cities | 1000 cities |
|:----------|-----------:|-----------:|-----------:|------------:|------------:|------------:|-------------:|
| **g**     | 1497.66 | 1755.51 | 2668.19 | 4043.70 | 5917.32 | 10173.91 | 20819.52 |
| **r1**    | 184.27  | 337.29  | 661.50  | 1143.91 | 2235.16 | 7266.88  | 13846.90 |
| **r2**    | -411.70 | -808.97 | -2128.65 | -4358.97 | -8442.08 | -19231.07 | -38825.75 |

---

### test problem 

| Instance | Best Fitness |
|:----------|-------------:|
| **test_problem** | 2823.79 |

---

> **Note:**   
> All results of fitness values found using the **hybrid_v2** evolutionary algorithm that seems to be the best one 


