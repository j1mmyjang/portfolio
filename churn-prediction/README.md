# Employee Churn Prediction Model

## Overview

This project utilizes logistic regression to develop a predictive model for anticipating employee churn. Employee turnover incurs substantial costs, ranging from one-half to twice the employee's annual salary. The goal of this model is to identify key factors that contribute to employee churn and provide actionable insights to enable proactive measures for churn mitigation.

## Analysis Steps

1. **Exploratory Data Analysis (EDA):**
    - **Shape of the Dataset:** Checked the dimensions of the dataset using `df.shape` to understand the number of rows and columns.
    - **Descriptive Statistics:** Examined summary statistics with `df.describe()` for numeric features to understand their distributions.
    - **Standard Deviation Analysis:** Investigated standard deviations of numeric features using `df.std().sort_values(ascending=False)` to identify variables with significant variance.
    - **Categorical Features Summary:** Reviewed statistics for categorical features with `df.describe(include=object)` to understand unique values and frequencies.
    - **Class Distribution:** Explored the distribution of the target variable `Attrition` using `df.value_counts(df['Attrition'])` to assess class balance.

2. **Data Cleaning:**
    - **Missing Values:** Checked for missing values with `df.isnull().sum()` to identify any columns with null values.
    - **Duplicate Rows:** Examined duplicate rows using `df.duplicated()` and handled them appropriately.

3. **Outlier Detection:**
    - **Boxplots for Numeric Columns:** Created boxplots for all numeric columns using seaborn to visually identify outliers.

3. **Feature Engineering:**
    - **Drop Columns:** Removed unnecessary columns (`EmployeeNumber`, `EmployeeCount`, `StandardHours`, `Over18`) that do not contribute to the prediction task.
    - **Binary Conversion:** Converted binary categorical features (`Attrition`, `Gender`, `OverTime`) to numerical values (1 for 'Yes', 0 for 'No').
    - **One-Hot Encoding:** Applied `OneHotEncoder` to convert categorical features (`BusinessTravel`, `Department`, `EducationField`, `JobRole`, `MaritalStatus`) with more than two categories into binary variables.

4. **Modeling**
    - **Model Training:** Split the preprocessed dataset into training and testing sets using `train_test_split` from `sklearn.model_selection` and use statsmodels to fit model
    - **Model Evaluation:** Evaluate summary statistics, coefficients, confusion matrix, and performance metrics (accuracy, precision, recall, F1 score, and AUC-ROC)
    - **Model Optimization:** Tune the model for better performance by adjusting Decision Threshold and/or Class Weight (`GridSearchCV` and `StratifiedKFold` for cross-validation to search for optimal class weight hyperparameters), which can be crucial for imbalanced datasets.
  
## Results

The logistic regression model demonstrated a strong predictive capability with an accuracy ranging from 0.82 to 0.88 and a reasonable ability to distinguish between employees likely to churn and those likely to stay with a AUC-ROC score of approximately 0.79. Given the imbalanced nature of the dataset, where class 1 constituted only 16% of the data, the F1 Score emerges as a more reliable indicator of model performance. Subsequently, adjustments were made to the classification thresholds, producing the following outcomes.

### Threshold Comparison

| Threshold | Accuracy | Precision | Recall | F1 Score | AUC-ROC |
|-----------|----------|-----------|--------|----------|---------|
| 0.3       | 0.823    | 0.377     | 0.513  | 0.435    | 0.788   |
| 0.4       | 0.864    | 0.487     | 0.487  | 0.487    | 0.788   |
| 0.5       | 0.878    | 0.548     | 0.436  | 0.486    | 0.788   |

In determining the optimal threshold for predicting employee churn, it's vital to assess the cost implications associated with Type I and Type II Errors.

### False Negatives (Type II Error - Predicted No Churn, Actual Churn):

**Cost Implication:** Employees who are predicted as not likely to churn but end up leaving the organization can result in substantial costs. This includes the expenses associated with recruitment, onboarding, and training a replacement. Additionally, there might be indirect costs related to productivity loss and disruption within the team.

### False Positives (Type I Error - Predicted Churn, Actual No Churn):

**Cost Implication:** While false positives may lead to unnecessary retention efforts and interventions, the direct financial impact is typically lower compared to the costs associated with replacing an employee. The costs of retention strategies, such as engagement programs, are generally outweighed by the expenses of recruitment and onboarding.

Considering the cost factors:

- If precision is more crucial (minimizing false positives), choose threshold = 0.5.
- If recall is more crucial (minimizing false negatives), choose threshold = 0.3.
- For a balance between precision and recall, threshold = 0.4 could be a reasonable choice.

## Coefficient Analysis

The logistic regression model's coefficients provide insights into the impact of each feature on the likelihood of employee churn. Here are key findings:

- **DistanceFromHome:** A positive coefficient suggests that as the distance from home increases, the likelihood of churn also increases.
  
- **EnvironmentSatisfaction:** A negative coefficient indicates that higher levels of job satisfaction reduce the likelihood of churn.

- **OverTime:** The substantial positive coefficient suggests that employees who work overtime are more likely to churn.

- **YearsAtCompany:** A positive coefficient indicates that longer tenures at the company correlate with a higher likelihood of churn.

- **BusinessTravel:** Frequent travelers (BusinessTravel_Travel_Frequently) show a higher likelihood of churn compared to those who travel rarely (BusinessTravel_Travel_Rarely).

- **JobRoles:** Certain job roles, such as Laboratory Technician, Sales Representative, and Human Resources, have notable coefficients suggesting a higher likelihood of churn.

- **MaritalStatus:** Single employees (MaritalStatus_Single) have a higher likelihood of churn compared to married ones.

## Strategic Recommendations

Based on the statistically significant coefficients from the logistic regression model, the following strategic recommendations can be considered:

1. **Distance-Related Considerations:** Explore options to support employees with longer commutes. This could include flexible work arrangements, remote work options, or transportation assistance.

2. **Overtime Management:** Monitor and manage overtime hours, ensuring employees are not consistently overburdened. Consider workload distribution, resource allocation, and employee well-being.

3. **Tenure and Career Development:** Develop retention strategies focused on employees with longer tenures. Offer career development opportunities, training programs, and advancement paths to keep employees engaged.

4. **Travel Policies:** Review and optimize travel policies, especially for employees who travel frequently. Consider alternative arrangements or incentives to mitigate the impact of frequent business travel.

5. **Job Role-Specific Interventions:** For roles with higher likelihoods of churn (e.g., Laboratory Technicians, Sales Representatives), tailor interventions such as career development programs, mentorship, or role-specific engagement initiatives.
