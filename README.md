# Credit Line Increase Model Card

## Basic Information
 1. Person or organization developing model: Patrick Hall, jphall@gwu.edu and Carissa Paul (carissa.paul@gwu.edu)
 2. Model date: August, 2021-2025
 3. Model version: 1.0
 4. License: MIT
 5. Model implementation code: DNSC_6301_Example_Project.ipynb

## Intended Use
   * Primary intended uses: This model is an example probability of default classifier, with an example use case for determining eligibility for a credit line increase.
   * Primary intended users: Students in GWU DNSC 6301 bootcamp.
   * Out-of-scope use cases: Any use beyond an educational example is out-of-scope. 

## Training Data
   * Data Dictionary
     |       Name       | Modeling Role | Measurement Level |                        Description                         |
     |:---------------:|:-------------:|:-----------------:|:---------------------------------------------------------:|
     |     term_360     |     input     |        int        | Binary variable indicating whether the loan term is 360 months (30 years) |
     |    conforming    |     input     |        int        | Indicates if the loan is conforming (meets government-sponsored enterprise guidelines) |
     | debt_to_income_ratio_missing | input | int | Flag indicating if debt-to-income ratio was missing in the original data |
     | loan_amount_std  |     input     |       float       | Standardized loan amount requested by the borrower       |
     | loan_to_value_ratio_std |  input  |      float       | Standardized ratio of loan amount to property value      |
     | no_intro_rate_period_std | input | float |                                                   |
     | intro_rate_period_std | input | float |                                                   |
     | property_value_std |  input      |      float        | Standardized property value of the home being purchased or refinanced |
     |   income_std     |     input     |       float       | Standardized reported income of the borrower             |
     | debt_to_income_ratio_std | input | float | Standardized ratio of monthly debt payments to monthly income |
     |   high_priced    |    target     |       float       | Target variable: 1 = high priced loan, 0 = not high priced |

   * Source of training data: GWU Blackboard, email jphall@gwu.edu or for more information
   * How training data was divided into training and validation data: 50% training, 25% validation, 25% test
   * Number of rows in training and validation data:
   * Training rows: 112253
   * Validation rows: 48085

## Test Data
   * Source of test data: GWU Blackboard, email jphall@gwu.edu for more information
   * Number of rows in test data: 48085
   * State any differences in columns between training and test data: None

## Model details
   * Columns used as inputs in the final model: 'TERM_360', 'CONFORMING', 'DEBT_TO_INCOME_RATIO_MISSING', 'LOAN_AMOUNT_STD', 'LOAN_TO_VALUE_RATIO_STD', 'NO_INTRO_RATE_PERIOD_STD', 'INTRO_RATE_PERIOD_STD', 'PROPERTY_VALUE_STD', 'INCOME_STD', 'DEBT_TO_INCOME_RATIO_STD'
   * Column(s) used as target(s) in the final model: 'HIGH_PRICED'
   * Type of model: Explainable Boosting Machine (EBM)
   * Software used to implement the model: Python, scikit-learn
   * Version of the modeling software: 0.22.2.post1
   * Hyperparameters or other settings of your model : ['loan_amount_std', 'no_intro_rate_period_std', 'term_360', 'income_std', 'debt_to_income_ratio_missing', 'intro_rate_period_std', 'property_value_std']

## Quantitative Analysis
   * Models were assessed primarily with AUC and AIR. See details below:
     | Metric    | Train AUC | Validation AUC |
     |:--------:|:---------:|:--------------:|
     | AUC Score | 0.7682    | 0.8245         |
   * Table 1. AUC values across data partitions.
     | Group               | Validation AIR |
     |:------------------:|:--------------:|
     | Black vs. White     | 0.791          |
     | Asian vs. White     | 1.151          |
     | Female vs. Male     | 0.957          |
   * Table 2. Validation AIR values for race and sex groups.

## (HINT: Test AUC taken from https://github.com/jphall663/GWU_rml/blob/master/assignments/model_eval_2023_06_21_12_52_47.csv) 


