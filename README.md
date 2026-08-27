# Forex-Arbitrage

Forex-Arbitrage is a Python-based project for detecting arbitrage opportunities in the foreign exchange (Forex) market using the **Bellman-Ford algorithm**. The system models currencies as a directed weighted graph, converts exchange rates into logarithmic edge weights, and identifies negative-weight cycles representing profitable arbitrage opportunities.

## Key Features

- **Graph-based detection**: Models currencies as nodes and exchange rates as directed edges
- **Bellman-Ford algorithm**: Finds negative-weight cycles indicating arbitrage opportunities
- **Realistic bid/ask spread simulation**: Applies configurable spread to account for transaction costs
- **Configurable profit threshold**: Filters out negligible arbitrage opportunities below a minimum profit level

## Setup

1. Clone the repository:
   ```bash
   git clone https://github.com/hsavthegreat/Forex-Arbitrage.git
   cd Forex-Arbitrage
   ```

2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

3. Configure API key:
   ```bash
   cp .env.example .env
   # Edit .env and add your Polygon.io API key
   ```

## Usage

Run the notebooks in order:
1. `Data Extraction.ipynb` — Fetch intraday forex data from Polygon.io
2. `build.ipynb` — Build graphs and detect arbitrage cycles using Bellman-Ford
3. `results.ipynb` — Analyze and visualize results

## Configuration

Key parameters in `build.ipynb`:

- `MIN_PROFIT_MULTIPLIER = 1.0001` — Minimum profit multiplier to consider a cycle viable (0.01% after spread/fees)
- `SPREAD_BPS = 5` — Simulated bid/ask spread in basis points (5 bps = 0.05% per leg, conservative for major pairs)

## Limitations & Assumptions

- **Data source**: Uses Polygon.io aggregates endpoint (midpoint/close prices), not live bid/ask quotes
- **Spread simulation**: Applies a fixed symmetric spread (5 bps) to all pairs; real spreads vary by pair and time
- **No fees/commissions**: Does not model broker commissions, slippage, or latency
- **Static graph per minute**: Assumes all trades execute at the same timestamp; real execution takes time
- **Triangular arbitrage only**: Detects cycles of any length, but practical execution favors 3-4 leg cycles

## Project Structure

- `Data/` — Raw forex CSV files (per day)
- `Arbitrage_Cycles/` — Detected arbitrage cycles per day
- `Results/` — Output visualizations and summary CSV
- `Forex_Arbitrage_Day_Wise/` — Alternative pipeline with broader currency set