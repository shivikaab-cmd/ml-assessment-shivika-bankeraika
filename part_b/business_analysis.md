Part B: Business Case Analysis
B1. Problem Formulation
(a)

This problem can be formulated as a supervised machine learning regression problem.

The target variable is:

items_sold (number of items sold)

The input features include:

store_id
store_size
location_type
promotion_type
is_weekend
is_festival
competition_density
date-based features such as month and day_of_week

The goal is to predict the number of items sold based on different store conditions and promotional strategies. Since the output is a continuous numeric value, this is a regression problem.

(b)

The company currently uses total sales revenue as a performance measure. However, using items_sold is more appropriate for this problem.

Revenue can vary due to:

price differences
discounts and offers
product mix

On the other hand, items_sold directly reflects customer demand and sales volume, which is more relevant when evaluating the effectiveness of promotions.

This illustrates an important machine learning principle:
The target variable should be aligned with the business objective.

In this case, the goal is to maximize the number of items sold, not just revenue.

(c)

Using a single global model for all stores may not be ideal because different stores behave differently based on their location and customer base.

A better approach would be:

Build separate models for different store segments (for example, urban, semi-urban, and rural stores), or
Include interaction features between store characteristics and promotion types

This allows the model to capture how different stores respond to promotions differently, leading to more accurate predictions.

B2. Data and EDA Strategy
(a)

The raw data comes from multiple tables such as transactions, store attributes, promotion details, and calendar data.

Before modeling, these tables should be merged using common keys like store_id and transaction_date.

The final dataset should have one row representing:

a store
on a specific date (or aggregated at a monthly level)

The grain of the dataset can be:

store-level per day, or
store-level per month

Aggregation steps may include:

summing total items sold
averaging competition density
marking whether the period includes weekends or festivals
(b)

Before building a model, several EDA steps should be performed:

Target distribution analysis
Check how items_sold is distributed
Identify skewness or outliers
Promotion effectiveness
Compare average sales across different promotion types
Helps understand which promotions perform better
Time-based trends
Analyze sales by month or day of the week
Identify seasonality patterns
Store-level comparison
Compare sales across store sizes and locations
Helps identify high-performing segments

These analyses help in better feature engineering and improve model performance.

(c)

If 80% of transactions occur without any promotion, the dataset is imbalanced.

This can cause the model to:

learn mostly from non-promotional data
underestimate the effect of promotions

To address this issue:

Use balanced sampling techniques
Ensure enough promotional data is included during training
Create features that highlight promotion effects clearly
B3. Model Evaluation and Deployment
(a)

Since the data is time-based, a time-based train-test split should be used instead of a random split.

For example:

Use older data for training
Use the most recent data for testing

A random split is inappropriate because it can lead to data leakage, where future information is used to predict past data.

Evaluation metrics:

RMSE (Root Mean Squared Error)
MAE (Mean Absolute Error)

These metrics measure how close the predicted values are to actual sales.

(b)

If the model recommends different promotions for the same store in different months, it indicates that:

Customer behavior changes over time
Seasonal effects influence promotion effectiveness

Using feature importance, we can:

Identify which features (like month, promotion type, or location) influence predictions
Explain why certain promotions are recommended at certain times

This helps the marketing team understand and trust the model’s recommendations.

(c)

For deployment:

Model saving
Save the trained model using joblib or pickle
Monthly data update
Collect new data every month
Preprocess it in the same way as training data
Prediction generation
Use the model to recommend the best promotion for each store
Monitoring performance
Track prediction errors over time
Check if performance is degrading
Retraining
Retrain the model periodically using updated data

This ensures that the model remains accurate and useful over time.