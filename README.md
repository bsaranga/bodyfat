# Body Fat Tracking — Jackson-Pollock 3-Site

Tracks body fat % over time using the Jackson-Pollock 3-site (men: chest, abdomen, thigh) skinfold equation with the Siri body-density-to-%BF conversion. Caliper noise and the formula's own SEE are propagated by Monte Carlo (10,000 draws per session).

The plots below are regenerated automatically by GitHub Actions on every push that touches `measurements.csv` or the notebook.

## Body fat % over time

![Body fat over time](plots/bodyfat_timeseries.png?v=fd322a0)

- **Inner shaded band** — 95% measurement uncertainty (caliper random + ±1 mm systematic).
- **Outer faint band** — ±3.5 %BF method SEE (JP3 vs. hydrostatic), the equation's own residual error.
- **Points** are color-coded by time of day (morning / afternoon / evening) since skinfolds genuinely shift across the day.

## Loss rate vs. reference ranges

![Rate speedometer](plots/rate_speedometer.png?v=fd322a0)

Weighted-least-squares fit of `BF% = a + b·t`, with 95% CI on the slope. Reference bands: sustainable cut (0.5–0.7 %BF/wk), aggressive (0.7–1.0), and faster-than-pure-fat-loss (>1.0).

## How to add a measurement

Append a row to `measurements.csv`:

```csv
timestamp,age,chest1,chest2,chest3,abdomen1,abdomen2,abdomen3,thigh1,thigh2,thigh3
2026-05-01 07:30,33,21,20,22,28,30,34,28,30,31
```

All skinfolds in mm. Three readings per site. Push to GitHub — the action re-runs the notebook and updates the plots in this README.

## Local setup

```sh
python3 -m venv .venv
.venv/bin/pip install -r requirements.txt
.venv/bin/jupyter notebook bodyfat.ipynb
```
