# Topological Regime Filter for Market Structure Detection

A quant research project that applies **topological data analysis (TDA)** to financial markets using **persistent homology**. This project analyzes how correlations between large-cap stocks evolve over time, and uses that information to **filter trades**, reducing risk exposure during turbulent market regimes.

---

## Project Summary

Using a sliding window over daily log returns of large-cap US stocks (e.g., AAPL, MSFT, AMZN, etc.), we compute correlation matrices to observe how these stocks move together. These correlations are converted to distance matrices and analyzed using persistent homology (via `ripser`) to extract topological features:

- **Betti-1 number**: Counts the number of loops (H1) in the market's correlation structure.
- **Total H1 persistence**: Measures the strength of those loops (more persistent = more dislocated structure).

These metrics are then used as a **filter**: we avoid trading when the market is structurally unstable.

---

## Performance Snapshot

| Metric           | Topological Strategy | Market  |
| ---------------- | -------------------- | ------- |
| **Sharpe Ratio** | 0.670                | 0.802   |
| **Volatility**   | 25.7%                | 27.8%   |
| **Max Drawdown** | -40.36%              | -44.25% |

> The topological strategy had slightly lower returns but significantly reduced drawdowns and volatility, especially during high-risk periods.

---


## Visual Results

### 1. Betti-1 (Number of Loops) Over Time
*Captures fragmentation in the market's internal structure.*
![Betti Plot](images/Betti-1%20(Number%20of%20Loops).png)

---

### 2. Total H₁ Persistence Over Time
*Measures how strong and long-lived those topological features are.*
![Persistence Plot](images/Total%20H%E2%82%81%20Persistence.png)

---

### 3. Cumulative Strategy Performance
*Strategy trades only when Betti-1 ≤ 1 and H₁ persistence < 0.05.*
![Performance Plot](images/Strategy%20Performance.png)

---

## Tools Used

- `yfinance` to fetch stock price data
- `numpy`, `pandas`, `matplotlib` for data manipulation and plotting
- `ripser.py` and `persim` for persistent homology

---

## Repository Structure
.
├── images/                        # Visualizations (Betti-1, Persistence, Strategy Performance)
├── notebooks/                    # Jupyter notebooks for analysis
│   └── topological_filter.ipynb  # Main notebook showing the strategy
├── strategy_analysis.py         # Python script version of the strategy (optional)
├── README.md                     # Project overview and results
├── LICENSE                       # License file (MIT)
└── .gitignore                    # Files to be ignored by Git

