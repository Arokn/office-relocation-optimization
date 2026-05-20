# Office Relocation Optimization

Optimization of personnel moves during a multi-phase building renovation, modeled and solved as part of a Mathematics of Data Science course (M1, Dauphine-PSL).

The problem: given an initial office configuration and a target final one, find the minimum number of moves across 5 renovation phases, subject to capacity and renovation constraints.

---

## Problem

A university building undergoes renovation phase by phase (wings B → D → C → A). At each phase, one wing is unavailable. The goal is to move personnel from an initial configuration to a target final one while minimizing total moves, with at most 2 people per office at all times.

---

## Approaches

| Part | Method | Tool |
|---|---|---|
| Part 1 | Linear Programming relaxation + KKT conditions | PuLP |
| Part 2 | Penalized LP with L1 penalty (lambda = 100) | PuLP |
| Part 3 | Semidefinite Programming relaxation + randomized rounding | CVXPY |

---

## Notebook Structure

- **Part 1** — LP formulation (flow conservation, capacity, renovation constraints), dual problem, KKT conditions, cohabitation constraints between Presidency and Students association
- **Part 2** — LP extended with an L1 penalty term to encourage early convergence toward the final allocation
- **Part 3** — SDP relaxation of the binary placement problem, Goemans-Williamson randomized rounding to recover an integer solution

---

## Key Results

- Minimum moves without extra constraints: **30**
- With cohabitation constraints (Q3): **31** (+1 move)
- With L1 penalty lambda=100 (Q5): **38** (+7 moves, converges faster to final state)
- SDP randomized rounding: produces an integer solution but does not guarantee feasibility (some entities end up with no office or multiple offices)

---

## Dependencies

```bash
pip install pulp cvxpy numpy
```

---

## Run

```bash
git clone https://github.com/your-username/office-relocation-optimization.git
cd office-relocation-optimization
jupyter notebook office_relocation_optimization.ipynb
```
