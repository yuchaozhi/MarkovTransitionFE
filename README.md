# MarkovTransitionFE

This is the official repository of **Medical status forecasting with Markov feature engineering for autocorrelated categorical response variable.**

![Markov](./figures/Markov.png)
Fig.1 Framework Overview.

We re-evaluated the subgroup test results using chronological train-test splits (80% training, 20% holdout) for subgroup threshold estimation. The revised Subgroup-test AUCs are consistent with the original rankings: Markov+ $y_t$ achieves the highest performance across all models (e.g., iTransformer: 0.908; RF: 0.891; LSTM: 0.878). Followed by Original+ $y_t$ (iTransformer: 0.881; RF: 0.872).

### Numerical simulations under different time lengths 𝑇
![different time lengths 𝑇](./figures/Table1.png)

![different time lengths 𝑇](./figures/Table2.png)

![different time lengths 𝑇](./figures/Table3.png)

![different time lengths 𝑇](./figures/Table4.png)

![different time lengths 𝑇](./figures/Table5.png)

### Numerical simulations under different binomial distribution parameter settings *p*
![different binomial distribution parameter settings *p*](./figures/Table6.png)

![different binomial distribution parameter settings *p*](./figures/Table7.png)

![different binomial distribution parameter settings *p*](./figures/Table8.png)

![different binomial distribution parameter settings *p*](./figures/Table9.png)

![different binomial distribution parameter settings *p*](./figures/Table10.png)

### different population sizes *N*
![different population sizes *N*](./figures/Table11.png)

![different population sizes *N*](./figures/Table12.png)

![different population sizes *N*](./figures/Table13.png)

![different population sizes *N*](./figures/Table14.png)

![different population sizes *N*](./figures/Table15.png)
