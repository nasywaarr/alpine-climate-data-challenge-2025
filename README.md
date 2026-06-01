# 🏔️ Alpine Climate Data Challenge 2025

> **Timeline:** 22 Feb – 3 Mar (8 days)  
> **Focus area:** Susa Valley & Maurienne Valley, Western Alps (Italy × France border)  
> **Goal:** Use open data to build predictive climate models & novel visualisations, with a view toward the **2030 Winter Olympics**

---

## 🗂️ Challenge Structure

| Track | Platform | Task |
|-------|----------|------|
| Data Processing & Model Development | **SoBigData** | Load notebooks, activate models, train/validate |
| Visualisation & Prototype | **Foundry (Palantir)** | Interactive dashboards, solution-building |

**AIP = Foundry + GenAI**

A physically-based climate modeling framework developed during the
[Alpine Climate Data Challenge](https://journal.opendataplayground.com/alpine-climate-data-challenge-en/),
organized by Open Data Playground and TELT (Tunnel Euralpin Lyon Turin), with
technical partners Palantir, SoBigData, and Fourth Age.

## Overview

The challenge tasked teams with building predictive climate models for the
**Val di Susa and Maurienne Valley** (Italy–France alpine corridor), combining
historical climate data with IPCC future scenarios. The goal: simulate the
evolution of key climate variables — temperature, precipitation, snow cover,
wind, humidity — and make results accessible through interactive dashboards.

This repository contains the physical climate model developed by Team H,
which focuses on alpine-specific processes calibrated on ERA5 reanalysis
data spanning 1990–2024.

## Model Architecture

The model combines physics-based process modules with data-driven calibration:

- **Orographic Precipitation Module** — simulates precipitation enhancement
  from mountain topography
- **Snow-Albedo Feedback Module** — captures feedback between snow cover
  and surface temperature
- **Mountain Boundary Layer Module** — models alpine atmospheric boundary
  layer dynamics
- **Surface Energy Balance Module** — computes radiative and turbulent
  heat fluxes
- **Glacier and Snowpack Module** — simulates snow accumulation, aging,
  and melt

## Data

Built on **ERA5 climate reanalysis data** (ECMWF), with variables including
2m temperature, total precipitation, snow depth, snow albedo, surface solar
radiation, wind components, cloud cover, and boundary layer height.

Additional open data sources referenced per challenge guidelines:
ARPA Piemonte, Copernicus Climate Data Store, Météo France, NOAA, ISPRA,
DREAL Auvergne-Rhône-Alpes.

## Calibration Approaches

Four calibration methodologies were explored:

**1. Basic Calibration** — calibrated on 1990–2014, validated on 2015–2024.

**2. Climate Change Era Analysis** — data split into early (1990–2000),
middle (2001–2012), and recent (2013–2024) eras to detect parameter shifts
over time.

**3. Seasonal Calibration** *(not executed — high error rate in base model)*
— designed to produce separate parameter sets for DJF, MAM, JJA, SON.

**4. K-fold Cross-Validation** *(not executed — same reason)* — 5-fold
cross-validation across the multi-decade dataset for robust uncertainty
quantification.

## Usage
```python
from alpine_model import load_historical_data, main_calibration_workflow

data_path = "path/to/era5_data.nc"
historical_data = load_historical_data(data_path)

calibration_period = slice('1990-01-01', '2013-12-31')
validation_period = slice('2014-01-01', '2024-12-31')

optimal_parameters = main_calibration_workflow(
    historical_data,
    calibration_period,
    validation_period
)
```

## Team H

| Name | University |
|------|------------|
| Maksim Kocheshkov | Università degli Studi di Milano |
| Aderinsola Yakubu | Birmingham City University |
| Nasywa Ramadhani | Università degli Studi di Messina |

## Competition

| | |
|-|-|
| **Organizers** | Open Data Playground, TELT |
| **Technical Partners** | Palantir, SoBigData, Fourth Age |
| **Duration** | Feb 22 – Mar 3, 2025 (8-day hackathon) |
| **Final Pitch** | March 12, 2025 · TELT HQ, Turin, Italy |

## Acknowledgments

ERA5 data provided by the European Centre for Medium-Range Weather
Forecasts (ECMWF). Physical parameterizations inspired by established
mountain climate literature.
