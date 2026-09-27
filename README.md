# NSW Electricity Demand & Spot Price Forecasting

澳大利亚新南威尔士州电力需求与现货电价预测。

Python time-series analysis of 15-minute electricity demand (`TOTALDEMAND`) and spot price (`RRP`), forecasting the next four observations (one hour).

## Workflow

- Align the timestamp index and inspect duplicates and data quality.
- Use chronological train / validation / test windows of 28 / 10 / 2 days.
- Interpolate implausible demand observations; retain economically meaningful negative prices and price spikes, applying `arcsinh(RRP / 100)` for price modelling.
- Explore intraday patterns, distributions, ACF/PACF and demand-price relationships.
- Construct lagged inputs, calendar features and historical windows with train-fitted scaling where applicable.
- Compare Naive, Seasonal Naive, decomposition, lagged regression (including Ridge), ETS, SARIMA, MLP, RNN, LSTM and GRU methods.
- Evaluate RMSE, including original-unit price errors and spike/non-spike comparisons. The final forecast sections use a demand MLP and a price RNN; these choices do not imply that neural networks outperform every statistical benchmark.

## Files

- `electricity_forecasting.ipynb`: analysis and modelling notebook; saved outputs and execution metadata removed.
- `requirements.txt`: imported dependencies (not a version-locked environment).

## Running

1. Create a Python environment and install `pip install -r requirements.txt`.
2. Place the original `PRICE_AND_DEMAND_train_15min.csv` beside the notebook. Required columns include `SETTLEMENTDATE`, `TOTALDEMAND` and `RRP`.
3. Start JupyterLab with `jupyter lab` and review/run the notebook sequentially. Both TensorFlow and PyTorch are used; model searches may be computationally expensive.

The input dataset is not included in this repository. The notebook is an exploratory analysis with alternative model experiments, and the final export expects the original study dates (forecasts beginning 10 February 2026). It has not been re-executed end-to-end in this publishing environment. It is not a production forecasting service.

## Publication notes

This repository presents the supplied project notebook as a portfolio code artifact. Personal identifiers and saved execution outputs are omitted. The accompanying report is not distributed. The original modelling logic is retained; academic/group submission filenames are replaced with neutral output names. Dependencies and data must be supplied to reproduce the experiments.
