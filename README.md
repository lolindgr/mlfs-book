# Air Quality Prediction Service (ID2223 Lab1)

Love Lindgren & Ahmad Al Khateeb
---
This repository contains our solution for **Lab 1 - Air Quality Prediction Service** in the course **ID2223: Scalable Machine Learning and Deep Learning** at KTH.

The lab builds an end-to-end ML system using **Hopsworks**, **AQICN**, **Open-Meteo**, **GitHub Actions**, and the provided notebooks from the original repo.


## Overview
The goal of the lab is to create a serverless ML pipeline that predicts PM2.5 air quality for selected sensor. The full system consists of:
- **Backfill pipelines** for historical air quality + weather data
- **Daily feature pipeline** (scheduled with GitHub Actions)
- **Training pipeline** to build a regression model
- **Batch inference pipeline** generating forecasts and hindcast plots
- A simple **dashboard** showing predictions

All notebooks and example code come from the original repository: [https://github.com/featurestorebook/mlfs-book/](https://github.com/featurestorebook/mlfs-book/).

This fork contains only minimal modifications needed to run the pipelines for our selected sensor.

### 1. API Keys Setup
Two APIs are required:

**_Hopsworks API Key_**
1. Log in at [https://app.hopsworks.ai](https://app.hopsworks.ai)
2. Go to **User** {\to} **API Keys**
3. Create a new key and save it.

**_AQICN API Key_**
1. Register at [https://aqicn.org](https://aqicn.org)
2. Get a **token** for API requests.

**_GitHub Secrets_**
<br>
Add the secret HOPSWORKS_API_KEY under **Settings** $\to$ **Secrets and variables** $\to$ **Actions* (used by GitHub Actions to run the daily pipeline).

### 2. Choose Sensor & Download Histrocial Data
A sensor from [https://aqicn.org](https://aqicn.org) was selected. Historical PM2.5 data and historical weather data were downloaded manually and loaded in the backfill notebook.

### 3. Daily Feature Pipeline (GitHub Actions)
The workflow file located in `.github/workflows/air-quality-daily.yml` runs once per day. It performs:
- Fetch latest PM2.5 value
- Fetch today's + 7-day weather forecast
- Updates Feature Groups in Hopsworks

### 4. Training Pipeline
The notebook `3_air_quality_training_pipeline.ipynb` trains an XGBoost regression model over joined weather + air quality features using a **Feature View**. The model is evaluated using **RMSE**, and registered in the Hopsworks Model Registry. The repository contains no changes to the training logic beyond sensor configuration.

### 5. Batch Inference & Dashboard
Teh notebook `4_air_quality_batch_inference.ipynb` loads the latest model and generates the **Forecast plot** (next 7 days), and **Hindcast plot** (actual vs predicted). These plots are exported as PNGs and served via **GitHub Pages** as a simple dashboard.

Dashboard URL: [https://lolindgr.github.io/mlfs-book/](https://lolindgr.github.io/mlfs-book/)

## How to Run Locally
1. Clone the repo
2. Create a local .env (at the root level of the cloned repository)
3. Create a Conda environment and install dependencies: `pip install -r requirements.txt`
4. Run notebooks 1-4 under `notebooks/airquality`

