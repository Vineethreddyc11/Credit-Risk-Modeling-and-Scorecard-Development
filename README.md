# Credit-Risk-Modeling-and-Scorecard-Development
- Developed data-driven credit risk model to predict probabilities of default (PD) and assigned credit scores to existing or potential borrowers using data includes information on over 450k consumer loans issued between 2007 and 2014 with 75 features.

- Performed feature selection using Chi-squared test for categorical features, ANOVA F-Statistic for numerical features, feature engineering using Weight of Evidence (WoE) and Information Value (IV), developed logistic regression model, and evaluated using AUROC. 

- Implemented credit risk scorecard to calculate individual credit scores and determine whether to approve or reject loans.

## Data

The dataset used for this projects is related to consumer loans issued by the Lending Club, a US P2P lender. The raw data includes information on over 450,000 consumer loans issued between 2007 and 2014 with almost 75 features, including the current loan status and various attributes related to both borrowers and their payment behavior.

- Link - https://drive.google.com/file/d/1xaF743cmUgI5kc76I86AeZDE84SMkMnt/view

## Data Exploration

- 18 features with more than 80% of missing values. Given the high proportion of missing values, any technique to impute them will most likely result in inaccurate results

- Certain static features not related to credit risk, e.g., id, member_id, url, title

- Other forward-looking features that are expected to be populated only once the borrower has defaulted, e.g., recoveries, collection_recovery_fee. Since our objective here is to predict the future probability of default, having such features in our model will be counterintuitive, as these will not be observed until the default event has occurred
