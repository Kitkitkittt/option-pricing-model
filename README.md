# Option Pricing Model Dashboard

## Overview

This project provides an advanced, interactive dashboard for pricing financial options using a variety of mathematical models. It integrates real-time financial data and sophisticated volatility analysis to deliver accurate and comprehensive pricing information. The application is built with Streamlit and features a modular architecture that is both scalable and easy to maintain.

For bounded agent work and checks that do not use market data, start with the
[offline verification handoff](SWARM_READY.md#verification-starting-point).

## Features

- **Multiple Pricing Models:**
  - **Black-Scholes:** The industry standard for European options.
  - **Binomial Tree:** A flexible model for both European and American options.
  - **Monte Carlo Simulation:** For pricing complex and path-dependent options.
  - **Heston Model:** A stochastic volatility model that captures the volatility smile.
  - **Merton Jump-Diffusion Model:** Accounts for sudden, significant price jumps.
- **Real-Time Data Integration:**
  - Fetches stock prices using the **Alpha Vantage API** when configured.
- **Advanced Volatility Analysis:**
  - **Historical Volatility:** Calculated from historical price data.
  - **Implied Volatility:** Extracted from market option prices.
- **Interactive Dashboard:**
  - A user-friendly interface built with **Streamlit** for easy input of option parameters.
  - Detailed visualizations of pricing results and model comparisons.
  - In-depth analysis of **Greeks** (Delta, Gamma, Vega, Theta, Rho).
- **Model Benchmarking:**
  - Tools to compare the accuracy and performance of different models.

## Architecture

The application is designed with a modular and extensible architecture, consisting of the following key components:

- **`streamlit_app.py`:** The main entry point for the user interface.
- **`data_provider.py`:** Fetches market data from Alpha Vantage when configured.
- **`volatility_engine.py`:** Centralizes the calculation of historical and implied volatility.
- **`models.py` & `advanced_models.py`:** Contain the implementations of the various option pricing models.
- **`base_model.py`:** Defines a common interface for all pricing models to ensure consistency.

For design context, see [`ADVANCED_MODELS_README.md`](ADVANCED_MODELS_README.md).
Its provider diagram predates the current Alpha Vantage implementation.

## Prerequisites

- Python 3.9+
- An Alpha Vantage API key only for live data; offline checks do not require one.

## Setup and Installation

1. **Clone the repository:**

   ```bash
   git clone https://github.com/Kitkitkittt/option-pricing-model.git
   cd option-pricing-model
   ```
2. **Create and activate a virtual environment:**

   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows, use `venv\Scripts\activate`
   ```
3. **Install the required dependencies:**

   ```bash
   pip install -r requirements.txt
   ```
4. **For authorized live data only:** Configure an Alpha Vantage API key in the
   dashboard sidebar. You can leave it blank for manual inputs.

## Running the Application

To launch the Streamlit dashboard, run the following command in your terminal:

```bash
streamlit run streamlit_app.py
```

## How to Use the Dashboard

1. **Fetch Market Data (Optional):**

   - With Alpha Vantage configured for live use, enter a stock ticker and select
     “Fetch Market Data.” Use manual inputs instead for offline work.
2. **Select a Pricing Model:**

   - Choose from the available models in the sidebar, such as Black-Scholes, Heston, or Merton Jump.
3. **Configure Option Parameters:**

   - Adjust the **Spot Price**, **Strike Price**, **Risk-Free Rate**, and other relevant parameters.
4. **Choose a Volatility Source:**

   - **Manual Input:** Enter a volatility value directly.
   - **Historical Volatility:** Calculate volatility based on historical data.
   - **Implied Volatility:** Fetch implied volatility from the options chain.
5. **Calculate the Option Price:**

   - Click the "Calculate Option Price" button to see the results, including the option price and a detailed analysis of the Greeks.
6. **Analyze a Portfolio:**

   - **Navigate to the "Portfolio Analysis" Tab:** Select the "Portfolio Analysis" tab from the main menu to access the portfolio management and risk analysis tools.
   - **Build Your Portfolio:**
     - In the sidebar, enter a stock ticker (e.g., `AAPL`), the quantity of shares, and the purchase price.
     - Click "Add to Portfolio" to include the asset in your portfolio.
     - Repeat this process to add multiple assets. Your portfolio will be displayed in a table.
   - **Run Risk Calculations:**
     - Once your portfolio is built, you can perform risk analysis.
     - Select the desired risk model (e.g., Historical VaR/CVaR, Monte Carlo VaR/CVaR, Parametric VaR).
     - Configure the parameters, such as the confidence level and time horizon.
     - The calculated Value at Risk (VaR) and Conditional Value at Risk (CVaR) will be displayed, giving you insight into potential losses.
   - **Define and Run Stress Tests:**
     - Create custom stress test scenarios to see how your portfolio would perform under specific market conditions.
     - Define a scenario by giving it a name, selecting an asset, and specifying the price shock (either as a percentage or an absolute value).
     - Run the stress test to see the potential profit and loss (P&L) impact on your portfolio.

## Contributing

Contributions are welcome! If you would like to improve the application or add new features, please feel free to submit a Pull Request.

## Deployment Instructions

#### Local Development

1. Ensure you have Python 3.9-3.12 installed
2. Create a virtual environment:
   ```
   python -m venv venv
   source venv/bin/activate  # On Windows use `venv\Scripts\activate`
   ```
3. Upgrade pip and setuptools:
   ```
   pip install --upgrade pip setuptools wheel
   ```
4. Install dependencies:
   ```
   pip install -r requirements.txt
   ```
5. Run the Streamlit app:
   ```
   streamlit run streamlit_app.py
   ```

#### Streamlit Deployment

1. Ensure you have a `requirements.txt` file with all dependencies
2. Set the main file as `streamlit_app.py`
3. Use Python 3.9-3.12 for compatibility

### Troubleshooting

- If you encounter `ModuleNotFoundError: No module named 'distutils'`:
  * Ensure you're using Python 3.9-3.12
  * Upgrade pip, setuptools, and wheel
  * Use the latest versions of dependencies
- Consider using `numpy>=1.26.0` and other flexible version constraints

## Installation

```bash
# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows use `venv\Scripts\activate`

# Install dependencies
pip install -r requirements.txt
```

## Running the Web Application

```bash
# On Windows
run.bat

# On macOS/Linux
python app.py
```

Navigate to `http://localhost:5000` in your web browser.

## Usage

### Python Module

```python
from option_pricing import calculate_option_price

# Calculate option price
price = calculate_option_price(
    spot_price=100,
    strike_price=100,
    risk_free_rate=0.05,
    volatility=0.2,
    time_to_expiry=1.0,
    option_type='call'
)
```

### Web Interface

1. Choose Option Type (Call or Put)
2. Enter Option Parameters
3. Click "Calculate Option Price"

## Update 12/13/24

**Added:**

- Implied Volatility Calculation
- Scenario Analysis
- Models Comparison
- Tooltips for Clarity
- Greeks Calculation (Delta, Gamma, Vega, Theta)

## License

MIT License

## WIP

* Fomula Accuracy
* More Robust Calculation
* Pricing for other assets classes
