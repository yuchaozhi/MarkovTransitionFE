# MarkovTransitionFE

This is the official repository of **Medical status forecasting with Markov feature engineering for autocorrelated categorical response variable.**

![Markov](./figures/Markov.png)
Fig.1 Framework Overview.

We re-evaluated the subgroup test results using chronological train-test splits (80% training, 20% holdout) for subgroup threshold estimation. The revised Subgroup-test AUCs are consistent with the original rankings: Markov+ $y_t$ achieves the highest performance across all models (e.g., iTransformer: 0.908; RF: 0.891; LSTM: 0.878). Followed by Original+ $y_t$ (iTransformer: 0.881; RF: 0.872).

# Discussion 

Several limitations and assumptions of the proposed method should be acknowledged. 

**Assumption 1: Subgroup structure existence.** The subgroup test assumes that patients can be stratified into groups with similar model adaptability profiles. If the patient population is homogeneous with respect to model performance, subgroup stratification provides no benefit. We validate this assumption empirically through cross-subgroup validation (matching vs.~non-matching subgroups), which demonstrates that correctly matched subgroups achieve significantly higher AUC than mismatched combinations.

**Assumption 2: Temporal dependency.** The Markov transformation assumes that the transition dynamics are informative, i.e., $P(y_{t+2} | y_{t+1}, X_t) \neq P(y_{t+2} | X_t)$. If the state transitions are independent of the preceding state (no autocorrelation), the Markov encoding provides no additional information beyond the standard prediction model. In our ICU dataset, the strong autocorrelation of patient states validates this assumption.

**Assumption 3: Sufficient sample size.** The four-class representation increases classification complexity and may require larger sample sizes to achieve stable estimates, particularly for rare transition types (e.g., rapid deterioration 0→1). In our real data analysis ($N=200$ patients, $T \approx 48$ time points per patient), the sample size was sufficient, but smaller datasets may require class balancing techniques or alternative encoding strategies.

**Assumption 4: Stationarity within individuals.** We assume that each patient's transition dynamics are relatively stable within the observation window. If a patient's disease progression pattern changes fundamentally (e.g., due to medical intervention or sudden physiological change), the learned transition model may become outdated. Dynamic model updating mechanisms could address this limitation in future work.

**Limitation 1: Increased classification complexity.** Predicting four classes instead of one binary outcome increases model complexity and computational burden. However, our results demonstrate that modern machine learning architectures (RF, NNET, LSTM, iTransformer) can effectively handle this complexity while maintaining competitive training efficiency.

**Limitation 2: Class imbalance.** In clinical practice, certain transition types may be rare (e.g., rapid improvement 1→0 in critically ill patients). This can lead to imbalanced multi-class distributions, potentially biasing model predictions toward majority classes. We address this through the subgroup test framework, which matches patients to models trained on similar transition profiles, thereby mitigating imbalance effects at the subgroup level.

**Limitation 3: Loss of one observation per patient.** The Markov transformation reduces the time-series length by one observation per patient (from $T$ to $T-1$). For very short time series (e.g., $T < 10$), this loss may be non-trivial and could impact model training stability. In our application with $T \approx 48$, this reduction is negligible.

**Relation to standard approaches.** The Markov transformation differs from standard lagged-variable models $y_{t+1} = f(X_t, y_t)$ by encoding transition information in the response variable rather than as a covariate. This forces the model to explicitly learn the joint distribution $P(y_{t+2}, y_{t+1} | X_t)$, which is advantageous when transition patterns (e.g., 0→1 vs.~1→1) carry distinct prognostic meanings. Compared to traditional Markov chain models that assume stationarity and homogeneity, our approach allows patient-specific, covariate-dependent transition probabilities, enabling personalized modeling in non-stationary clinical environments.

**Drawbacks of the four-class transformation.** The four-class transformation introduces three potential drawbacks that should be considered: (i) increased classification complexity from 2 to 4 classes, which modern ML architectures (RF, NNET, LSTM, iTransformer) can handle effectively as demonstrated in our experiments; (ii) potential class imbalance for rare transition types (e.g., rapid improvement $1 \to 0$ in critically ill patients), which can be mitigated through subgroup-specific modeling that matches patients to models trained on similar transition profiles; and (iii) higher sample size requirements for stable four-class estimation, which was satisfied in our dataset ($N=200$, $T \approx 48$) but may require careful validation in smaller datasets.

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
