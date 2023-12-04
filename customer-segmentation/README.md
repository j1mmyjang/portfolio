# RFM and KMeans Clustering Analysis

## Overview

This project leverages RFM (Recency, Frequency, Monetary) analysis and KMeans clustering to gain insights into customer behavior in an e-commerce dataset. By segmenting customers into clusters based on their transaction patterns, the analysis aims to provide actionable insights for marketing and business strategies.

## Analysis Steps

1. **Data Preparation:**
    - Load the dataset and preprocess the data, including calculating the TotalCost and converting InvoiceDate to datetime.

2. **RFM Analysis:**
    - Calculate RFM values (Recency, Frequency, Monetary) for each customer.
    - Visualize RFM distributions and explore customer segments.

3. **KMeans Clustering:**
    - Use KMeans clustering to group customers into clusters based on RFM values.
    - Visualize clusters and derive actionable insights for each segment.

4. **Customer Profiles and Strategies:**
    - Create customer profiles for each cluster.
    - Formulate targeted marketing and business strategies for each segment.

## Results

<img src="https://github.com/j1mmyjang/portfolio/blob/758e85c3cf8d621b62336faebaa360d4d7f2d990/customer-segmentation/visualizations/boxplot.png">

### Overall Observations

- Cluster 1 seems to represent high-value, high-frequency customers who have made very recent purchases.
- Cluster 0 and Cluster 2 represent customers with recent transactions, but with varying levels of frequency and monetary value.
- Cluster 3 represents customers with transactions that are not as recent, moderate frequency, and moderate monetary value.


<img src="https://github.com/j1mmyjang/portfolio/blob/758e85c3cf8d621b62336faebaa360d4d7f2d990/customer-segmentation/visualizations/heatmap.png" width=70% height=70%>

### Cluster Profiles

| Cluster | Recency | Frequency | Monetary Value | Profile Description |
|---------|-------------|----------------|---------------------|--------------------|
| 0       | 0.25 (Recent) | 0.01 (Infrequent) | 0.02 (Low) | Occasional Shoppers: Recent transactions, infrequent, and low-value purchases. |
| 1       | 0.01 (Very Recent) | 0.26 (Frequent) | 0.86 (Very High) | High-Value Frequent Buyers: Very recent transactions, frequent, and high-value purchases. |
| 2       | 0.02 (Recent) | 0.27 (Moderate) | 0.27 (Moderate) | Balanced Shoppers: Recent transactions, moderate frequency, and moderate monetary value. |
| 3       | 0.04 (Moderately Recent) | 0.12 (Moderate) | 0.07 (Moderate) | Moderate Frequency Shoppers: Moderately recent transactions, moderate frequency, and moderate monetary value. |

### Insights and Actions

- **Occasional Shoppers:**
   - *Insight:* Recent but infrequent and low-value purchases.
   - *Action:* Targeted promotions to encourage repeat purchases. Highlight new products or limited-time offers.

- **High-Value Frequent Buyers:**
   - *Insight:* Very recent, frequent, and high-value purchases.
   - *Action:* Develop a loyalty program for exclusive offers. Provide personalized discounts to enhance loyalty.

- **Balanced Shoppers:**
   - *Insight:* Recent, moderate frequency, and moderate monetary value.
   - *Action:* Targeted marketing campaigns to maintain engagement. Consider cross-selling complementary products.

- **Moderate Frequency Shoppers:**
   - *Insight:* Moderately recent, moderate frequency, and moderate monetary value.
   - *Action:* Re-engagement strategies, such as personalized email campaigns. Leverage customer feedback to address pain points.

## Strategic Considerations

1. **Customer Satisfaction Surveys:** Explore customer satisfaction surveys to gather feedback, understand preferences, and enhance customer experience. Use insights to address pain points and tailor products or services for each segment.

2. **A/B Testing for Marketing Strategies:** Test different marketing strategies to understand what resonates most with each cluster. Conduct A/B testing on promotions, advertisements, or communication channels to optimize engagement and conversion rates for each segment.

3. **Customer Journey Analysis:** Analyze the customer journey for each cluster to understand touchpoints and interactions. Optimize the customer journey based on insights, ensuring marketing messages are timed appropriately and align with preferred channels.

4. **Dynamic Pricing Strategies:** Understand the price sensitivity of each cluster. Consider implementing dynamic pricing strategies, personalized discounts, or targeted promotions to maximize revenue from each segment.
 
