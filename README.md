# bitcoin_volatility_forecast
Application of GARCH model to forecast the volatility of Bitcoin
# Technology of Blockchain : Application of GARCH model to forecast the volatility of Bitcoin

In finance, volatility is a statistical measure of the dispersion of asset returns over time. It is often calculated as the standard deviation or variance of price returns. In this course, we will use the term "volatility" to describe either standard deviation or variance. Volatility describes the uncertainties surrounding the potential evolution of financial asset prices. It is an essential concept, widely used in risk management, portfolio optimization and other areas. It is also one of the most active areas of research in empirical finance and time series analysis. In general, the higher the volatility, the riskier a financial asset.

The GARCH model deals with stationary (mean around 0 and variance constant over time) and non-stationary variables.

The GARCH model embeds 3 concepts:
* **Autoregressive :** The current value can be expressed as a function of previous values, i.e. they are correlated. 
* **Conditional:** This indicates that the variance is based on past errors. 
* **Heteroscedasticity:** This implies that the series displays an unusual variance (variable variance).
GARCH models can be understood intuitively. Firstly, the model is autoregressive in nature. It attempts to estimate volatility at time $t$ on the basis of information known at time $t-1$. Secondly, it estimates volatility as a weighted average of past information.

For a GARCH(1,1) process to be realistic, two conditions must be met: 
* Firstly, all parameters $\omega$, $\alpha$, $\beta$ and must be non-negative. This ensures that the variance cannot be negative. 
* Secondly, $\alpha+\beta<1$ means that the model estimates are mean reversions of the long-term variance.
* The long-term variance is equal to $\omega/(1-\alpha-\beta)$.

The empirical rules for model parameters is that the larger the parameter $\alpha$, the greater the immediate impact of shocks. Here, shocks are expressed as residuals or prediction errors. If fixed, the larger the $\beta$ is, the longer the duration of the impact, i.e. periods of high or low volatility tend to persist.

### GARCH(1,1) equation 

$$GARCH(1,1): \sigma_{t}^{2} = \omega+\alpha\epsilon_{t-1}^{2}+\beta\sigma_{t-1}^{2}$$

### GARCH(p,q) equation

$$\text{GARCH}(p, q) : \sigma_t^2 = \omega + \sum_{i=1}^{p} \alpha_i \epsilon_{t-i}^2 + \sum_{j=1}^{q} \beta_j \sigma_{t-j}^2$$

* $\sigma_t^2$ represents the conditioal variance at time $t$
* $\omega$ is the constant or intercept term
* $\alpha_i$ are the parameters for the autoregressive conditional variance terms, where $i$ range from $1$ to $p$
* $\epsilon_{t-i}^2$ represents the squared returns at time $t-i$
* $\beta_j$ are the parameters for the conditional variance lag terms, where $j$ ranges from $1$ to $q$
* $\sigma_{t-j}^2$ represents the conditional variance at time $t-j$


Intuitively, the GARCH variance forecast can be interpreted as a weighted average of three different variance forecasts. One is a constant variance that corresponds to the long-term average. The second is the new information that was not available when the previous forecast was made. The third is the forecast made in the previous period. The weights of these three forecasts determine how quickly the variance changes with new information, and how quickly it returns to its long-term average.

In expectation, $X_t^2$ is the marginal variance of the log returns. Why is this the case? Recall the relationship between variance and expected value of $var(X) = E[X^2] - E[X]^2$. We know that $E[X_t] = 0$ because expected returns are trivially 0 due to the efficient market hypothesis. Thus, E[Xₜ]² = 0, and we are left with the marginal variance $\sigma = E[X^2]$, which is constant and does not depend on t.

We build on the concept of constant marginal variance to incorporate heteroskedasticity by modeling the volatility at time $t$ ($\sigma_t^2$), which is the conditional variance of the time series and is directly influenced by the squared log return $X_t^2$.

#### Note:

It's important to note that GARCH model can only be applied to time series that do not have any trends or seasonal effects, i.e. that has no (evident) serially correlation. Otherwise, the series have to be a white noise (mean close to 0 and constant variance over the time)
