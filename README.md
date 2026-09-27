# Cyclone Prediction Model

## What it does
Given a storm's recent 3 readings (lat, lon, wind speed, pressure), predicts
the storm's position and intensity for the next 3, 6, 9, 12, 15, and 18 hours.

## Input format
List of exactly 3 readings, oldest to newest, each: [lat, lon, wind_knots, pressure_hPa]
Readings should be spaced ~3 hours apart.

## Output format
List of 6 predictions, one per forecast horizon (+3h to +18h), each containing
lat, lon, wind, pressure.

## Usage
See inference.py — call load_cyclone_model() once, then predict_cyclone_path()
per request.

## Validated on
Trained on IBTrACS North Indian Ocean cyclone data (1980-2024, JTWC wind/pressure).
Backtested on real Cyclone Amphan (2020) data — correctly identified Kolkata as
at-risk ~41 hours before actual landfall.

## Known limitations
- Requires an existing tracked storm with at least 3 readings — does not predict
  cyclone formation/genesis
- Trained only on North Indian Ocean (Bay of Bengal + Arabian Sea) storms
- No built-in uncertainty visualization beyond the fixed per-horizon confidence
  radius used in alert.py — treat outputs as estimates, not certainties
- This is a research/seminar prototype, not validated for real public safety use