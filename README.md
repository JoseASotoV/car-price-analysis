# 🚗 Used Car Price Prediction Analysis

## 🗎 Overview

In this project, I analyze a dataset containing information about 426,880 used cars from Kaggle. The original dataset contained 3 million records, but it was downsampled to 426,880 entries for faster processing and modeling. My goal is to understand what factors contribute to the price of used cars and provide actionable insights to a used car dealership about what consumers value in a used car.

In this project I follow the CRISP-DM (Cross-Industry Standard Process for Data Mining) methodology, which is a well-established framework for addressing data problems.

## 📊 Data

The dataset used for this project contains the following features:

* Price: The price of the used car.
* Year: The year of manufacture of the car.
* Manufacturer: The brand or manufacturer of the car.
* Model: The model name of the car.
* Condition: The condition of the car (e.g., excellent, good, like new).
* Fuel: The type of fuel used by the car (e.g., gas, diesel, electric).
* Transmission: The type of transmission (e.g., automatic, manual).
* Odometer: The distance driven by the car in miles.
* Drive: The drive type (e.g., 4wd, fwd, rwd).
* Size: The size category of the car (e.g., compact, full-size).
* Type: The type of vehicle (e.g., sedan, SUV, pickup).
* Paint color: The color of the car’s paint.
* State: The state in which the car is located.

The dataset can be found in `data/vehicles.csv`

## ✨ Data Preprocessing

The following steps were taken to clean and prepare the data:

1. Handling Missing Values: Several columns in the original dataset had missing values. The missing values were handled as follows:
    * Numerical Columns: Rows with numerical values missing for critical columns (e.g., `year`, `price`, `odometer`) were removed.
    * Categorical Columns: For categorical columns such as condition, manufacturer, and model, missing values were imputed by using the most frequent value (mode), or rows with missing values were dropped when imputation was not suitable.
    * After preprocessing, no missing values remained in the dataset.

2. Removing Irrelevant Columns
Certain columns that were not relevant to the analysis, such as id, VIN, and state, were removed from the dataset to reduce noise and ensure more accurate modeling.
3. Converting Data Types
Several columns had incorrect data types. For example:
The year and age columns were converted to integers, with age being derived as the difference between the current year and the car’s manufacture year.
The price, odometer, and age columns were set as numerical types (int64, float64).
Categorical features such as condition, fuel, manufacturer, and model were kept as object (string) types.
4. Feature Engineering:
    * Age of the car: A new feature, age, was created by subtracting the year column from the current year, providing valuable information for modeling.
    * Categorical Encoding: Several categorical columns such as manufacturer, condition, fuel, and transmission were transformed using one-hot encoding to convert them into numerical representations suitable for modeling.
5. Removing Outliers: Outliers in the price and odometer columns were identified and removed. Cars with an odometer reading of 0 miles and extreme prices were considered outliers and removed to avoid skewing the analysis.
6. Dropping Duplicates: Duplicate entries were identified and removed to ensure the integrity of the dataset. This was especially important for categorical features like model and manufacturer, where duplicates could impact model training.
After these preprocessing steps, the dataset was reduced from 426,880 to 381,712 rows with 16 columns. The cleaned data was ready for further analysis and model building.

## 🗃️ Project Organization

* `notebook/used_cars.ipynb` The Jupyter notebook containing the data cleaning, analysis, and modeling steps.
* `data/vehicles.csv` The raw dataset used for the analysis.
* `images/` Folder containing the relevant plots and visualizations used in the analysis.

## 🔍 Key Findings

### Model Performance

Three regression models were tested:

* Linear Regression
  * R² Score: 0.45682
  * RMSE: $9,898.68
* Ridge Regression
  * R² Score: 0.45682
  * RMSE: $9,898.69
* Lasso Regression
  * R² Score: 0.45666
  * RMSE: $9,900.17

The models showed similar performance, so I decided to dive deeper on Ridge using `GridSearchCV` to find the best features and hyperparameter `alpha`.

## 💸 Recommendations to Dealership

The top features positively impacting used car pricing include vehicle condition (especially "new" or "like new"), certain car types like trucks, pickups, and convertibles, larger engine sizes (e.g., 12 cylinders), and premium brands like Audi. On the other hand, features negatively affecting pricing include front-wheel drive (FWD) vehicles, less conventional fuel types like electric, hybrid, and unknown, as well as cars in "salvage" or "fair" condition and those with smaller engines (e.g., 3 or 5 cylinders). For the dealership, this suggests a focus on high-demand car types, well-maintained vehicles in excellent condition, and premium brands. Additionally, balancing the inventory with fuel-efficient and high-performance models, while avoiding overstocking cars with lower drive types or subpar conditions, can help optimize sales and pricing.

![Top 10 Positive Impacting Features](images/top10pos.png)
![Top 10 Negative Impacting Features](images/top10neg.png)

Price Distribution: Distribution of car prices, highlighting the skew towards lower-priced vehicles.

Placeholder for plot: {{plot_price_distribution}}
Correlations with Price: A heatmap showing the correlation between numeric features and price.

Placeholder for plot: {{plot_price_correlations}}
Top Positive and Negative Features: Bar plots showing the features that most positively and negatively affect car prices.

Placeholder for plot: {{plot_top_positive_features}}
Placeholder for plot: {{plot_top_negative_features}}
Model Tuning
Grid search was performed to tune hyperparameters, particularly the regularization strength (alpha) for Ridge regression, leading to the following optimal parameter:

Best Alpha (Ridge): 0.1
Data After Cleanup
After cleaning the data (removing missing values and irrelevant columns), the dataset was reduced to 381,712 rows and 16 columns. The following are some key stats after cleaning:

## 🔮 Next Steps & Recommendations

For the used car dealership, the following actions are recommended:

* Prioritize Vehicles with Positive Features: Cars that are in good or excellent condition, have automatic transmission, and are pickups or trucks are likely to fetch higher prices.
* Assess the Market for Negative Features: Cars with salvage titles, non-gasoline fuel types (e.g., electric, hybrid), or front-wheel drive (fwd) may need to be priced more competitively or avoided for premium sales.
* Continual Model Improvement: Further feature engineering (e.g., adding more information about the car’s maintenance history) and testing different models could improve prediction accuracy.
