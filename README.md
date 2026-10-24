# Eskom Demand Forecasting: How Much Electricity Will South Africa Need Next Week?

## 1. Business problem

**Why the forecast matters.** Eskom has to have enough generation ready to meet demand every hour. When demand turns out higher than planned, the control room has two expensive options: run the diesel-fired open-cycle gas turbines (OCGTs), which cost far more per unit of electricity than coal, or reduce load (load shedding). When demand turns out lower than planned, coal units are kept running or on standby for nothing. A better forecast means less diesel, fewer emergencies and lower cost.

**Question.** How much electricity will South Africa need next week, hour by hour, and can a simple, transparent model match or beat Eskom's own published forecast?

**Forecast set-up**

- **Target:** `RSA Contracted Demand`, the hourly demand that Eskom has to supply through all the resources it has contracts with (its own plants and contracted independent power producers).
- **Horizon:** 7 days ahead, hourly: every week, forecast the next 168 hours.
- **Error metrics:** **MAPE** (mean absolute percentage error), easy for managers to read, and **MAE in MW**, the size of the error the control room has to cover with reserves.
- **Validation:** walk-forward over a full year, so every season is tested and nothing from the future leaks into training.
- **Benchmarks:** two simple baselines, and Eskom's own published forecast for the same hours.

**Why this is the South African flagship project.** It uses genuine South African data, published by Eskom, on a problem every South African has lived through.
