# Insurance Claims Prediction

A company sells automobile insurance policies where customers pay us an annual premium to insure their vehicle for a year. Assume that each customer only has one vehicle, and one vehicle only has one driver (i.e., the customer). Also assume that if they get into an accident, they will always open a claim with the company.

#### Input
In the attached dataset, you will see the following fields:
-	Claim ID: customer unique ID
-	Gender: gender of customer
-	Age: age of the customer at the time of policy submission
-	Driving license: valid driver's license at the time of policy submission (1 = has a driving license, 0 = no driving license)
-	Region code: region code of the customer’s address
-	Previously insured: customer is previously insured with the company (1 = yes, previously insured with the company, 0 = no, not previously insured with the company)
-	Vehicle age: age of the customer’s vehicle at the time of policy submission
-	Previous_Vehicle_Damage: customer’s vehicle has previous damage (1 = has previous damage, 0 = no previous damage)
-	Annual premium: annual premium that the customer pays for their automobile policy
-	Policy_Sales_Channel: encoded sales channel that customer use to purchase their policy
-	Response: whether customer submitted a claim (1 = submitted claim, 0 = did not submit claim)

#### Objective
The task is to create a model that predicts whether a customer will get into an accident and submit a claim.

## Summary Report for Automobile Insurance Claims Prediction
The goal of the project is to predict whether a customer will submit an insurance claim based on their profile. This was achieved using various machine learning models and addressing class imbalance issues to enhance model performance.

## 1. Data Overview and Preparation
The dataset contains 382,154 records with 11 features related to customer demographics, insurance details, and the target variable, `Response` (1 = claim, 0 = no claim). Key features include:
- **Categorical Features**: `Gender`, `Driving_License`, `Region_Code`, `Previously_Insured`, `Vehicle_Age`, `Previous_Vehicle_Damage`, `Policy_Sales_Channel`, and `Response`.
- **Numerical Features**: `Age` and `Annual_Premium`.

### Data Cleaning and Encoding
- Missing values were not present in the dataset.
- Encoding was performed using binary encoding for features like `Gender`, `Driving_License`, and one-hot encoding for `Vehicle_Age`, `Region_Code`, and `Policy_Sales_Channel`.
- Numerical features were scaled using `MinMaxScaler` for `Age` and `StandardScaler` for `Annual_Premium`.

### Key Findings from Exploratory Data Analysis (EDA)
- The dataset contains more male (1) customers than female (0).
- Younger customers (20s and 30s) and those with older vehicles (>2 years) are more likely to submit a claim.
- Customers with previous vehicle damage are more likely to submit a claim.
- `Previously_Insured` has a strong negative correlation with `Response`, indicating that previously insured customers are less likely to file a claim.

## 2. Model Development and Evaluation
Three main modeling strategies were used: Baseline, Oversampling (using SMOTE), and Undersampling (using NearMiss2). Various models were developed and tuned for optimal performance using `RandomizedSearchCV`.

### Baseline Models
- Models such as Random Forest, XGBoost, and LightGBM were used without addressing class imbalance.
- **Performance**: LightGBM performed best with a **ROC AUC score** of ~0.57 for testing. However, the recall for minority class (claims) was low (17%), highlighting the need for resampling.

### Oversampling Models (SMOTE Technique)
- SMOTE was applied to balance the class distribution by creating synthetic samples for the minority class.
- **Performance**: LightGBM showed the best results with an **ROC AUC score** of **0.88** and **Precision-Recall AUC score** of **0.91**, demonstrating significant improvement in minority class predictions. This approach showed a balanced recall and precision, making it suitable for practical applications.

### Undersampling Models (NearMiss2 Technique)
- NearMiss2 undersampling was applied to balance the dataset by reducing the majority class, which led to reduced precision for non-claim predictions.
- **Performance**: LightGBM again outperformed other models with an **ROC AUC score** of **0.60** for testing, but the overall performance was lower than the oversampling approach due to the loss of majority class samples.

## 3. Recommendations
- **Computation Power**: Due to the computational costs of hyperparameter tuning and resampling techniques, we should use distributed computing. I had no access to GPU so had to use NearMiss version 1, instead of version 2 or 3. (Biggest Issue)
- **Feature Importance**: Further analysis of feature importance can provide insights into the key factors influencing claim submissions. I didn't have the time to do this but it could be a good next step.
- **Preferred Model**: The **LightGBM model with SMOTE oversampling** is recommended due to its balanced handling of both classes and high performance metrics. It provides a good balance between minimizing false negatives (missed claims) and managing false positives. But then again, it can only be because of over-sampling or over-fitting.

## 4. Final Say
The analysis reveals the importance of addressing class imbalance, The **LightGBM model with SMOTE** achieves the most balanced and reliable results, but still I doubt it as it is achived by synthetic data results. Though, it gives better results for risk management and decision-making in insurance pricing and claims handling strategies.
