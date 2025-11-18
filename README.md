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

## API Keys Setup
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
Add the following secrets under **Settings** $\to$ **Secrets and variables** $\to$ **Actions*:
- HOPSWORKS_API_KEY
