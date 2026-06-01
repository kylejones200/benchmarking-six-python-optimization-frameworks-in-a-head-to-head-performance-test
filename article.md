---
author: "Kyle Jones"
date_published: "August 8, 2025"
date_exported_from_medium: "November 10, 2025"
canonical_link: "https://medium.com/@kyle-t-jones/benchmarking-six-python-optimization-frameworks-in-a-head-to-head-performance-test-4836c61a65a1"
---

# Benchmarking Six Python Optimization Frameworks in a Head-to-Head Performance Test Linear programming is used throughtout operational decision-making, from
supply chains to finance. A well-formulated linear model can cut...

### Benchmarking Six Python Optimization Frameworks in a Head-to-Head Performance Test
Linear programming is used throughtout operational decision-making, from supply chains to finance. A well-formulated linear model can cut costs, optimize schedules, and balance competing constraints. I wrote another article about different solvers but wanted to expand that to include more (and newer) libraries.

I built a benchmark problem and running it across six modern Python optimization stacks: Python-MIP, PuLP, PyOptInterface, Pyomo, CVXPY, and PyOFrame. The goal was to keep everything fair: the same data, the same constraints, and the same objective, run in the same environment. The only variable was the library and solver combination.

The test problem came from a simplified supply chain model for crude oil inventory management. We had:

- Multiple sources shipping to storage tanks over a series of months.
- Per-source shipping costs.
- Tank capacities, starting inventories, and monthly demand.
- Maximum supply constraints by source and month.
- The objective: minimize total shipping cost while meeting demand and respecting capacity limits.

Every library solved exactly this model. I measured runtime (seconds), peak memory usage (KB), and objective value (the optimal cost, to confirm correctness).

All solvers reached the same optimal cost of 17,972,000, confirming that the models were equivalent.

### Python-MIP + CBC
Python-MIP offers a direct, modern API for linear and mixed-integer programming, with CBC and other solvers under the hood. In our test, it was the fastest of the bunch --- blazing through in 0.0228 seconds with minimal memory use. Its API is straightforward, making it a strong choice for those who want speed and simplicity.

### PuLP + CBC
PuLP has been a Python LP staple for years, with a high-level, readable model definition style. It posted 0.0283 seconds runtime, just a fraction slower than Python-MIP, and similarly light on memory. If readability and a well-established user base matter, PuLP remains a safe bet.

### PyOptInterface + HiGHS
PyOptInterface (POI) is newer, designed for a clean, solver-agnostic interface. Paired with the HiGHS solver, it hit 0.0325 seconds --- very close to the leaders. The API feels low-level but precise, appealing to those who value explicit control over every modeling detail.

### Pyomo (CBC/HiGHS/GLPK)
Pyomo is a heavyweight: it supports algebraic modeling across linear, nonlinear, and stochastic problems. That flexibility comes at a cost --- 0.0549 seconds runtime and modestly higher memory usage. For larger or more complex models, Pyomo's feature depth may outweigh the slight speed penalty.

### CVXPY + ECOS/OSQP
CVXPY focuses on convex optimization, offering a declarative, math-first modeling style. It took 0.1263 seconds here, the slowest in our group, and used more memory. While not the top performer on pure LPs, CVXPY shines when you need to move beyond linear constraints into more general convex problems.

### PyOFrame + HiGHS
PyOFrame is an emerging high-level modeling framework. It ran in 0.2787 seconds, last in this set, though still well under a second. Its expressive, dataframe-like model definition will appeal to those coming from a data science background, even if speed isn't its primary advantage.

### The Results
All libraries found the same solution, so the real differences were in speed and resource use. Python-MIP and PuLP were essentially neck-and-neck for top runtime honors, with PyOptInterface not far behind. Pyomo was slower but still very usable for small to medium problems. CVXPY and PyOFrame trailed in raw speed but bring other strengths to the table.


For small to medium LPs where speed matters, Python-MIP, PuLP, and PyOptInterface are standouts. For large-scale or more complex modeling, Pyomo offers unmatched flexibility. If you're in the convex optimization world, CVXPY is the right tool. And for those who prefer data-table-style modeling, PyOFrame is worth watching as it matures.

For LP, there is no one-size-fits-all winner. The best library depends on your problem scale, solver access, and personal modeling style. But with this benchmark, you have a clearer map of the trade-offs.
