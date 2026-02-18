# Weather Trend Forecasting - Data Science Assessment

**Developer**: Jinwoo Oh

---

**Product Manager Accelerator**

The Product Manager Accelerator Program is designed to support PM professionals through every stage of their careers. From students looking for entry-level jobs to Directors looking to take on a leadership role, our program has helped over hundreds of students fulfill their career aspirations. Our Product Manager Accelerator community are ambitious and committed. Through our program they have learnt, honed and developed new PM and leadership skills, giving them a strong foundation for their future endeavors.

Website: https://www.pmaccelerator.io/ | LinkedIn: https://www.linkedin.com/school/pmaccelerator/

---

## Project Overview

This project analyzes the **Global Weather Repository** dataset, covering 124,721 records across 34 features from 256 capital cities worldwide. The goal is to forecast future weather trends using both basic and advanced data science techniques.

**Dataset Source**: https://www.kaggle.com/datasets/nelgiriyewithana/global-weather-repository

## Key Analyses Performed

1. **Data Cleaning & Preprocessing** (`01_data_cleaning.ipynb`) - Handles missing values, removes duplicate unit columns, detects and caps outliers using IQR, and normalizes numeric features with StandardScaler.
2. **Exploratory Data Analysis** (`02_eda.ipynb`) - Explores temperature distributions, precipitation patterns, correlation heatmaps, and time series trends. Includes anomaly detection using Isolation Forest and Z-score methods.
3. **Weather Forecasting Models** (`03_forecasting.ipynb`) - Builds, trains, and evaluates 5 forecasting models with an ensemble approach. Includes feature engineering (lag features, rolling means) and feature importance analysis.
4. **Advanced Analysis** (`04_advanced_analysis.ipynb`) - Conducts climate analysis by continent and hemisphere, examines air quality correlations with weather, creates interactive spatial maps, and analyzes geographical patterns.

## Models Built

| Model | Description |
|-------|-------------|
| Linear Regression | Baseline model |
| Random Forest Regressor | Tree-based ensemble |
| XGBoost / GradientBoosting | Gradient boosted trees |
| SARIMA | Seasonal time series model (statsmodels) |
| Prophet / SARIMA Variant | Additional time series model |
| **Ensemble** | Weighted average of top 3 models |

All models are evaluated with **MAE**, **RMSE**, **MAPE**, and **R-squared** metrics, with a comparison table and actual vs. predicted visualizations.

## Advanced Analyses

- **Climate Analysis** - Long-term temperature trends by continent, seasonal patterns (Northern vs. Southern Hemisphere), temperature variability by country
- **Environmental Impact** - Air quality pollutant correlations with weather variables, PM2.5/PM10 analysis by weather condition
- **Anomaly Detection** - Isolation Forest and Z-score methods to identify extreme weather events
- **Spatial Analysis** - Interactive Folium world maps for temperature and PM2.5 distributions by city
- **Geographical Patterns** - Temperature distribution by continent, latitude vs. temperature regression, weather conditions by continent
- **Feature Importance** - Random Forest, XGBoost, and permutation importance compared side by side

## Tech Stack

- **Language**: Python 3.14
- **Core**: pandas, numpy
- **Visualization**: matplotlib, seaborn, plotly
- **Machine Learning**: scikit-learn, xgboost
- **Time Series**: statsmodels (SARIMA), prophet
- **Spatial**: folium (interactive maps)
- **Statistical**: scipy
- **Report**: Jupyter Notebook

## Project Structure

```
weather-data-analysis/
├── data/
│   └── GlobalWeatherRepository.csv    # Downloaded from Kaggle
├── notebooks/
│   ├── 01_data_cleaning.ipynb         # Data cleaning and preprocessing
│   ├── 02_eda.ipynb                   # Exploratory data analysis
│   ├── 03_forecasting.ipynb           # Forecasting models
│   └── 04_advanced_analysis.ipynb     # Advanced analysis
├── outputs/
│   └── figures/                       # Saved plots (PNG)
├── requirements.txt
├── .gitignore
└── README.md
```

## How to Run

1. Clone the repository:
   ```bash
   git clone https://github.com/jinwoooh2027/weather-data-analysis.git
   cd weather-data-analysis
   ```

2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

3. Download the dataset from [Kaggle](https://www.kaggle.com/datasets/nelgiriyewithana/global-weather-repository) and place `GlobalWeatherRepository.csv` in the `data/` folder.

4. Open the notebooks in order (01 through 04) in Jupyter:
   ```bash
   jupyter notebook
   ```

## Results Highlights

- 5 forecasting models compared with a weighted ensemble approach that combines the top performers
- Interactive world maps visualizing temperature and air quality distributions across 256 cities (HTML files in `outputs/`)
- Comprehensive climate and air quality analysis spanning 6 continents, revealing seasonal patterns, pollution hotspots, and geographical trends
