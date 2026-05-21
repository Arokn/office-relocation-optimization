# Office Relocation Optimization

Optimization of personnel moves during a multi-phase building renovation. The goal is to find the minimum number of moves to go from an initial office configuration to a target final one, across 5 renovation phases, subject to capacity and availability constraints.

---

## Problem

A university building undergoes renovation wing by wing (B → D → C → A). At each phase, one wing is unavailable and its occupants must relocate. Each office holds at most 2 people. The objective is to minimize the total number of moves across all phases while reaching a fixed final configuration.

5 services are involved: Presidency (P), Students Association (S), Optimization (O), Theoretical Computer Science (T), Mathematics (M).

---

## Approaches

| Part | Method | Tool |
|---|---|---|
| Part 1 | Linear Programming + KKT conditions | PuLP |
| Part 2 | Penalized LP with L1 penalty | PuLP |
| Part 3 | Semidefinite Programming + randomized rounding | CVXPY |

---

## Notebook Structure

- **Part 1** — LP formulation with flow conservation, capacity and renovation constraints. Dual problem and KKT conditions. Extended with cohabitation constraints separating Presidency and Students Association by wing.
- **Part 2** — LP extended with an L1 penalty term weighted by lambda to encourage early convergence toward the final allocation. Dual analysis of the penalized problem.
- **Part 3** — SDP relaxation of the binary placement problem. Dimensional reduction from 18 individuals to 12 functional groups to make the problem tractable. Goemans-Williamson randomized rounding to recover an integer solution.

---

## Key Results

| Model | Min moves |
|---|---|
| LP baseline | 30 |
| LP + cohabitation constraints | 31 |
| LP + L1 penalty (lambda=100) | 38 |
| SDP + randomized rounding | non-feasible (violations of unique assignment) |

The SDP rounding does not guarantee feasibility — a repair step (reassigning entities with conflicts to their best available office) would be needed to recover a valid solution.

---

## Dependencies

```bash
pip install pulp cvxpy numpy
```

---

## Run

```bash
git clone https://github.com/your-username/office-relocation-optimization.git
cd renovation-relocation-LP-SDP
jupyter notebook office_relocation_optimization.ipynb
```
