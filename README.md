# Quant Finance Lab

**Quant Finance Lab** is a personal research and development project exploring the mathematics behind quantitative finance through programming, probability theory, and computational experiments.

The goal is to build a strong mathematical understanding of financial models, implement them in Python, and investigate their behaviour using simulation and statistical analysis.

---

## Project 1 — Stochastic Analytics Simulation (SAS)

### A Monte Carlo Study of Random Trading Outcomes

**Stochastic Analytics Simulation (SAS)** is a Python-based mathematical modelling project that investigates how uncertain trading outcomes affect portfolio capital over repeated trades.

Suppose we simulate 1,000 or 10,000 independent trading experiments. Each experiment consists of a specified number of trades, with every trade producing either a gain or a loss according to predefined probabilistic assumptions.

By analysing the final balance of every experiment, SAS investigates not only the average outcome but also the distribution of possible outcomes and the probability of finishing below the initial capital.

### Central Research Question

> How do win probability, winning return, losing return, initial capital, and the number of trades influence the distribution of final portfolio balances and the probability of a net loss?

## Research Objectives

- Model random trading outcomes using probability theory.
- Investigate the effect of configurable win probabilities and per-trade returns.
- Simulate multiple independent trading paths using Monte Carlo methods.
- Analyse the distribution of final balances using histograms.
- Estimate the probability of reaching different capital targets.
- Calculate the proportion of simulated experiments ending below the initial balance.
- Compare summary statistics to understand the spread and shape of simulated outcomes.

## Mathematical Framework

### 1. Random Trade Returns

Each trade has two possible outcomes in the current model.

\[
R_t =
\begin{cases}
r_w & \text{with probability }p\\
-r_l & \text{with probability }1-p
\end{cases}
\]

Where:

- \(R_t\) = fractional return on trade \(t\)
- \(p\) = probability of a winning trade
- \(1-p\) = probability of a losing trade
- \(r_w\) = fractional return from a winning trade
- \(r_l\) = magnitude of the fractional loss

The win probability and returns are model inputs. They are not assumed to represent actual market probabilities.

### 2. Portfolio Capital Evolution

Let \(B_0\) denote the initial balance. The balance evolves after each trade according to:

\[
B_t=B_{t-1}(1+R_t)
\]

After \(n\) trades:

\[
B_n=B_0\prod_{t=1}^{n}(1+R_t)
\]

This multiplicative model represents percentage gains and losses applied to the current balance.

### 3. Monte Carlo Simulation

The model repeats the trading process across \(M\) independent experiments, producing final balances:

\[
B_n^{(1)},B_n^{(2)},\ldots,B_n^{(M)}
\]

The collection of final balances forms an empirical distribution that can be analysed statistically.

### 4. Probability of Finishing Below Initial Capital

The estimated probability of a net loss is:

\[
\widehat{P}(B_n<B_0)=
\frac{1}{M}\sum_{i=1}^{M}
\mathbf{1}\left(B_n^{(i)}<B_0\right)
\]

Here, \(\mathbf{1}(\cdot)\) equals 1 when the condition is true and 0 otherwise.

This estimates the proportion of simulated experiments whose final balance is below their initial balance.

## Simulation Versions

| Version | Description |
|---|---|
| v0.0.1 | Initial model with fixed simulation parameters |
| v0.0.2 | Configurable initial balance, win probability, win return, loss return, experiment count, trades per experiment, and target threshold spacing |

Version 0.0.2 is the more flexible version for investigating different model assumptions.

## Statistical Analysis

SAS calculates several statistics to help interpret the simulation results.

| Metric | Purpose |
|---|---|
| Mean final balance | Measures the average ending balance |
| Median final balance | Identifies the middle final-balance outcome |
| Minimum and maximum | Show the lowest and highest observed outcomes |
| Standard deviation | Measures the spread of final balances around the mean |
| Experiments below initial capital | Counts simulated paths that finish below their starting balance |
| Estimated probability of a net loss | Measures the proportion of paths finishing below their starting balance |
| Target success rate | Measures the proportion of paths reaching or exceeding a specified balance |

The mean and median provide complementary information. A difference between them can suggest a skewed distribution, which should be examined using the histogram rather than inferred from those statistics alone.

## Visualisation

The current implementation generates two graphs.

**1. Distribution of Final Balances**

A histogram displays how simulated final balances are distributed across experiments. It helps reveal concentration, spread, skewness, and variation between outcomes.

**2. Success Rate vs Target Balance**

A line graph displays the proportion of simulated experiments reaching each specified capital target. It illustrates how the estimated probability of reaching a target changes as the target increases.

Both graphs describe the simulated model, not a forecast of actual market performance.

## Technology Stack

- **Python** — simulation logic and calculations
- **`random`** — generation of random trade outcomes
- **`statistics`** — calculation of descriptive statistics
- **Matplotlib** — graphical visualisation of simulation results

## Getting Started

### Prerequisites

- Python 3
- Matplotlib

Install Matplotlib if it is not already installed:

```bash
python -m pip install matplotlib
```

### Run the configurable simulation

Clone the repository:

```bash
git clone https://github.com/manishsai-rv/quant-finance-lab.git
cd quant-finance-lab
```

Run version 0.0.2:

```bash
python stochastic_analytics_simulation/stochastic_analytics_simulation_v0.0.2.py
```

The program prompts for the simulation parameters, executes the experiments, prints summary statistics, and displays the graphs.

On some systems, the Python executable may be called `python3` instead of `python`.

## Repository Structure

```text
quant-finance-lab/
├── README.md
└── stochastic_analytics_simulation/
    ├── stochastic_analytics_simulation_v0.0.1.py
    └── stochastic_analytics_simulation_v0.0.2.py
```

## Model Assumptions and Limitations

The current model is intentionally simplified to make the mathematical behaviour easier to investigate.

- Each trade is generated independently using a fixed win probability.
- Winning and losing trades use fixed percentage returns.
- Returns are applied multiplicatively to the current balance.
- The model does not use historical market data to estimate its parameters.
- Transaction costs, commissions, slippage, taxes, and execution constraints are not included.
- The model does not account for changing market conditions or dependencies between consecutive trades.
- The simulated outcomes depend on the selected assumptions and random outcomes.

A simulated probability is an estimate based on a finite number of experiments. In particular, observing zero successful paths at a target does not prove that the true probability of reaching that target is zero.

The model is an educational and mathematical research tool. It does not establish that a real trading strategy has a profitable edge or predict future market returns.

## Future Research Directions

Potential extensions include:

- Theoretical validation of simulated results.
- More detailed downside-risk and drawdown analysis.
- Analysis of how the number of experiments affects estimation uncertainty.
- Transaction costs and alternative return assumptions.
- Alternative stochastic models and dependent trade outcomes.
- Portfolio optimization as a separate mathematical module, if developed.

These are possible future extensions, not features claimed to be implemented in the current version.

## Conclusion

Stochastic Analytics Simulation explores how probability, compounding, and randomness interact to produce a distribution of possible portfolio outcomes.

By combining mathematical modelling with computational experimentation, SAS aims to move beyond a single simulated result and investigate the uncertainty surrounding many possible outcomes.

**The objective is to understand the mathematics behind the distribution—not to assume that randomness guarantees profit.**

---

*Repository: Quant Finance Lab*  
*Project: Stochastic Analytics Simulation (SAS)*  
*Status: Experimental mathematical modelling and development*
