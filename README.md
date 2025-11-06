🌾 Crop Yield Prediction using Machine Learning
📘 Overview

This project predicts crop yield (hg/ha_yield) using features like rainfall, temperature, pesticide use, area, and crop type. It’s a regression problem comparing multiple ML models.

📊 Dataset

File: yield_df.csv
Features:

Year, Area, Item, average_rain_fall_mm_per_year, pesticides_tonnes, avg_temp

Target: hg/ha_yield

🧹 Data Processing

Removed duplicates and unnecessary columns

Converted datatypes to numeric

Split into 80% train / 20% test

Used ColumnTransformer with:

StandardScaler → numeric columns

OneHotEncoder(drop='first') → categorical columns

🤖 Models & Results
Model	MAE	R² Score	Notes
Decision Tree Regressor	3,880.99	0.9807	⭐ Best
Linear Regression	29,907.49	0.7473	Moderate
Ridge	29,864.62	0.7473	Similar to LR
Lasso	29,893.95	0.7473	Convergence issue
✅ Conclusion

DecisionTreeRegressor gave the best performance (R² ≈ 0.98, MAE ≈ 3,881), effectively modeling non-linear relationships between environmental and agricultural features.

🔮 Prediction Example
