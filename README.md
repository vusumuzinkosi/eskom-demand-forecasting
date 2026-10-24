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

## 2. Data

**Source:** [Eskom Data Portal](https://www.eskom.co.za/dataportal/). The public pages show only the last week, so the full history was requested through the [data request form](https://www.eskom.co.za/dataportal/data-request-form/), which emails a download link. The file covers 1 April 2022 (the earliest date available) to 31 March 2027: **actual values up to 6 October 2026** (39,600 hours, 4.5 years, no gaps) and Eskom's forecasts after that.

The raw file is **not committed** to this repository (Eskom's terms apply). To run the notebooks, request the same data and save the CSV in `data/raw/`.

| Column | Meaning (MW, hourly average) |
|---|---|
| `RSA Contracted Demand` | Demand to be supplied by all resources Eskom has contracts with. **The target.** |
| `Residual Demand` | Demand to be supplied by resources Eskom National Control can dispatch: contracted demand minus wind, solar and other renewables |
| `RSA Contracted Forecast`, `Residual Forecast` | Eskom's own forecasts of the two demands |
| `Dispatchable Generation` | What the dispatchable fleet actually generated |
| `Wind`, `PV`, `CSP`, `Other RE`, `Total RE` | Contracted renewable generation (photovoltaic, concentrated solar, small hydro, biomass, landfill gas) |
| `... Installed Capacity` | Installed renewable capacity by type |

Definitions from the [Eskom Data Portal glossary](https://www.eskom.co.za/dataportal/glossary/). Two consistency checks pass: contracted minus residual demand equals renewable generation (median difference 0 MW), and residual demand exceeds dispatchable generation only in hours of load shedding (37% of hours, almost all in 2022 and 2023). The demand target therefore appears to include demand that was cut off, so it is consistent before and after load shedding.
