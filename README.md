# Benchmarking Six Python Optimization Frameworks in a Head to Head Performance Test

Published: 2025-08-08
Medium: [https://medium.com/@kyle-t-jones/benchmarking-six-python-optimization-frameworks-in-a-head-to-head-performance-test-4836c61a65a1](https://medium.com/@kyle-t-jones/benchmarking-six-python-optimization-frameworks-in-a-head-to-head-performance-test-4836c61a65a1)

## Business context

Linear programming is used throughtout operational decision-making, from supply chains to finance. A well-formulated linear model can cut costs, optimize schedules, and balance competing constraints. I wrote another article about different solvers but wanted to expand that to include more (and newer) libraries.

I built a benchmark problem and running it across six modern Python optimization stacks: Python-MIP, PuLP, PyOptInterface, Pyomo, CVXPY, and PyOFrame. The goal was to keep everything fair: the same data, the same constraints, and the same objective, run in the same environment. The only variable was the library and solver combination.

The test problem is a simplified **crude-oil supply LP**: sources, tanks, monthly demand, capacities, and shipping costs—minimize cost while meeting demand.

## About

Place the code for this article in this repository.
The original article export is saved as `article.md`.

## Files

Add your `.ipynb`, `.py`, `.yaml`, `.js`, `.ts`, or other project files here.

Run the benchmark: `uv sync && uv run python main.py` (writes `benchmark_results.csv` and timing plots).

## Disclaimer

Educational/demo code only. Not financial, safety, or engineering advice. Use at your own risk. Verify results independently before any production or operational use.

## License

MIT — see [LICENSE](LICENSE).