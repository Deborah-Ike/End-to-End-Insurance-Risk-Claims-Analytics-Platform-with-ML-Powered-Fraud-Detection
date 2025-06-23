# Machine Learning for Insurance Fraud Detection 

## 1. Business Context
Problem:
Insurance fraud is a significant challenge in South Africa’s financial services sector. The South African Insurance Association (SAIA) estimates that fraudulent and dishonest claims cost the industry billions of rand each year. Manual review processes remain common, placing heavy pressure on claims teams and making it difficult to detect fraud quickly and consistently.

Impact:

* Substantial financial losses due to undetected or late-detected fraud
* Increased premiums for law-abiding policyholders
* Strained resources and backlogs in claims departments

## 2. Business Question
Can fraudulent insurance claims be accurately identified using machine learning to reduce financial losses and improve the efficiency of claims investigation?

## 3. Objectives
| Objective                                  | Success Metric                                    |
| ------------------------------------------ | ------------------------------------------------- |
| Develop a supervised fraud detection model | Precision > 90% (to reduce false accusations)     |
| Identify high-risk fraud patterns          | Insights via feature importance analysis          |
| Reduce manual review burden                | Prioritize top 10% of suspicious claims for audit |

## 4. Methodology
### Data Sources

* Historical structured data on insurance claims (e.g., policy details, customer profiles, vehicle info, incident and claim timing)

### **Key Steps**

#### Exploratory Data Analysis (EDA)

* Analyzed class imbalance (6% fraud rate)
* Identified behavioral red flags such as:

  * High claim-to-premium ratios
  * Incidents lacking police reports or witness statements
  * Claims submitted during unusual hours

#### Feature Engineering

* Created `loss_ratio` (claim amount / annual premium)
* Transformed `incident_hour` into time-of-day categories
* Encoded categorical features using label and one-hot encoding
* Scaled numerical features and handled class imbalance using SMOTE

#### Modeling

* Trained and compared Logistic Regression, Decision Tree, Random Forest, XGBoost, and CatBoost
* Focused on minimizing false negatives while preserving model interpretability
* Employed stratified 80/20 split and cross-validation to ensure consistent results across folds

#### Validation

* Evaluated using Precision, Recall, F1 Score, and ROC-AUC
* Emphasized Precision-Recall tradeoff due to high class imbalance

## 5. Results & Evaluation

### Model Performance

CatBoost outperformed all other models and was selected for its ability to handle categorical variables and deliver high precision and recall.

| Model | Accuracy | Precision | Recall | F1-score |
|-------|----------|-----------|--------|----------|
| CatBoost | 0.856 | 0.804 | 0.942 | 0.867 |
| Random Forest | 0.856 | 0.807 | 0.937 | 0.867 |
| XGBoost | 0.855 | 0.799 | 0.949 | 0.867 |
| Gradient Boosting | 0.854 | 0.796 | 0.950 | 0.867 |
| Decision Tree | 0.852 | 0.801 | 0.937 | 0.864 |
| KNN | 0.842 | 0.791 | 0.929 | 0.854 |
| Logistic Regression | 0.793 | 0.743 | 0.896 | 0.812 |
| Isolation Forest | 0.475 | 0.295 | 0.036 | 0.063 |

### Key Features Identified

* `witness_present`
* `reported_to_police`
* `total_claim_amount`
* `incident_severity`
* `base_policy`
* `vehicle_claim`
* `policy_annual_premium`

### Business Impact

* Automatically flagging the top 15% of high-risk claims can enable more focused investigations
* With a recall of over 94%, most fraudulent cases are detected early
* Potential to reduce fraud losses significantly and speed up the processing of low-risk claims

## 6. Alignment with Business Question

The project successfully answered the business question by building a model that flags high-risk claims with high precision. This allows investigation teams to allocate resources more efficiently and reduce exposure to fraudulent payouts. The model enhances operational capacity without introducing undue burden on honest claimants.

## 7. Recommendations

### Short-Term

* Integrate the model into existing claims processing workflows via an internal dashboard or scoring API
* Prioritize audit of claims with risk scores above 80%
* Implement a human-in-the-loop review for flagged claims during early deployment

### Long-Term

* Extend the model to include natural language processing of adjuster notes for deeper insights
* Collaborate with external insurance networks to improve fraud pattern recognition
* Establish a retraining and monitoring pipeline to maintain model accuracy over time



