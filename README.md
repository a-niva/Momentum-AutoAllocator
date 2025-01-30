# Momentum-Sharpe Portfolio Strategy 📈

A sophisticated Python implementation of a systematic trading strategy that combines momentum and Sharpe ratio signals to build and manage an equity portfolio. This implementation features an interactive Jupyter interface for real-time strategy adjustment and performance monitoring.

## Why This Strategy? 🎯

Traditional momentum strategies often suffer from high volatility and significant drawdowns. By combining momentum with the Sharpe ratio, this strategy aims to select assets that not only show strong price appreciation but also demonstrate favorable risk-adjusted returns characteristics. This dual-signal approach helps mitigate the typical pitfalls of pure momentum strategies while maintaining their positive aspects.

Key advantages of this hybrid approach:
- Reduced volatility compared to pure momentum strategies
- Better downside protection during market turbulence
- More stable portfolio turnover
- Enhanced risk-adjusted returns

## How It Works 🔄

The strategy operates through several sophisticated mechanisms:

### Signal Generation
- **Momentum Calculation**: Uses a 252-day (1 year) window to compute price momentum for each asset
- **Sharpe Ratio Calculation**: Evaluates risk-adjusted returns over the same period
- **Combined Scoring**: Implements a weighted ranking system combining both signals
  - Momentum weight is adjustable (default: 70%)
  - Sharpe ratio complement (default: 30%)
- **Signal Processing**: Includes data cleaning, outlier handling, and missing data management

### Portfolio Construction
- Maintains a fixed number of positions (configurable, default: 10)
- Implements a minimum holding period to reduce excessive trading
- Uses equal weighting for simplicity and robustness
- Considers transaction costs for realistic performance assessment

### Risk Management
- **Position Limits**: Equal weighting ensures no single position dominates
- **Holding Period**: Enforces minimum holding duration to reduce turnover
- **Transaction Costs**: Explicitly considers trading fees
- **Liquidity Management**: Filters out illiquid assets
- **Drawdown Control**: Monitors and reports maximum portfolio drawdown

## Features 🔧

### Interactive Interface
The strategy comes with a comprehensive Jupyter-based interface that provides:
- Real-time parameter adjustment through interactive sliders:
  - Number of positions
  - Signal weights
  - Holding period requirements
  - Transaction cost assumptions
- Dynamic visualization updates
- Performance metrics dashboard
- Portfolio composition tracking
- Trade history monitoring

### Data Management
Robust data handling infrastructure:
- **Automated Downloads**: Uses yfinance for data acquisition
- **Data Validation**: Implements comprehensive checks for data quality
- **Missing Data Handling**: Uses sophisticated interpolation techniques where appropriate
- **Update Management**: Tracks and updates price data automatically

### Performance Analytics
Comprehensive performance measurement system:
- **Returns Analysis**: 
  - Total return computation
  - Annualized returns calculation
  - Risk-adjusted metrics
- **Risk Metrics**:
  - Maximum drawdown tracking
  - Volatility measurement
  - Sharpe ratio calculation
- **Trading Analytics**:
  - Daily transaction counts
  - Portfolio turnover metrics
  - Position holding periods

## Installation and Setup 🚀

### Prerequisites
```bash
# Create a new virtual environment (recommended)
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install required packages
pip install pandas numpy yfinance ipywidgets matplotlib seaborn tqdm
```

### Initial Configuration
```python
# Import required modules
from portfolio_strategy import update_stock_data, initialize_strategy

# Define your universe of stocks
TICKERS = ['AAPL', 'MSFT', 'GOOGL', ...]  # Add your preferred stocks

# Update stock data
data, error = update_stock_data(TICKERS)

# Initialize strategy
if not error:
    strategy = initialize_strategy(data)
```

## Detailed Parameters ⚙️

### Core Parameters
- **top_n** (default: 10)
  - Number of positions in the portfolio
  - Range: 1-50
  - Impact: Higher numbers increase diversification but may dilute alpha

- **momentum_weight** (default: 0.7)
  - Weight given to momentum signal vs Sharpe ratio
  - Range: 0-1
  - Impact: Higher values favor price momentum over risk-adjusted returns

- **hold_period** (default: 15)
  - Minimum holding period in trading days
  - Range: 5-200
  - Impact: Higher values reduce turnover but may delay necessary portfolio updates

- **transaction_fee_rate** (default: 0.005)
  - One-way transaction cost
  - Range: 0-0.02
  - Impact: Higher values penalize frequent trading more heavily

### Advanced Features
- Automatic data quality checks
- Sophisticated error handling
- Performance caching
- Interactive visualization
- Real-time metrics updates

## Implementation Details 📝

### Trade Execution
- Decisions are based on previous day's data
- Trades are executed at next day's opening price
- Includes realistic slippage and transaction cost modeling

### Performance Optimization
- Vectorized operations for core calculations
- Efficient data structures for portfolio tracking
- Optimized memory usage for large datasets
- Smart caching of intermediate results

### Error Handling
- Comprehensive exception management
- Graceful degradation in case of data issues
- Detailed logging and error reporting
- Automatic recovery mechanisms

## Best Practices and Usage Tips 💡

1. **Universe Selection**
   - Start with liquid, large-cap stocks
   - Ensure sufficient historical data availability
   - Consider sector diversification

2. **Parameter Tuning**
   - Begin with default parameters
   - Adjust gradually while monitoring impact
   - Consider your investment horizon
   - Watch for overfitting

3. **Performance Monitoring**
   - Regular strategy assessment
   - Monitor turnover and costs
   - Track risk metrics
   - Analyze drawdowns

## Common Issues and Solutions 🔨

1. **Data Quality**
   - Missing prices
   - Corporate actions
   - Survivorship bias
   - Look-ahead bias

2. **Performance**
   - Computation speed
   - Memory usage
   - Real-time updates

3. **Risk Management**
   - Position sizing
   - Sector exposure
   - Market timing
   - Drawdown control

## Contributing 🤝

Contributions are welcome! Please feel free to submit a Pull Request. For major changes, please open an issue first to discuss what you would like to change.

When contributing:
1. Fork the repository
2. Create your feature branch
3. Commit your changes
4. Push to the branch
5. Open a Pull Request

## Disclaimer ⚠️

This strategy implementation is provided for educational and research purposes only. It is not financial advice and should not be used as the sole basis for investment decisions. Past performance does not guarantee future results.

Key risks to consider:
- Market risk
- Implementation risk
- Parameter sensitivity
- Transaction costs
- Data quality issues
- Technology risk

## License 📄

This project is licensed under the MIT License - see the LICENSE file for details.

## Contact 📫

For questions, suggestions, or collaboration opportunities:
- Open an issue on GitHub
- Submit a pull request
- Contact through project discussions

Your feedback and contributions are greatly appreciated!
