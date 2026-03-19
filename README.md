# Data Analysis Report for the Weather Prediction Dataset

## 1. Project Overview
This project focuses on analyzing and forecasting world weather patterns using a comprehensive global weather dataset. The primary goal is to perform Exploratory Data Analysis (EDA) to find key insights and build robust machine learning models to forecast the current temperature (`temperature_celsius`) based on various environmental factors. This analysis helps understand geographical, spatial, and long-term climate variations, along with forecasting for environmental impact analysis.

## 2. Dataset Features
The dataset includes the following key meteorological and air quality parameters:
- **`last_updated`**: Time series information of the record.
- **`temperature_celsius`**: Current temperature (Target Variable).
- **`condition_text`**: Descriptive weather condition (e.g., Clear, Cloudy).
- **`wind_kph`**, **`wind_degree`**, **`wind_direction`**: Wind parameters.
- **`pressure_mb`**: Atmospheric pressure.
- **`precip_mm`**: Precipitation (Rainfall).
- **`humidity`**: Humidity levels.
- **`cloud`**: Cloud cover percentage.
- **`feels_like_celsius`**: Perception of temperature.
- **`visibility_km`**: Visibility.
- **`uv_index`**: UV radiation index.
- **`gust_kph`**: Gust speed.
- **Air Quality Parameters**: `air_quality_Carbon_Monoxide`, `air_quality_Ozone`, `air_quality_Nitrogen_dioxide`, `air_quality_Sulphur_dioxide`, `air_quality_PM2.5`, `air_quality_PM10`.
- > **Note:** The original dataset `.csv` file is larger than GitHub's 25MB upload limit, therefore it is not included in this repository. All data processing steps and results are fully documented within the Jupyter Notebook.

## 3. Data Analysis Steps

### Introduction
The weather dataset provides granular insights into different climatic metrics globally. Understanding these is crucial for precise weather forecasting.

### Data Cleaning
Rigorous data cleaning was performed to ensure model accuracy:
1.  **Duplicate Removal**: No duplicates were found in the dataset.
2.  **Null Value Handling**: Columns with significant missing values (like `gust_kph`) or less relevance (like `sunrise`, `sunset`, `moonrise`, `moonset`, `moon_phase`, `moon_illumination`) were dropped to simplify the model.
3.  **Data Typing**: Ensured `last_updated` was converted to a proper `datetime` format.

### Exploratory Data Analysis (EDA)
Comprehensive EDA revealed essential patterns:
- **Temperature Distribution**: Found that most records are clustered around the average temperature range, with rare occurrences of extremes.
- **Precipitation (Rainfall) Patterns**: Data showed that most days/locations in the dataset do not experience rainfall, with few heavy rain occurrences (outliers handled via IQR).
- **Correlations**: Significant correlations were found between `uv_index` and `temperature_celsius`.
- **Advanced EDA**: Used the Interquartile Range (IQR) method to detect and handle anomalies/outliers in precipitation and wind features to stabilize model training.

### Spatial and Geographical Analysis
Analyzed weather features across different locations:
- Identified **top 10 hottest countries** based on average recorded temperature.
- Visualized **continent-wise average temperature** to understand geographical patterns.

### Climate Analysis
Analyzed long-term patterns over time:
- Identified a clear monthly **temperature trend line**, showing how the global temperature varies throughout the year in the dataset.

## 4. Model Building
For this analysis, we implemented a robust forecasting pipeline using:
- **Train-Test Split**: Data was split into 80% training and 20% testing sets.
- **Features Used**: Selected numerical meteorological features (humidity, pressure, wind, uv_index, etc.) and extracted time-based features (`month`, `day`, `hour`) from the `last_updated` column.
- **Models Implemented**:
    1.  **Random Forest Regressor**: A base ensemble bagging model was trained.
    2.  **XGBoost Regressor**: An advanced boosting model was implemented to improve accuracy.
    3.  **Final Ensemble**: A combined model averaging predictions from both Random Forest and XGBoost.

## 5. Model Evaluation
The models were evaluated using Root Mean Squared Error (RMSE) and R-Squared (R2) score:

| Model | R2 Score | RMSE |
| :--- | :--- | :--- |
| Random Forest Regressor | **~0.874** | **~0.069** |
| XGBoost Regressor (Tuned) | **~0.879** | **~0.068** |
| Final Ensemble Model | **~0.88** | **~0.067** |

The results indicate that the advanced **XGBoost and Ensemble models outperformed the basic Random Forest model**, capturing around 88% of the variance in the temperature data on Normalized values. Feature importance analysis revealed that `uv_index` and `pressure_mb` are the most critical factors for temperature forecasting in this dataset.

## 6. Environmental Impact Analysis
An integral part of the assessment involved analyzing how weather features affect air quality. Our analysis demonstrated that **Temperature has a positive correlation with PM2.5 pollution**, suggesting warmer conditions are associated with higher particulate matter concentrations in the dataset.

## 7. Conclusion
In conclusion, this project successfully cleaned, analyzed, and built highly accurate forecasting models for global weather data. Using an ensemble of powerful models (Random Forest, XGBoost), we achieved an R2 score of **0.88**, demonstrating a strong predictive capability. The insights derived from EDA and Feature Importance will be instrumental in making informed decisions regarding environmental monitoring.
