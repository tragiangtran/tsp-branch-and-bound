# Traveling Salesperson Problem (TSP) – Branch and Bound

This project was developed to model and solve optimization problems in logistics and route planning.

---

## Problem Overview
The Traveling Salesperson Problem (TSP): given a set of cities and the distances between each pair, the objective is to find the shortest possible route that visits each city exactly once and returns to the origin city.

---

## Algorithmic Approach

### 1. Lower Bound Calculation 
In any valid TSP tour, every vertex must be incident to exactly two edges (degree = 2). A global lower bound can be established by considering the two smallest incident edges for each node and dividing the total sum by 2 (as each edge connects two vertices):

$$\text{Lower Bound} = \frac{1}{2} \sum_{v \in V} (\text{weight of edge}_1(v) + \text{weight of edge}_2(v))$$

For a partial path (chosen_path):
- **Internal path nodes:** The two incident edges are completely fixed.
- **End nodes (first & last):** One incident edge is fixed, the second is chosen as the minimum-weight available edge among remaining neighbours.
- **Unvisited nodes:** The lower bound is bounded by the sum of their two smallest incident edges.

### 2. Branch and Bound 
- **Priority Queue (heapq):** Employs priority-based expansion to evaluate partial paths with the lowest lower bounds first.
- **Cycle Detection (BFS):** Utilizes BFS to prevent premature cycle formation before all vertices are visited.
- **Pruning:** If the lower bound of an active branch meets or exceeds the current minimum tour distance, the entire sub-tree is pruned from search space.
