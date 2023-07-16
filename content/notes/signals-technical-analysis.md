+++
title = "Trading Signals using Technical Analysis"
description = "trading signals using technical analysis"
date = "2023-07-03"
aliases = ["trading signals using technical analysis"]
author = "Benjamin Hong"
math = true
+++

These are my notes from Chapter 2 of *Learn Algorithmic Trading* by Sebastien Donadio and Sourav Ghosh.

Signals in trading are pieces of information derived from market data, limit order books, or trade information that can be used to increase a trading strategy's profitability. Signals can be built using technical analysis. Below are different types of technical analysis.

### » Simple Moving Average
Takes the price average over a certain time period, where each price is weighted equally.
$$SMA = \frac{\sum_{i=1}^N P_i}{N}$$
where $P_i$ is the price at time $i$ and $N$ is the number of time periods.

### » Exponential Moving Average
Takes the price average over a certain time period, but more recent price observations are typically weighted more heavily while older observations are weighted less. However, it is also possible to weight older observations more heavily and weight new observations less.
EMAs with shorter time periods are more reactive and are called Fast EMA, while EMAs with longer time periods are less reactive and are called Slow EMA.
$$EMA = P * \mu + EMA_{old} * (1 - \mu) = (P - EMA_{old}) * \mu + EMA_{old}$$
where $P$ is the current price, $EMA_{old}$ is the previous EMA value, and $\mu$ is a smoothing constant (usually set to $\frac{2}{N+1}$ where $N$ is the number of time periods).

### » Absolute Price Oscillator
Uses moving averages to capture short-term deviations in prices. It measures how far the Fast EMA deviates from the Slow EMA. A large APO value usually means prices are starting to trend or overbuying/overselling is occurring.
$$APO = EMA_{fast} - EMA_{slow}$$
APO values are positive when prices are breaking out to the upside and negative when prices are breaking out to the downside. The magnitude of the APO value is relative to the magnitude of the break out.

### » Moving Average Convergence Divergence
Establishes the difference between a Fast EMA and a Slow EMA like APO. However, it uses additional smoothing via EMA to produce the final signal output. By smoothing out the noise of raw MACD values, the MACD signal can capture lasting trending periods.
$$MACD = EMA_{fast} - EMA_{slow}$$
$$MACD_{signal} = EMA_{MACD}$$
The difference between MACD values and the signals can be visualized as a histogram. The histogram captures the time period over which the trend occurs and the magnitude of lasting trends.
$$MACD_{histogram} = MACD - MACD_{signal}$$

### » Bollinger Bands
Computes a moving average of the prices as well as the standard deviation of the prices in the lookback period. It creates an upper band and a lower band that represent the expected volatility of the prices. When the prices move outside of these bands, this is interpreted as a signal for a breakout or for overbuying/overselling.
$$BBAND_{middle} = SMA$$
$$BBAND_{upper} = BBAND_{middle} + \sigma * \delta$$
$$BBAND_{lower} = BBAND_{middle} - \sigma * \delta$$
where $\sigma$ is the standard deviation and $\beta$ is the parameter controlling the width of the Bollinger band.

### » Relative Strength Indicator
Calculates the magnitude of the average of gains/price increases and the magnitude of the average of losses/price decreases over a lookback period. An RSI value is then computed to normalize the value between 0 and 100 and to find if there have been more gains than losses, or vice versa. RSI values over 50 signal for uptrends while values under 50 signal for downtrends.
For the last $N$ periods, if price increases monotonically, then absolute loss over the period is 0. If price decreases monotonically, then absolute gain over the period is 0. Otherwise,
$$RS = \frac{\sum |GainsOverLastNPeriods|}{\sum |LossesOverLastNPeriods|}$$
$$RSI = 100 - \frac{100}{1+RS}$$

### » Momentum
Measure of speed and magnitude of price movements. It is the difference between the current price and the price of some fixed time periods in the past. Consecutive periods of positive momentum indicate an uptrend and consecutive periods of negative momentum indicate a downtrend. SMAs and EMAs of the momentum indicator are often taken to detect sustained trends.
$$MOM = Price_t - Price_{t-n}$$