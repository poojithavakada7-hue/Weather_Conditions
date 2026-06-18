# Weather_Conditions
# Air Quality Prediction and AQI Estimation using XGBoost

## Overview

This project predicts multiple air pollutants using machine learning techniques and estimates the Air Quality Index (AQI) based on the predicted pollutant concentrations. The model is trained on the Beijing Multisite Air Quality dataset and uses weather-related parameters to forecast air pollution levels.

The project also provides a simple interpretation of weather conditions such as temperature, humidity, and wind characteristics.

---

## Features

* Predicts multiple air pollutants simultaneously:

  * PM2.5
  * PM10
  * SO₂
  * NO₂
  * CO
  * O₃
* Uses XGBoost Regression for high-performance predictions.
* Supports Multi-Output Regression.
* Estimates Air Quality Index (AQI).
* Categorizes AQI into standard air quality levels.
* Provides weather condition interpretation.
* Handles missing values automatically.

---

## Dataset

**Dataset Used:** Beijing Multisite Air Quality Dataset

The dataset contains:

### Input Features

| Feature | Description           |
| ------- | --------------------- |
| month   | Month of observation  |
| day     | Day of observation    |
| hour    | Hour of observation   |
| TEMP    | Temperature (°C)      |
| PRES    | Atmospheric Pressure  |
| DEWP    | Dew Point Temperature |
| RAIN    | Rainfall              |
| WSPM    | Wind Speed            |

### Target Variables

| Pollutant | Description             |
| --------- | ----------------------- |
| PM2.5     | Fine particulate matter |
| PM10      | Particulate matter      |
| SO₂       | Sulfur Dioxide          |
| NO₂       | Nitrogen Dioxide        |
| CO        | Carbon Monoxide         |
| O₃        | Ozone                   |

---

## Technologies Used

* Python
* Pandas
* Scikit-learn
* XGBoost
* NumPy

---

## Installation

### Clone Repository

```bash
git clone https://github.com/your-username/air-quality-prediction.git
cd air-quality-prediction
```

### Install Dependencies

```bash
pip install pandas numpy scikit-learn xgboost
```

---

## Project Workflow

### 1. Data Loading

The air quality dataset is loaded using Pandas.

```python
df = pd.read_csv('Beijing Multisite air Quality data.csv')
```

### 2. Data Preprocessing

Missing numerical values are replaced with the mean value of each column.

```python
df = df.fillna(df.mean(numeric_only=True))
```

### 3. Feature Selection

Selected weather parameters are used as model inputs.

```python
inputs = [
    'month',
    'day',
    'hour',
    'TEMP',
    'PRES',
    'DEWP',
    'RAIN',
    'WSPM'
]
```

### 4. Model Training

XGBoost Regressor is wrapped inside a MultiOutputRegressor to predict multiple pollutants simultaneously.

```python
xgb_model = XGBRegressor(
    n_estimators=100,
    learning_rate=0.1,
    objective='reg:squarederror'
)

model = MultiOutputRegressor(xgb_model)
```

### 5. Pollutant Prediction

The trained model predicts:

* PM2.5
* PM10
* SO₂
* NO₂
* CO
* O₃

---

## AQI Estimation

A simplified AQI estimation method is implemented:

```python
aqi = max(pm25 * 4, pm10 * 2)
```

### AQI Categories

| AQI Range | Category                       |
| --------- | ------------------------------ |
| 0 – 50    | Good                           |
| 51 – 100  | Moderate                       |
| 101 – 150 | Unhealthy for Sensitive Groups |
| 151 – 200 | Unhealthy                      |
| 201 – 300 | Very Unhealthy                 |
| >300      | Hazardous                      |

---

## Weather Interpretation Module

The project analyzes weather conditions from test samples.

### Temperature Classification

* Hot (≥ 30°C)
* Warm (20°C – 29°C)
* Cool (< 20°C)

### Humidity Classification

Estimated using dew point values.

* High Humidity
* Moderate Humidity
* Low Humidity

### Wind Analysis

* High Wind Energy
* Moderate Wind
* Low Wind

### Wind Direction Approximation

* North-East
* East
* Calm / Variable

---

## Sample Output

```text
Predicted Pollutant Levels for Sample Row:

PM2.5: 44.96
PM10: 83.51
SO2: 7.88
NO2: 62.74
CO: 904.07
O3: 10.91

Estimated AQI Value: 179.85

AQI Category: Unhealthy

Weather Condition Interpretation:

Temperature Condition: Cool
Estimated Humidity: 24.60% (Low Humidity)
Wind Speed: 1.7 m/s (Low Wind)
Wind Direction: Calm / Variable
Time of Observation: Hour 2.0, Month 12.0
```

---

## Future Enhancements

* Real-time air quality forecasting.
* Interactive dashboard using Streamlit.
* Integration with weather APIs.
* Advanced AQI calculation based on official EPA standards.
* Deep learning models such as LSTM and GRU.
* Model performance evaluation metrics (MAE, RMSE, R²).

---

## Applications

* Smart City Monitoring
* Environmental Research
* Air Quality Forecasting Systems
* Public Health Analysis
* Pollution Control and Management
