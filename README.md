🌾 Crop Yield Prediction using Machine Learning

Project Overview

This project aims to predict crop yield ($\text{hg/ha\_yield}$) using a dataset that combines geographic, environmental, and agricultural input factors (such as rainfall, pesticide usage, area, and temperature).

This is a regression problem, and the final notebook explores several machine learning models to determine the most accurate predictor.

Data

The dataset used, yield_df.csv (or similar, based on the notebook content), contains features influencing crop productivity across various regions and years.

Key Features

Feature Name

Description

Unit/Type

Year

The year of cultivation.

Integer

Area

The geographical area/country where the crop was grown.

Categorical (String)

Item

The specific type of crop (e.g., Maize, Potatoes, Wheat).

Categorical (String)

average_rain_fall_mm_per_year

Average annual rainfall.

$\text{mm}$/year

pesticides_tonnes

Total amount of pesticides used.

Tonnes

avg_temp

Average annual temperature.

Celsius

hg/ha_yield (Target)

The crop yield.

$\text{Hectograms}$ per $\text{Hectare}$ ($\text{hg/ha}$)

Data Preprocessing and Cleaning

The following steps were performed to prepare the data for machine learning models:

Drop Unnecessary Column: The initial index column (Unnamed: 0) was removed.

Handle Duplicates: All duplicate rows (2,310 entries) were identified and removed using data.drop_duplicates().

Data Type Conversion: The average_rain_fall_mm_per_year column was checked for non-numeric/string values, but no issues were found, and the column was explicitly cast to float64.

Feature and Target Separation:

Features ($\mathbf{X}$): Year, average_rain_fall_mm_per_year, pesticides_tonnes, avg_temp, Area, Item.

Target ($\mathbf{y}$): hg/ha_yield.

Train-Test Split: The data was split into training (80%) and testing (20%) sets.

Feature Engineering (ColumnTransformer)

A ColumnTransformer was used to apply appropriate scaling and encoding to different column types to prevent data leakage:

Transformation Name

Transformer

Columns

Purpose

StandardScale

StandardScaler

[0, 1, 2, 3] (Numeric)

Standardizes the numeric features ($\mu=0, \sigma=1$).

OHE

OneHotEncoder(drop='first')

[4, 5] (Categorical)

Converts categorical features (Area, Item) into a numeric format for modeling, dropping the first category to avoid multicollinearity.

Model Training and Evaluation

Four regression models were trained on the preprocessed training data (X_train_dummy) and evaluated on the test data (X_test_dummy).

Evaluation Metrics

MAE (Mean Absolute Error): The average magnitude of the errors (lower is better).

R2 Score (Coefficient of Determination): Measures the proportion of the variance in the target that is predictable from the features (closer to 1.0 is better).

Results Summary

Model

MAE

R2 Score

Convergence Notes

DecisionTreeRegressor (Dtr)

3,880.99

0.9807

Best Performer

LinearRegression (lr)

29,907.49

0.7473

Moderate performance.

Ridge (Rid)

29,864.62

0.7473

Similar to basic linear regression.

Lasso (lss)

29,893.95

0.7473

Warning encountered (Duality gap too large).

Conclusion

The Decision Tree Regressor achieved the highest $R^2$ score ($\approx 0.98$) and the lowest Mean Absolute Error ($\approx 3,881 \text{ hg/ha}$), indicating that it is the most effective model for capturing the complex, non-linear relationships between the input features and the crop yield.

Prediction Function

A final function was created to allow easy prediction of crop yield for new input parameters:

def prediction(Year, average_rain_fall_mm_per_year, pesticides_tonnes, avg_temp, Area, Item):
    # ... Uses the trained preprocesser and DecisionTreeRegressor model ...
    # Example input result: prediction(1990, 1485.0, 121.00, 16.37, 'Albania', 'Maize')
    # Example output: array([36613.])


Next Steps

Address Lasso Convergence: Re-run the Lasso model with max_iter set higher (e.g., 10,000) to ensure convergence.

Hyperparameter Tuning: Tune the hyperparameters of the Decision Tree Regressor (e.g., max_depth, min_samples_leaf) to potentially improve generalization and prevent overfitting.

Ensemble Methods: Explore high-performing ensemble models like RandomForestRegressor and XGBoost for further performance gains.
