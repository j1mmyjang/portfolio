# Exploratory SQL Analysis of SaaS Data
This analysis delves into SaaS data, extracting insights on user behavior such as engagement, login patterns, and plan-specific activities. These findings can inform strategic decisions for optimizing SaaS services.

### Customer Table

| Field Name          | Description                                         |
|---------------------|-----------------------------------------------------|
| customer_id         | Primary Key                                         |
| age                 | Number of days the customer is (or was) a subscriber|
| churned             | Whether the customer has unsubscribed (1) or is still a subscriber (0)|
| sprout_base_plan    | Type of plan the customer subscribes to             |
| segment             | Small Business (SMB), Agency, or Corporate. NULL if unknown.|
| industry            | Industry the customer belongs to. NULL if unknown. |
| customer_demo_given | Date the customer received a demo of the product. NULL if the customer did not receive a demo.|
| facebook_profiles   | Number of Facebook accounts/pages the customer has connected|
| twitter_profiles    | Number of Twitter accounts the customer has connected|

### Customer Logins Table

| Field Name | Description                           |
|------------|---------------------------------------|
| customer_id| Foreign Key from customer              |
| login_id   | Unique ID for a user                   |

### Login History Table

| Field Name | Description                           |
|------------|---------------------------------------|
| login_id   | ID of user logging in                  |
| login_date | Date of log in                         |
| num_logins | Number of times user logged in on the given login_date|

## Analysis 
### Login Activity

Question: How many times has each customer logged in?
```sql
SELECT customer_id, COUNT(lh.login_id) AS num_login_days, SUM(lh.num_logins) num_total_logins
FROM customer_logins cl
LEFT JOIN login_history lh
ON cl.login_id = lh.login_id
GROUP BY customer_id
ORDER BY num_login_days DESC
```
Output:
| customer_id                           | num_login_days | num_total_logins |
|---------------------------------------|----------------|-------------------|
| cdd8541b3bad316034ecceb1ba51ce7b72f0b197 | 110            | 136               |
| 413a344f1c4bde8abd6cde7670d81af704b36ded | 80             | 95                |
| 38b47b7962702efe2067a86057bb51274688abfe | 72             | 102               |
| 1d5491d09e59eb21c67543a81df56c7235cad721 | 69             | 93                |
| edbfec6a28c8b602c0aa049cd82b02bae3c6d67c | 64             | 87                |

Answer: This query provides insights into the login activity of each customer. By examining the frequency of logins, we can distinguish between active and inactive customers. Analyzing these behavioral differences can offer valuable insights into customer engagement and usage patterns.

### Inactive Customers
Question: Are there any customers that have never logged in? If so, what percentage of total customers is this?
```sql
SELECT customer_id, SUM(num_logins) AS sum_logins
FROM customer_logins cl
LEFT JOIN login_history lh
ON cl.login_id = lh.login_id
GROUP BY customer_id
HAVING total_logins IS NULL
```
Output:
| customer_id                           | sum_logins |
|---------------------------------------|------------|
| 05d90656118773c37b03673a0aeb4bab45c463be | NULL       |
| 0c2a86df9149bdf8f6bb27572f0d4264efe35c0a | NULL       |
| 22f589a1d97508f65821eaac19511598be4f6268 | NULL       |
| 263b738c7a6a3bc96fb7bcd1f28e76472aaab911 | NULL       |
| 2ab4468da3bbd1ccd880e5a9383ee25a01659024 | NULL       |

Answer: 13 customers have never logged in which accounts for only ~2% of all customers. However, it's important to note that there are also 68 inactive login IDs. Many of these customers may still be considered "active" as they may have multiple login IDs, and a majority of them are logging in using other login IDs.
