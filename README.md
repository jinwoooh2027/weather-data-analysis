# Weather Trend Forecasting - Data Science Assessment

**Developer**: Jinwoo Oh

---

**Product Manager Accelerator**

The Product Manager Accelerator Program is designed to support PM professionals through every stage of their careers. From students looking for entry-level jobs to Directors looking to take on a leadership role, our program has helped over hundreds of students fulfill their career aspirations. Our Product Manager Accelerator community are ambitious and committed. Through our program they have learnt, honed and developed new PM and leadership skills, giving them a strong foundation for their future endeavors.

Website: https://www.pmaccelerator.io/ | LinkedIn: https://www.linkedin.com/school/pmaccelerator/

---

## Project Overview

Global weather data from 256 capital cities (124,721 records, 34 features) analyzed end-to-end: cleaning, exploration, forecasting, and advanced climate/air quality analysis. The forecasting target is daily mean temperature in Washington Harbor, predicted using lag features, rolling means, and calendar variables.

**Dataset**: [Global Weather Repository](https://www.kaggle.com/datasets/nelgiriyewithana/global-weather-repository) (Kaggle)

## Notebooks

| Notebook | What it does |
|----------|-------------|
| `01_data_cleaning.ipynb` | Missing value imputation, duplicate unit column removal, IQR-based outlier capping, StandardScaler normalization demo |
| `02_eda.ipynb` | Temperature/precipitation distributions, correlation heatmap, humidity and pressure trends, anomaly detection (Isolation Forest + Z-score) |
| `03_forecasting.ipynb` | 5 models trained on Washington Harbor daily temperature, ensemble of top 3, feature importance comparison (3 methods) |
| `04_advanced_analysis.ipynb` | Continent-level climate trends, hemisphere seasonality, air quality vs weather correlations, interactive Folium maps, latitude-temperature regression |

## Forecasting Models

Five models trained on Washington Harbor daily mean temperature with an 80/20 chronological split:

| Model | Role in pipeline |
|-------|-----------------|
| Linear Regression | Baseline. Lag and rolling features carry enough signal for a simple linear combination to perform well. |
| Random Forest | Captures non-linear interactions (e.g., season-dependent lag behavior) that the baseline misses. |
| XGBoost | Sequential error correction on structured tabular data. Falls back to sklearn GradientBoosting if unavailable. |
| SARIMA | Works directly on the raw temperature series without engineered features. Weekly seasonality (s=7). |
| Prophet / SARIMA Variant | Automatic yearly and weekly seasonality detection. Falls back to SARIMA with monthly seasonality (s=30) on Python 3.14. |
| **Ensemble** | Simple average of the top 3 models by RMSE. |

**Best individual model**: Linear Regression (MAE: 2.15, RMSE: 2.64). All models evaluated on MAE, RMSE, MAPE, and R-squared. Note: MAPE is unreliable for this dataset because Washington Harbor winter temperatures approach 0 degrees C, causing near-zero division. MAE and RMSE are the more meaningful metrics here.

## Key Findings

- **Forecasting**: Lag features (especially lag_1) dominate feature importance across all three methods (Random Forest, XGBoost, permutation). The ensemble slightly improves on the best individual model.
- **Climate patterns**: Northern Hemisphere continents show strong seasonal swings; Southern Hemisphere (dominated by tropical Africa) stays relatively flat. Countries with the highest temperature variability sit at mid-to-high latitudes with continental climates.
- **Air quality**: Ozone formation is temperature-driven (photochemical). PM2.5 and PM10 decrease with wind speed (dispersion). Pollution hotspots concentrate in South Asia and parts of Africa/Middle East.
- **Spatial**: Interactive Folium maps (HTML in `outputs/`) show temperature and PM2.5 distributions across all 256 cities.

## Tech Stack

- **Language**: Python 3.14
- **Core**: pandas, numpy
- **Visualization**: matplotlib, seaborn, plotly
- **Machine Learning**: scikit-learn, xgboost
- **Time Series**: statsmodels (SARIMA), prophet
- **Spatial**: folium
- **Statistical**: scipy

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

4. Run the notebooks in order (01 through 04):
   ```bash
   jupyter notebook
   ```
