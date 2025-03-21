# Finance Simulation Library

A comprehensive Python library for simulating and analyzing financial instruments, including stock prices, options, and portfolios.

## Features

- **Stock Price Simulation**: Generate realistic stock price paths using Geometric Brownian Motion (GBM)
- **Growth Models**: Flexible framework for incorporating various growth models into price simulations
- **Volatility Analysis**: Calculate historical volatility and other key market metrics
- **Financial Data Fetching**: Easily obtain historical price data, risk-free rates, and more
- **Visualization Tools**: Create beautiful, informative plots of simulation results
- **Command-Line Interface**: Run simulations directly from the terminal
- **Extensible Architecture**: Add your own models and strategies with the base classes provided

## Installation

### Requirements

- Python 3.7 or higher
- Dependencies listed in `requirements.txt`

### Using Virtual Environment (Recommended)

```bash
# Create and activate a virtual environment
python3 -m venv .venv
source .venv/bin/activate  # On Windows, use: .venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Install the package in development mode
pip install -e .
```

### Install from source

```bash
# Clone the repository
git clone https://github.com/your-username/financial_sim_library.git
cd financial_sim_library

# Install dependencies
pip install -r requirements.txt

# Install the package in development mode
pip install -e .
```

## Quick Start

### Stock Price Simulation with Growth Models

```python
from financial_sim_library.stock_simulator.models.gbm import GBMModel
from financial_sim_library.stock_simulator.models.growth_models import (
    FixedGrowthModel,
    PowerLawGrowthModel,
    ExogenousGrowthModel,
    CompositeGrowthModel
)
from financial_sim_library.visualization.price_plots import plot_price_simulations

# Create a GBM model with fixed growth
model = GBMModel(
    ticker="AAPL",
    growth_model=FixedGrowthModel(growth_rate=0.1)  # 10% annual growth
)

# Run a simulation
results = model.simulate(
    days_to_simulate=30,
    num_simulations=1000
)

# Print key statistics
stats = results['statistics']
print(f"Current price: ${results['current_price']:.2f}")
print(f"Expected price after 30 days: ${stats['mean']:.2f}")
print(f"Expected return: {stats['expected_return']:.2f}%")
print(f"Probability of price increase: {stats['prob_above_current']:.2f}%")

# Visualize the results
plot_price_simulations(results)
```

### Available Growth Models

1. **Fixed Growth Model**
   - Constant annual growth rate
   - Suitable for stable, predictable growth scenarios

2. **Power Law Growth Model**
   - Growth rate scales with time
   - Useful for modeling diminishing returns or accelerating growth

3. **Exogenous Growth Model**
   - Custom growth function based on external factors
   - Supports market cycles, seasonal patterns, and other complex growth patterns

4. **Composite Growth Model**
   - Combines multiple growth models with weights
   - Allows for complex growth scenarios combining different factors

### Growth Model Examples

Run the growth model examples to see different growth scenarios in action:

```bash
python3 -m financial_sim_library.examples.growth_model_examples
```

This will demonstrate:
- Fixed growth with 10% annual rate
- Power law growth with diminishing returns
- Oscillating growth based on market cycles
- Composite growth combining multiple factors
- Complex growth with market cycles and exogenous variables

### Command Line Usage

The library includes a command-line interface for quick simulations:

```bash
# Run a basic simulation
python3 -m financial_sim_library.run_stock_simulator AAPL

# Customize the simulation
python3 -m financial_sim_library.run_stock_simulator AAPL --days 90 --simulations 500 --plot-type paths

# Save the results
python3 -m financial_sim_library.run_stock_simulator AAPL --save-plots --output-dir results
```

## Main Components

### Stock Simulator

- `StockPriceModel`: Abstract base class for all stock price models
- `GBMModel`: Implementation of Geometric Brownian Motion for stock price simulation

### Utilities

- `financial_calcs`: Utilities for financial calculations (volatility, risk-free rate, etc.)
- `data_fetcher`: Functions for fetching historical data and other market information

### Visualization

- `price_plots`: Functions for creating various types of plots for simulation results
  - Price path visualizations
  - Price distribution histograms
  - Price probability heatmaps

## Examples

More detailed examples are available in the `examples` directory:

- Basic simulation with default parameters
- Custom simulation with specific parameters
- Comparing simulations with different volatilities
- Simulating multiple tickers and comparing results

To run the examples:

```bash
python3 -m financial_sim_library.examples.stock_simulation_examples
```

## Architecture

The library is designed with extensibility in mind:

1. **Base Models**: Abstract base classes define the interfaces for different types of models
2. **Implementations**: Concrete implementations provide specific functionality
3. **Utilities**: Common functions for data handling and calculations
4. **Visualization**: Tools to analyze and display results

## Development

### Running Tests

Tests are available in the `tests` directory and can be run with:

```bash
python3 -m unittest discover -s financial_sim_library/tests
# or
pytest financial_sim_library/tests
```

### Adding New Models

To add a new stock price model:

1. Create a new class that inherits from `StockPriceModel`
2. Implement the required methods (`calibrate` and `simulate`)
3. Add any additional methods specific to your model

## License

[MIT License](LICENSE)

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## Acknowledgments

- This library uses [yfinance](https://github.com/ranaroussi/yfinance) for fetching market data
- Visualization is powered by [matplotlib](https://matplotlib.org/)
- Code was generated using Cursor with Sonnet 3.7
