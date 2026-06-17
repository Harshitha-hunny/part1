# part1
1. Data Loading and Initial Inspection
Loading Datasets: Six different CSV files (web_events, churn, customer, intervention, orders, support, rfm_modeling_snapshot) 
Initial Overview: The shape (.shape) and information (.info()) of each DataFrame are printed to understand their structure, column types, and initial non-null counts.



2. Data Quality Checks and Handling
Missing Values:
Identified missing values in customer (e.g., loyalty_tier, skin_type) and orders (rating).
Imputed loyalty_tier with 'Bronze' in both customer and rmf DataFrames.
Imputed skin_type with 'unknown' in the customer DataFrame.
Imputed rating with its mean in the orders DataFrame.

Duplicate Records: Checked for and confirmed no duplicate rows across all DataFrames.

Invalid/Unusual Values & Outliers:

orders DataFrame: Filtered out future order_date values (post 2025-09-30).
Identified potential outliers (using IQR method) in numerous numerical columns across web_events, orders, support, and rmf DataFrames (e.g., sessions_30d, gross_amount, resolution_hours).

Join/Key Issues & Consistency:
Ensured all customer_ids in related DataFrames are present in the master customer DataFrame, indicating good referential integrity.

Data Type Conversion: Converted relevant date columns (e.g., snapshot_date, signup_date, order_date, ticket_date) to datetime objects for proper temporal analysis.



3. Exploratory Data Analysis (EDA)
 
a)Customer Demographics and Profile Analysis: Visualized the distribution of various customer attributes using count plots, including:
City Tiers
Age Groups
Acquisition Channels
Loyalty Tiers
Preferred Categories
Skin Types
Marketing Consent

b)Churn Distribution Analysis: Plotted the distribution of the churn_next_60d target variable and calculated the percentage of churning vs. non-churning customers.
Order Behavior Analysis: Examined distributions of order-related metrics using histograms and count plots:
Quantity per order
Gross Amount per order
Discount Percentage
Delivery Days
Returned Orders
Order Ratings

c)Monetary Behavior Analysis (from RMF): Explored key RFM metrics distributions:
Recency Days
Frequency (orders in last 180 days)
Monetary Value (spend in last 180 days)

d)Support Ticket Issues Analysis: Visualized distributions of support-related data:
Issue Types
Support Channels
Ticket Resolution Hours
Customer Sentiment Scores
Reopened Support Tickets

e)Return/Refund Behavior Analysis: Displayed the distribution of return_rate_180d from the rmf DataFrame.

f)Web/App Activity Analysis: Analyzed distributions of web interaction metrics:
Web Sessions (last 30 days)
Product Views (last 30 days)
Cart Adds (last 30 days)
Wishlist Adds (last 30 days)
Abandoned Carts (last 30 days)
Email Opens (last 30 days)
Campaign Clicks (last 30 days)
Last Visit Days Ago

g)Campaign or Intervention History Analysis: Visualized distributions related to marketing interventions:
Last Campaign Received
Last Campaign Cost
Manual Priority Bucket



4. Churn Risk Hypotheses
Tested five specific hypotheses regarding customer churn using box plots to compare churned vs. non-churned groups and printing mean values:

Hypothesis 1: Customers with lower monetary value are more likely to churn. (Confirmed: Churned customers have significantly lower monetary value.)
Hypothesis 2: Customers with higher recency (haven't purchased for a long time) are more likely to churn. (Confirmed: Churned customers have higher recency days.)
Hypothesis 3: Customers with fewer web sessions (less engagement) are more likely to churn. (Confirmed: Churned customers have fewer web sessions.)
Hypothesis 4: Customers with a lower average rating for their orders are more likely to churn. (Confirmed: Churned customers have a slightly lower average rating.)
Hypothesis 5: Customers with a higher return rate are more likely to churn. (Confirmed: Churned customers have a higher mean return rate.)
