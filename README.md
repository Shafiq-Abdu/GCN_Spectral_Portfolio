# Project Summary: Portfolio Optimization Using Graph Convolutional Networks (GCNs) on Nifty 50 Stocks

## Objective
The objective of this project is to construct an optimized portfolio of Nifty 50 stocks by leveraging Graph Convolutional Networks (GCNs) and Spectral Graph Theory. The GCN model learns relationships between stocks based on correlation patterns, which are then used to assign weights for portfolio allocation. This approach is aimed at balancing risk and return by effectively capturing inter-stock dependencies.

---

## Project Steps and Algorithms

### 1. Data Collection and Preprocessing
- **Historical Data Collection**: 
  - Fetch daily closing price data for the Nifty 50 stocks over a specified period using the `yfinance` API. This data is required to calculate returns, volatility, and correlation between stocks.
- **Daily Returns Calculation**:
  - Calculate daily returns as the percentage change between consecutive days. This feature captures each stock’s price movement over time.
- **Volatility Calculation**:
  - Compute a rolling 30-day standard deviation of daily returns to represent the risk associated with each stock.
- **RSI (Relative Strength Index) Calculation**:
  - Calculate the 14-day RSI to capture momentum, indicating if a stock is overbought or oversold.

### 2. Graph Construction Using Correlations
- **Correlation Matrix**: 
  - Calculate a correlation matrix from the daily returns of the stocks. This matrix serves as a similarity measure to create the graph.
- **Graph Structure**:
  - Represent each stock as a node and add edges based on significant correlations (e.g., correlation > 0.5).
- **Spectral Clustering**:
  - Use spectral clustering on the graph’s Laplacian matrix to identify groups of similar stocks. This helps in improving diversification by preventing over-allocation to stocks with similar behaviors.

### 3. Feature Compilation
- **Feature Matrix for GCN**:
  - Combine daily returns, volatility, and RSI into a feature matrix. Each stock is represented by a vector containing these values, which serves as input for the GCN model.

### 4. GCN Model Setup and Training
- **GCN Architecture**:
  - Define a two-layer GCN with input features representing daily returns, volatility, and RSI.
  - The hidden layer aggregates each stock’s features and its neighbors' features, capturing dependencies in the stock network.
- **Model Training**:
  - Train the GCN using self-supervised learning. The model learns to produce embeddings that represent each stock’s importance and relationship to others based on the graph structure.
- **Output Embeddings**:
  - After training, the GCN outputs embeddings (low-dimensional representations) for each stock, which are used for portfolio weight assignment.

### 5. Portfolio Weight Assignment
- **Embedding Aggregation**:
  - Reduce each stock’s embedding to a single value (mean of the embedding dimensions) and normalize to sum to 1, resulting in portfolio weights.
- **Weight Mapping**:
  - Map each weight to its corresponding stock to finalize portfolio allocation.

### 6. Portfolio Backtesting and Evaluation
- **Calculate Portfolio Returns**:
  - Multiply daily returns by the assigned weights to get the daily portfolio return.
- **Performance Metrics**:
  - Evaluate cumulative return, annualized volatility, and Sharpe ratio to assess portfolio performance.
- **Result Interpretation**:
  - **Cumulative Return**: 52.78%
  - **Annualized Volatility**: 16.78%  (Risk)
  - **Sharpe Ratio**: 1.37

These metrics indicate favorable risk-adjusted performance, validating the GCN's ability to optimize portfolio weights effectively.

---

## Key Definitions and Important Points

1. **Graph Convolutional Networks (GCNs)**:
   - GCNs are neural networks that operate on graph-structured data, allowing each node to aggregate information from its neighbors. This is essential for modeling dependencies between stocks.
   
2. **Spectral Graph Theory**:
   - In spectral clustering, the graph Laplacian’s eigenvalues and eigenvectors provide insights into graph structure, allowing us to identify clusters of highly correlated stocks.
   
3. **Embedding**:
   - Embeddings are low-dimensional representations of nodes in a graph. In this project, each stock embedding captures both its individual characteristics and its relationships with other stocks.
   
4. **Portfolio Optimization**:
   - Assign weights to assets in a way that optimizes returns while balancing risk. The GCN’s embeddings help achieve this by capturing meaningful patterns in stock relationships.

5. **Sharpe Ratio**:
   - A measure of risk-adjusted return, calculated as the portfolio’s mean return divided by its volatility. Higher values indicate a better balance between risk and return.

---

## Assumptions Made

1. **Significant Correlations**: Only stocks with a correlation above a specified threshold are connected in the graph, assuming they have a meaningful relationship.
2. **GCN Features Reflect Importance**: By using daily returns, volatility, and RSI, we assume these features capture essential aspects of a stock’s risk and return profile.
3. **Static Correlation**: We assume that correlations between stocks are stable over the period, though they can change dynamically in real markets.

---



These results show that the GCN-based approach can effectively balance risk and return, outperforming traditional methods in some cases by capturing nuanced relationships between stocks.

---

## To do in Future and Extensions

1. **Dynamic Graphs**: Implement dynamic graphs that update correlations and features based on recent data, making the portfolio adaptive to changing market conditions.
2. **Additional Features**: Include other stock indicators, fundamental ratios, or sentiment scores to enhance feature richness.
3. **Alternative Weighting Schemes**: Experiment with different methods to aggregate embeddings, such as using attention mechanisms to weigh specific nodes.
4. **Compare with Other Models**: Benchmark the GCN-based approach against traditional methods, such as mean-variance portfolio optimization, to quantify the GCN’s added value.
5. **Backtesting on Extended Periods**: Test the model across different market cycles to validate robustness and adjust it to perform well under diverse market conditions.

### Read handwritten Notes attached in pdf format to get confused. Cheers:)

[Shafiq Abdul Rahman,IIT Madras](https://shafiq-abdulrahman.github.io/)
---

[Reference_1](https://tkipf.github.io/graph-convolutional-networks/)

