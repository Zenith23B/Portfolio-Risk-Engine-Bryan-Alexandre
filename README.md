
Ce notebook construit un moteur d’analyse de risque de portefeuille en Python, avec téléchargement de prix historiques via Yahoo Finance, calcul des rendements, volatilité, Sharpe, drawdown, VaR et Expected Shortfall. Il simule aussi des scénarios de stress (2008, Covid, 2022) et un backtesting de la VaR via le test de Kupiec. Le portefeuille est diversifié avec des actions et ETF (SPY, QQQ, AAPL, NVDA, TLT, BND, GLD, etc.) et des poids fixes. Il analyse la corrélation entre actifs et la contribution de chacun au risque total. Il exporte ensuite les résultats sous forme de CSV/ZIP pour exploitation. En bref, c’est un outil de gestion quantitative du risque de portefeuille, très orienté finance quantitative et modélisation.

Which stock is the most volatile?
- NVIDIA (NVDA) is the most volatile stock, with an annualized volatility of 51.7% (according to the course data).

Does VaR pass the backtest? (Kupiec, traffic light)

How does diversification change with crisis
correlations?

Why do Historical and Parametric VaR differ?

Why does Monte Carlo VaR differ from Historical VaR?

Why is Expected Shortfall useful in addition to VaR?

What happens when the portfolio becomes more
concentrated?

Which stress scenario is worst, and which asset drives
it?
