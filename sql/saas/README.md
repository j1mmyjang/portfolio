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
