# NYC Taxi Data Analysis: Classification and Regression

## Overview
This project analyzes NYC yellow taxi trip data from January 2015, focusing on classification and regression tasks. The goal is to predict whether a trip results in a high fare (classification) and to accurately estimate the fare amount (regression). The analysis leverages PySpark on Databricks to efficiently process and visualize large datasets, enabling scalable insights.

## Dataset
- **Source**: [NYC Yellow Taxi Trip Data (January 2015) on Kaggle](https://www.kaggle.com/datasets/elemento/nyc-yellow-taxi-trip-data)
- **Description**: This dataset includes various details about yellow taxi trips, such as pickup and drop-off times, trip distances, fare amounts, passenger counts, and pickup and drop-off locations.
- **Key Columns**:
  - `tpep_pickup_datetime` & `tpep_dropoff_datetime`: Timestamps of when the trip started and ended
  - `trip_distance`: Distance of the trip in miles
  - `fare_amount`: Fare charged for the trip
  - `passenger_count`: Number of passengers on the trip
  - `pickup_longitude` & `pickup_latitude`: GPS coordinates of pickup location
  - `dropoff_longitude` & `dropoff_latitude`: GPS coordinates of drop-off location
    
## Project Tasks
**Task 1: Classification**
Objective: Predict whether a trip resulted in a high fare (over $20) based on trip characteristics.

**Pipelines**:
- Decision Tree Classifier (Best Model)
- Logistic Regression
- Metrics: F1 Score, Precision, Recall
**Visualizations**:
- Bar charts comparing F1, Precision, and Recall.

**Task 2: Regression**
Objective: Predict the fare amount based on trip characteristics.

**Pipelines**:
- Linear Regression
- Random Forest Regressor (Best Model)
- Metrics: RMSE, R² Score
**Visualizations**:
- Residual plots
- Predicted vs. Actual plots

## Key Analyses and Insights
- `Trip Duration Analysis`:
Investigated trends in trip durations by hour and day to identify peak usage times.
- `Fare Amount Analysis`:
Explored fare variations by pickup location and passenger count.
- `Hotspot Identification`:
Mapped the most frequent pickup/drop-off locations, identifying high-demand areas.
- `Hourly Demand Analysis`:
Analyzed hourly patterns in taxi demand, highlighting peak hours.
- `Correlation Analysis`:
Evaluated relationships between trip duration, trip distance, and fare amount to uncover underlying trends.

## Project Structure
- `NYC-Taxi-Data-Analysis.ipynb`:
Jupyter Notebook containing the complete analysis, including data processing, feature engineering, and visualizations.
- `NYC-Taxi-Data-Analysis-Databricks.pdf`:
Exported Databricks notebook summarizing the workflow and findings.
- `README.md`:
Project overview and instructions.

## How to Run the Analysis
### Prerequisites
1. Databricks Environment (Recommended):
Use Databricks for a seamless PySpark setup.
2. Local Setup (Optional):
Install PySpark and required libraries:

```bash
Copy code
pip install pyspark pandas matplotlib seaborn
```
Steps
Clone this repository:
``` bash
Copy code
git clone https://github.com/TrueCodee/NYC-Taxi-Data-Analysis.git
```
Upload the NYC-Taxi-Data-Analysis.ipynb notebook to Databricks or open it locally in Jupyter Notebook.
Download the dataset from Kaggle and place it in the working directory.
Run all code cells in sequence to reproduce the analysis.

## Findings Summary
- `Average Fare by Hour`:
Higher fares observed during early morning hours (4-6 AM).
Lowest fares around 7 PM, likely due to competition during peak demand times.
- `Trip Duration Patterns`:
Peak demand occurs between 6 PM and 10 PM, aligning with the most frequent pickup hours.
- Popular Locations:
Certain GPS coordinates reveal hotspots with high pickup/drop-off frequencies, suggesting areas of increased demand.
- Fare and Distance Relationship:
A moderate correlation exists between fare amount and trip distance, reflecting standard fare calculation methods.
A weaker correlation between trip duration and fare highlights variability caused by traffic and route efficiency.
- Visualizations
Bar Charts:
Compare F1 Score, Precision, and Recall for classification pipelines (Decision Tree and Logistic Regression).
- Residual Plots:
Highlight model accuracy and consistency for regression pipelines.
- Predicted vs. Actual Plots:
Assess alignment between model predictions and actual fare amounts.
Model Pipelines
Classification
Decision Tree Classifier (Best Model):

Performance:
F1 Score: 97.68%
Precision: 98.32%
Recall: 99.11%
Purpose: Predict whether a trip results in a high fare (above $20).
Logistic Regression:

Performance:
F1 Score: 83.18%
Precision: 88.56%
Recall: 100%
Regression
Random Forest Regressor (Best Model):

Performance:
RMSE: 3.29
R² Score: 0.889
Purpose: Predict fare amounts based on trip characteristics.
Linear Regression:

Performance:
RMSE: 9.51
R² Score: 0.071
Saving and Loading Pipelines
Why Save Pipelines?
Reusability: Avoid retraining models for similar tasks.
Efficiency: Load pre-trained models for immediate use in production.
Reproducibility: Ensure consistent performance across environments.
How to Save a Pipeline
Example:
python
Copy code
```
cvModel.bestModel.write().overwrite().save("dbfs:/FileStore/random_forest_pipeline")
```
How to Load a Pipeline
Example:
python
Copy code
```
from pyspark.ml import PipelineModel

rf_pipeline = PipelineModel.load("dbfs:/FileStore/random_forest_pipeline")
predictions = rf_pipeline.transform(test_df_filtered)
```
## License
This project is open-source and available for educational and research purposes.
