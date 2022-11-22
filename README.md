# Credit-Risk-Modeling-and-Scorecard-Development
- Developed data-driven credit risk model to predict probabilities of default (PD) and assigned credit scores to existing or potential borrowers using data includes information on over 450k consumer loans issued between 2007 and 2014 with 75 features.

- Performed feature selection using Chi-squared test for categorical features, ANOVA F-Statistic for numerical features, feature engineering using Weight of Evidence (WoE) and Information Value (IV), developed logistic regression model, and evaluated using AUROC. 

- Implemented credit risk scorecard to calculate individual credit scores and determine whether to approve or reject loans.

## Data

The dataset used for this projects is related to consumer loans issued by the Lending Club, a US P2P lender. The raw data includes information on over 450,000 consumer loans issued between 2007 and 2014 with almost 75 features, including the current loan status and various attributes related to both borrowers and their payment behavior.

- Link - https://drive.google.com/file/d/1xaF743cmUgI5kc76I86AeZDE84SMkMnt/view

## Data Exploration

- 18 features with more than 80% of missing values. Given the high proportion of missing values, any technique to impute them will most likely result in inaccurate results.

- Certain static features not related to credit risk, e.g., id, member_id, url, title.

- Other forward-looking features that are expected to be populated only once the borrower has defaulted, e.g., recoveries, collection_recovery_fee. Since our objective here is to predict the future probability of default, having such features in our model will be counterintuitive, as these will not be observed until the default event has occurred.

## Data Cleaning

- Remove text from the emp_length column (e.g., years) and convert it to numeric.

- For all columns with dates: convert them to Python’s datetime format, create a new column as a difference between model development date and the respective date feature and then drop the original feature.

-Remove text from the term column and convert it to numeric.

## Feature Selection

- Performed feature selection to identify the most suitable features for our binary classification problem using the Chi-squared test for categorical features and ANOVA F-statistic for numerical features.

- Calculated the pair-wise correlations of the selected top 20 numerical features to detect any potentially multicollinear variables. A heat-map of these pair-wise correlations identifies two features (out_prncp_inv and total_pymnt_inv) as highly correlated. Therefore,  droping them also for our model.

<img width="743" alt="Screen Shot 2022-11-21 at 8 56 05 PM" src="https://user-images.githubusercontent.com/68578215/203225169-997f983d-f7ef-4821-8346-9b4b2b6b18d5.png">



## WoE Binning and Feature Engineering

Creating new categorical features for all numerical and categorical variables based on WoE is one of the most critical steps before developing a credit risk model.


### WoE and IV
Weight of Evidence (WoE) and Information Value (IV) are used for feature engineering and selection and are extensively used in the credit scoring domain.

WoE is a measure of the predictive power of an independent variable in relation to the target variable. It measures the extent a specific feature can differentiate between target classes, in this case: good and bad customers.

IV assists with ranking our features based on their relative importance.

### Steps for WoE feature engineering

- 1. Calculate WoE for each unique value (bin) of a categorical variable, e.g., for each of grad:A, grad:B, grad:C, etc.
- 2. Bin a continuous variable into discrete bins based on its distribution and number of unique observations, maybe using pd.cut (called fine classing)
- 3. Calculate WoE for each derived bin of the continuous variable
- 4. Once WoE has been calculated for each bin of both categorical and numerical features, combine bins as per the following rules (called coarse classing)
