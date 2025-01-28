# Momentum-AutoAllocator
This Python script allows you to analyze a stock portfolio using momentum strategies, optimize asset allocation, and visualize the results through an interactive interface.

## Features

- **Momentum Analysis**: Identify top-performing stocks based on momentum over different time periods (1 day, 1 week, 1 month, YTD, and 1 year).
- **Performance Metrics**: Calculate portfolio performance, including returns, volatility, and Sharpe ratio.
- **Optimized Asset Allocation**: Create a balanced portfolio with risk constraints using hierarchical clustering and volatility optimization.
- **Interactive Analysis**: An interactive interface using ipywidgets to analyze portfolio performance and adjust parameters.

## Requirements

To use this script, you will need to install the following Python packages:

- `yfinance` for downloading stock data
- `pandas` for data manipulation
- `numpy` for numerical operations
- `scikit-learn` for clustering
- `ipywidgets` for interactive widgets
- `IPython` for displaying widgets

Install them using pip:

```bash
pip install yfinance pandas numpy scikit-learn ipywidgets IPython
```

## Functions

### `get_portfolio_performance(data, tickers, top_n=None)`

This function performs a momentum analysis on a given set of tickers and calculates performance metrics.

#### Arguments:
- `data`: A Pandas DataFrame containing stock price data.
- `tickers`: A list of tickers to analyze.
- `top_n`: The number of top-performing stocks to analyze (default is 10).

#### Returns:
- `current_top`: A DataFrame with the top performing tickers.
- `perf`: A dictionary containing performance metrics for different periods.
- `valorisations`: A dictionary containing portfolio values based on performance.
- `entries`: A set of tickers that entered the top N rankings.
- `exits`: A set of tickers that exited the top N rankings.
- `days_in_topN`: A dictionary with the number of days each ticker stayed in the top N.
- `data`: The raw stock data used for analysis.
- `perf_since_entry`: A dictionary with performance since entry for each stock.

### `optimize_vol_constrained(allocation, returns, max_vol)`

Optimizes the portfolio allocation based on a maximum volatility constraint.

#### Arguments:
- `allocation`: The initial portfolio allocation.
- `returns`: A DataFrame containing returns for the assets in the portfolio.
- `max_vol`: The maximum allowed volatility for the portfolio.

#### Returns:
- The optimized portfolio allocation.

### `get_balanced_portfolio(data, tickers, total_amount=1000, n_clusters=10, momentum_weight=0.6, sharpe_weight=0.4, max_vol=0.25)`

This function constructs a balanced portfolio by clustering stocks based on their correlations and selecting the best performing stocks within each cluster.

#### Arguments:
- `data`: A DataFrame containing stock price data.
- `tickers`: A list of tickers to include in the portfolio.
- `total_amount`: The total amount to invest (default is 1000).
- `n_clusters`: The number of clusters to create for asset grouping (default is 10).
- `momentum_weight`: The weight given to the momentum factor in the selection process (default is 0.6).
- `sharpe_weight`: The weight given to the Sharpe ratio in the selection process (default is 0.4).
- `max_vol`: The maximum allowed volatility for the portfolio (default is 0.25).

#### Returns:
- `final_allocation`: A Pandas Series with the final portfolio allocation.
- `metrics`: A dictionary with portfolio metrics such as return, volatility, and Sharpe ratio.
- `clusters`: A Series with the cluster assignments for each stock.

### `interactive_portfolio_analysis(TICKERS)`

Launches an interactive analysis interface that allows users to adjust portfolio parameters and analyze results.

#### Arguments:
- `TICKERS`: A list of stock tickers to analyze.

#### Widgets:
- **Top N Stocks**: Slider to choose the number of top-performing stocks to consider.
- **Clusters**: Slider to adjust the number of clusters used in portfolio optimization.
- **Total Amount (€)**: Input field to specify the total amount to invest.
- **Momentum Weight**: Input field to adjust the weight of momentum in the portfolio selection.
- **Sharpe Weight**: Input field to adjust the weight of the Sharpe ratio in the portfolio selection.
- **Max Volatility**: Input field to specify the maximum allowed volatility for the portfolio.

The interface will display the results, including the top-performing stocks, performance metrics, and optimized portfolio allocation.

## Example Usage

To use the script, simply import it and run the interactive analysis function with a list of stock tickers:

```python
from portfolio_analysis import interactive_portfolio_analysis

TICKERS = ["AAPL", "MSFT", "GOOGL", "AMZN", "TSLA"]
interactive_portfolio_analysis(TICKERS)
```

## Notes

- The script uses historical adjusted close prices and volume data from Yahoo Finance.
- The performance metrics include returns, volatility, and Sharpe ratio, which are annualized based on daily returns.
- The portfolio optimization uses a maximum volatility constraint to ensure the portfolio doesn't exceed a specified level of risk.

## License

This script is licensed under the MIT License.
