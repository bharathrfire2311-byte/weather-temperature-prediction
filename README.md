# weather-temperature-prediction
A browser-based weather analytics and temperature prediction application using Linear Regression and Random Forest ML models, with interactive dashboards, data visualization, model evaluation, and real-time temperature forecasting.
#  Weather Temperature Prediction

A machine-learning-powered web application for **weather analysis and temperature prediction**. The application processes historical weather observations, performs data validation and feature engineering, trains machine learning models directly in the browser, and provides interactive visualizations and real-time temperature predictions.

##  Features

*  Interactive weather analytics dashboard
*  Temperature prediction using machine learning
*  Random Forest Regression
*  Linear Regression
*  Chronological **80/20 train-test split**
*  Automatic data validation and preprocessing
*  Feature engineering and standardization
*  Model performance evaluation
*  Feature importance analysis
*  Residual/error analysis
*  Seasonal weather analysis
*  Temperature distribution and timeline charts
*  Temperature vs. humidity analysis
*  Temperature vs. wind speed analysis
*  Temperature vs. atmospheric pressure analysis
*  Client-side machine learning execution
*  Weather prediction reports
*  Fast and interactive React interface

##  Machine Learning

The application currently implements two regression models:

### 1. Linear Regression

The Linear Regression model predicts temperature based on multiple meteorological and temporal variables.

### 2. Random Forest Regression

The Random Forest model uses an ensemble of decision trees with bootstrap sampling and feature subsampling to predict temperature.

The Random Forest implementation includes:

* Multiple decision trees
* Bootstrap sampling
* Random feature selection
* Variance-reduction-based splitting
* Feature importance calculation
* Ensemble prediction

##  Input Features

The prediction pipeline uses the following features:

| Feature              | Description                       |
| -------------------- | --------------------------------- |
| Previous Temperature | Previous observed temperature     |
| Humidity             | Relative humidity (%)             |
| Atmospheric Pressure | Atmospheric pressure (hPa)        |
| Wind Speed           | Wind speed (km/h)                 |
| Cloud Cover          | Cloud coverage (%)                |
| Precipitation        | Precipitation (mm)                |
| Season               | Spring, Summer, Autumn, or Winter |
| Hour of Day          | Observation/prediction hour       |
| Month                | Month derived from date/season    |
| Day of Week          | Day derived from date             |

Season is converted into numerical features using one-hot encoding.

##  Machine Learning Pipeline

```text
Historical Weather CSV
        ↓
Data Loading
        ↓
Data Validation
        ↓
Data Cleaning & Preprocessing
        ↓
Feature Engineering
        ↓
Season Encoding
        ↓
Feature Standardization
        ↓
Chronological 80/20 Split
        ↓
 ┌─────────────────────┐
 │                     │
 ▼                     ▼
Linear Regression   Random Forest
 │                     │
 └──────────┬──────────┘
            ↓
      Model Evaluation
            ↓
   MAE / MSE / RMSE / R²
            ↓
   Feature Importance
            ↓
   Temperature Prediction
```

##  Model Evaluation

The application evaluates both models using:

* **MAE** — Mean Absolute Error
* **MSE** — Mean Squared Error
* **RMSE** — Root Mean Squared Error
* **R² Score** — Coefficient of Determination

The test data is kept chronologically after the training data rather than randomly shuffled. This makes the evaluation more representative of a time-based prediction scenario.

##  Data Preprocessing

The application performs several validation checks before training:

* Missing required values
* Invalid temperature values
* Invalid humidity values
* Invalid atmospheric pressure values
* Invalid wind-speed values
* Invalid cloud-cover values
* Invalid precipitation values
* Duplicate observations
* Date and time parsing
* Season normalization

Invalid records are removed and validation warnings are generated.

##  Dashboard

The dashboard provides an overview of the historical weather dataset, including:

* Total weather records
* Average temperature
* Minimum temperature
* Maximum temperature
* Average humidity
* Average atmospheric pressure
* Average wind speed
* Most common season

### Visualizations

The application includes interactive charts for:

* Temperature distribution
* Temperature over time
* Temperature vs. humidity
* Temperature vs. atmospheric pressure
* Temperature vs. wind speed
* Average temperature by season

## Temperature Predictor

Users can enter weather conditions such as:

* Previous temperature
* Humidity
* Pressure
* Wind speed
* Cloud cover
* Precipitation
* Season
* Time

The application then predicts the expected temperature using the selected machine learning model.

The prediction also provides an expected temperature range based on the model's RMSE.

##  Project Structure

```text
weather-temperature-prediction/
│
├── public/
│   └── data/
│       └── weather_temperature.csv
│
├── src/
│   ├── components/
│   │   ├── ChartCard.tsx
│   │   ├── Header.tsx
│   │   ├── ModelMetrics.tsx
│   │   ├── ReportButton.tsx
│   │   ├── ResidualChart.tsx
│   │   ├── StatCard.tsx
│   │   ├── TemperatureResult.tsx
│   │   ├── WeatherDetails.tsx
│   │   ├── WeatherForm.tsx
│   │   └── WeatherTable.tsx
│   │
│   ├── ml/
│   │   ├── encoding.ts
│   │   ├── featureEngineering.ts
│   │   ├── linearRegression.ts
│   │   ├── modelTraining.ts
│   │   ├── preprocessing.ts
│   │   └── randomForest.ts
│   │
│   ├── pages/
│   │   ├── Dashboard.tsx
│   │   ├── ModelPerformance.tsx
│   │   ├── TemperaturePredictor.tsx
│   │   └── WeatherAnalysis.tsx
│   │
│   ├── services/
│   │   └── dataset.ts
│   │
│   ├── utils/
│   │   ├── insights.ts
│   │   ├── metrics.ts
│   │   ├── reportGenerator.ts
│   │   └── weatherAnalysis.ts
│   │
│   ├── App.tsx
│   ├── main.tsx
│   ├── index.css
│   └── types.ts
│
├── .env.example
├── .gitignore
├── index.html
├── package.json
├── tsconfig.json
├── vite.config.ts
└── README.md
```

##  Technologies Used

### Frontend

* React
* TypeScript
* Vite
* Tailwind CSS
* Lucide React

### Machine Learning

* JavaScript/TypeScript-based ML implementation
* TensorFlow.js
* Linear Regression
* Random Forest Regression

### Data Processing

* PapaParse
* CSV-based weather dataset
* Feature engineering
* Data validation
* Standardization

### Visualization

* Recharts
* Interactive charts and analytics

### Reporting

* jsPDF
* html2canvas

##  Installation

### Prerequisites

Make sure you have:

* Node.js
* npm

### Clone the repository

```bash
git clone https://github.com/YOUR_USERNAME/weather-temperature-prediction.git
cd weather-temperature-prediction
```

### Install dependencies

```bash
npm install
```

### Start the development server

```bash
npm run dev
```

The application will be available at the local Vite development URL shown in your terminal.

##  Production Build

Create a production build:

```bash
npm run build
```

Preview the production build:

```bash
npm run preview
```

Run TypeScript validation:

```bash
npm run lint
```

##  Dataset

The application reads the weather dataset from:

```text
public/data/weather_temperature.csv
```

The expected dataset contains fields such as:

```text
record_id
date
time
temperature
previous_temperature
humidity
pressure
wind_speed
cloud_cover
precipitation
season
```

The application validates the required columns before processing the dataset.

##  Prediction Workflow

When a user requests a prediction:

1. Weather conditions are collected from the prediction form.
2. Input values are validated.
3. Season is encoded.
4. Date/time information is converted into numerical features.
5. A feature vector is generated.
6. The selected trained model performs inference.
7. The predicted temperature is rounded to one decimal place.
8. An expected temperature range is calculated using model RMSE.
9. The result is displayed with a temperature category and model information.

##  Use Cases

This project can be used for:

* Weather data analysis
* Machine learning demonstrations
* Regression model comparison
* Educational ML projects
* Exploratory meteorological analysis
* Browser-based ML applications
* Temperature forecasting experiments
* Data visualization projects

##  Limitations

This project is intended primarily for **educational and analytical purposes**.

Prediction accuracy depends heavily on the quality, size, and representativeness of the historical dataset.

The application should not be considered a replacement for professional meteorological forecasting systems.

##  Future Improvements

Potential improvements include:

* LSTM-based time-series forecasting
* XGBoost/Gradient Boosting models
* More advanced hyperparameter tuning
* Cross-validation for time-series data
* Weather API integration
* Longer-term forecasting
* Model persistence
* More weather variables
* Automated dataset updates
* Location-based weather prediction
* Improved uncertainty estimation
* Cloud/server-side model training

##  License

This project can be used for educational and personal development purposes. Add an appropriate open-source license such as MIT if you want others to freely reuse and modify the project.

---

 **If you find this project useful, consider giving the repository a star!**
