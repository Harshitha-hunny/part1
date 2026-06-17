Data Quality Report Summary
This report summarizes the data quality performed on the provided datasets.
1. Missing Values
Findings:-
a)customer DataFrame:
loyalty_tier: 1386 missing values (57.75%)
skin_type: 401 missing values (16.71%)
b)orders DataFrame:
rating: 80 missing values (0.98%)

Action Taken:-
loyalty_tier (in both customer and rmf DataFrames) was imputed with 'Bronze'.
skin_type in customer DataFrame was imputed with 'unknown'.
rating in orders DataFrame was imputed with the mean rating.

Potential Impact on Analysis/Modeling:-
Pre-imputation: Analysis involving loyalty_tier or skin_type would be biased or incomplete without handling missing values. Models relying on these features would either fail or produce inaccurate results. The high percentage of missing values in loyalty_tier and skin_type suggests that 'Bronze' and 'unknown' might become over-represented categories, potentially obscuring true patterns if not handled carefully.
Post-imputation: While imputation addresses missingness, it introduces assumptions. Using 'Bronze' for loyalty_tier might incorrectly categorize customers who could belong to higher tiers, potentially misrepresenting the loyalty distribution. Similarly, 'unknown' for skin_type creates a new category that may or may not be truly representative of these customers' characteristics. Mean imputation for rating reduces variance and can lead to underestimation of uncertainty in models.

2. Duplicate Records
Findings:-
No duplicate rows were found across any of the datasets (web_events, churn, customer, intervention, orders, support, rmf).

Potential Impact on Analysis/Modeling:-
This is a positive finding. The absence of duplicate records ensures that each observation is unique, preventing overcounting or biased statistics in analysis and training data inflation in models.

3. Outliers and Invalid Values
Findings:-
Numerous numerical columns across web_events, orders, support, and rmf DataFrames contained outliers (values falling outside the 1.5*IQR range).
Examples include sessions_30d, product_views_30d, abandoned_carts_30d, quantity, gross_amount, return_rate_180d, ticket_count_90d, negative_ticket_rate_90d, etc.
orders DataFrame: order_date contained future dates (post-2025-09-30). These were removed.
Potential Impact on Analysis/Modeling:

Outliers: Outliers can disproportionately influence statistical measures (means, standard deviations) and the training of models, especially those sensitive to extreme values (e.g., linear regression, K-Means clustering). They can skew distributions, inflate error rates, and lead to incorrect inferences about variable relationships. While some outliers might represent genuine extreme customer behavior (e.g., high spenders), others might be data entry errors or system anomalies. A deeper investigation into the nature of these outliers is often warranted.
Invalid Dates: Future dates((post-2025-09-30). These were removed.) in orders were invalid for historical analysis and would have introduced data leakage or erroneous calculations if not removed, particularly for time-series analysis or churn prediction models that rely on past behavior.

4. Join/Key Issues and Consistency
Findings:-
customer_id is unique in web_events, churn, customer, intervention, and rmf.
customer_id is not unique in orders and support (as a customer can have multiple orders and support tickets).
order_id is unique in orders.
ticket_id is unique in support.
All customer_ids in associated dataframes are present in the customer master list, indicating good referential integrity.
Potential Impact on Analysis/Modeling:

Non-unique customer_id in orders and support: This is expected and necessary for proper relational joining (one-to-many relationships). It allows for aggregating customer-level metrics from these transactional dataframes. However, care must be taken during aggregation to avoid data duplication or incorrect aggregation (e.g., summing gross_amount directly without grouping by order_id first if a customer has multiple items in one order).
Consistent customer_id across dataframes: This is a critical positive finding. It ensures that customer records can be reliably joined and matched across all datasets, enabling a comprehensive 360-degree view of each customer. This consistency is fundamental for accurate feature engineering and model building
