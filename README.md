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

##### (HINT: Test AUC taken from https://github.com/jphall663/GWU_rml/blob/master/assignments/model_eval_2023_06_21_12_52_47.csv) 

#### Figures 

* Assignment 1
![image](https://github.com/user-attachments/assets/98416845-2509-458a-9bec-4f3d5e3f57a9)

Figure 1. Histograms.

![image](https://github.com/user-attachments/assets/4023506c-11a1-4fd9-a0cc-4c908954ce2b)

Figure 2. Heatmaps.

* Assignment 2

![image](https://github.com/user-attachments/assets/c93e2d8f-8e08-459f-86cf-40fac21f842d)

Figure 3. Histograms.

![image](https://github.com/user-attachments/assets/90ac6451-7707-465a-aeaa-1fb5af298f28)

Figure 4. Bar graphs

![image](https://github.com/user-attachments/assets/f9ed6a3d-8608-42ed-b4bc-c1842151c4df)

Figure 5. Line graphs

* Assignment 3

![image](https://github.com/user-attachments/assets/a883ea20-141f-4132-9a0a-e7e4744ff301)

Figure 6. AIR V/S AUC EBM

* Assignment 4

![image](https://github.com/user-attachments/assets/d4c025ff-f676-4045-88f9-2e7d8020529e)

Figure 7. Simulated data


![image](https://github.com/user-attachments/assets/f3999e5b-cb4e-48e8-a0f3-f0bfaeff6c90)

Figure 8. Stolen model

![image](https://github.com/user-attachments/assets/110054f1-830c-4c3b-a325-8ff32d75e0cf)

Figure 9. Distributed random forest

* Assignment 5

![image](https://github.com/user-attachments/assets/da28a198-35e0-4b1d-a68b-efc8d358011d)

Figure 10. Simulate recession conditions in validation data

![image](https://github.com/user-attachments/assets/3db04701-fdb3-48cc-aa63-cb4a7322641d)

Figure 11. Global Logloss Residuals










