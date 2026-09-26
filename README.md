# Customer Segmentation & Churn Analysis — Online Retail Dataset

Customer retention is significantly more cost-effective than acquiring new customers, 
making churn prediction and customer segmentation key priorities for any business 
with repeat buyers. This project segments customers by purchasing behavior, predicts 
which customers are at risk of churning, and identifies which customers represent 
the greatest priority for retention efforts.

## Project Goals
1. What customer segments exist based on purchasing behavior, and what defines each?
2. What is the likelihood that a given customer will churn, and what are the key 
   indicators driving that risk?
3. Which customers represent the greatest revenue risk if lost, and what retention 
   strategies follow from that?

## Dataset
[UCI Online Retail dataset](https://archive.ics.uci.edu/dataset/352/online+retail): 
~540,000 transaction line items from a UK-based online retailer, spanning December 
2010 to December 2011, covering 4,372 unique customers after cleaning.

## Approach
1. Data cleaning (missing values, duplicates, returns/cancellations)
2. RFM (Recency, Frequency, Monetary) calculation and customer segmentation
3. Behavioral feature engineering (purchase rhythm, return rate, spending trend)
4. Churn prediction modeling, with class imbalance addressed via SMOTE
5. Feature importance analysis to identify key churn indicators
6. Churn probability scoring and revenue-at-risk prioritization for retention

## Key Findings

**Segmentation:** Customers were grouped into six segments (VIP, Loyal, Potential 
Loyal, At Risk, High Risk Win Back, Lost) based on RFM scoring. Nearly 44% of 
customers fall into the two lowest-engagement segments (At Risk and Lost), 
representing a significant retention opportunity.

**Churn likelihood:** A logistic regression model, trained on SMOTE-balanced data 
with engineered behavioral features, achieved 77% recall on churned customers, 
correctly identifying most at-risk customers while maintaining reasonable precision 
(53%). This outperformed both a baseline model without behavioral features (51% 
recall) and a Random Forest model with the same features (56% recall), showing 
that feature engineering contributed more to performance than model complexity alone.

**Key churn indicators:** Monetary value is the dominant predictor of churn (46% of 
feature importance), with purchase frequency, rhythm, and spending trend each 
contributing comparably as secondary signals. Return behavior played a minor role 
by comparison.

**Retention priority:** Combining churn probability with customer value identified 
a concrete list of high-priority retention targets — customers who are both likely 
to churn and represent meaningful historical revenue.

**A note on model choice and retention cost:** the selected model favors recall over 
precision, meaning it will also flag some customers who wouldn't have actually 
churned. Whether this trade-off is worthwhile depends on the retention channel: for 
low-cost outreach (e.g., an automated email), a wider net is reasonable; for 
high-cost outreach (e.g., personal account manager calls), a higher-precision model 
may be preferable.

**Limitations & next steps:** This analysis was validated on a held-out test set 
(20% of customers). For actual deployment, the final model would be retrained on 
the full customer base. Additionally, return behavior for a small number of 
customers appears tied to purchases made
