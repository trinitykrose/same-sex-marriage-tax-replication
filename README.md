Same-Sex Marriage Recognition and Taxes: A Replication


Group project — three contributors (this notebook reflects joint work across all stages).


A replication of Friedberg & Isaac (2024), "Same-Sex Marriage Recognition and Taxes: New Evidence about the Impact of Household Taxation," The Review of Economics and Statistics, 106(1): 85–101.


The paper asks if the tax treatment of marriage (the "marriage subsidy" or "penalty" created by joint filing) affects whether same-sex couples choose to marry? The paper exploits staggered state-level recognition of same-sex marriage in the US, plus the 2013 federal recognition following United States v. Windsor, to identify the effect.


This replication builds the sample from American Community Survey (ACS) microdata, 2003–2017, identifying same-sex couples (married or cohabiting) via partner links and relationship codes.
Validates the sample against the paper's published Table A2 summary statistics — our sample of 16,146 married / 21,761 cohabiting couples closely matches the paper's 16,098 / 21,136.
Predicts earnings with a two-step LASSO model, trained on 2012 data, to construct an instrument for the marriage subsidy that doesn't suffer from simultaneity bias (couples adjusting labour supply in response to marriage/tax incentives).
Simulates tax liability for each couple under joint vs. separate filing using NBER's TAXSIM35, computing the implied marriage subsidy/penalty.
Estimates the effect via 2SLS, instrumenting the observed marriage subsidy with the LASSO-predicted subsidy, replicating the paper's Table 3.


Key result


Our IV estimate implies a marriage-subsidy elasticity of marriage propensity broadly consistent in direction with the paper's headline finding (paper: 0.011), though our estimate is noisier — see Limitations below.


Limitations 


Our first-stage F-statistics range from 15–32, versus 15–60 in the original paper. This is mainly because our LASSO feature set omits college major codes (a strong earnings predictor available to the original authors but not cleanly recoverable from our ACS extract), and because our employment-probability thresholds were calibrated slightly differently (0.957/0.923 vs. the paper's 0.963/0.969), which compresses the predicted earnings distribution and weakens the instrument.
As a result, our IV estimates are somewhat less precise than the original paper's, though the OLS specifications align closely.


Possible extensions


Quantile IV regression to test whether the marriage response to tax incentives is concentrated at specific points in the earnings distribution, rather than assuming a smoothly declining elasticity (as the paper's polynomial specification implicitly does).


Data & tools required to reproduce


ACS microdata (2003–2017), via IPUMS USA — restricted-access extract, not included in this repo.
NBER TAXSIM35 command-line binary, for tax liability simulation.
Python: pandas, numpy, scikit-learn, linearmodels, statsmodels.


Repo structure


replication_notebook.ipynb — full analysis, from raw ACS data through to the final regression table.
