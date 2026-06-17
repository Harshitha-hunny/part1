Business Memo: Recommendations for Retention Campaign Investigation
To: Head of Retention
Subject: Key Areas for Investigation Before Launching Retention Campaigns

Executive Summary:
initial exploratory data analysis of customer behavior, transaction history, web interactions, and support engagements has revealed several critical indicators of customer churn. Before launching any retention
campaigns, we recommend focusing investigations on specific customer segments and behavioral patterns that exhibit a higher propensity for churn. This memo outlines the key findings and suggests areas for deeper
dive.
Key Findings & Recommendations for Investigation:
	1. Monetary Value and Recency of Purchase:
		- Finding: Customers with lower total spending in the last 180 days (monetary_180d) ,ie, lower moetary rate and longer periods since their last purchase (recency_days),ie, higher recency are significantly more likely to churn.
		- Recommendation: Investigate the demographics and purchase history of these low-monetary, high-recency customers. Are they new customers who made a single purchase and disengaged?Are there specific product
    categories they bought that led to dissatisfaction? We should explore personalized re-engagement offers, potentially focusing on products related to their initial purchase or high-value items with attractive 
    discounts.
	2. Web and App Engagement:
		- Finding: A decrease in web sessions (sessions_30d) in the last 30 days and an increase return rate ('return_rate_180d') in last 180 days are strong predictors of churn.
		 Recommendation: Examine the user journeys of customers with declining engagement. Are there technical issues on the website/app? Is the product discovery process intuitive? For customers with abandoned
     carts, immediate follow-up strategies (e.g., email reminders with offers) should be evaluated. We should also investigate if there are specific points in the user journey where customers drop off.
	3.average rating 
		- Finding:  Customers with a lower average rating ('avg_rating_180d')for their orders are more likely to churn.
		- Recommendation: Consistently low ratings for purchased products suggest dissatisfaction with product quality or service, which can be a significant factor driving customers to churn. Higher average
    ratings would imply greater satisfaction and loyalty.
	4. Loyalty Tier and Skin Type (Missing Values):
		○ Finding: While we imputed missing loyalty_tier with 'Bronze' and skin_type with 'unknown', a significant portion of customers initially lacked this information.
		○ Recommendation: Investigate why these fields were missing. Is there a gap in the customer onboarding process? Capturing this data could provide richer segmentation for retention efforts.
    For instance, are 'Bronze' tier customers more prone to churn
	5. Outliers in Key Metrics:
		○ Finding: Several numerical features (e.g., quantity, gross_amount, return_rate_180d) show a notable number of outliers.
		○ Recommendation: Analyze these outliers more closely. Are they legitimate high-value customers, frequent returners, or potential data entry errors? 
    For example, high return rates could indicate product dissatisfaction or deliberate abusive behavior, both requiring different retention strategies.high gross amount indicate high value customers
Conclusion:
The insights from this preliminary EDA provide a strong foundation for understanding churn drivers. We recommend a focused investigation into these areas to refine our understanding of why customers churn 
and to design targeted, effective retention campaigns. Subsequent steps should include building predictive models to quantify churn risk and test the effectiveness of different intervention strategies
