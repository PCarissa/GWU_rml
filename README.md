# DNSC6330_Assignment 6 - RML Overview

## Basic Information
 1. Person or organization developing model: Patrick Hall, jphall@gwu.edu and Carissa Paul (carissa.paul@gwu.edu)
 2. Model date: August, 2021-2025
 3. Model version: 1.0
 4. License: MIT
 5. Model implementation code: [Group_2.ipynb](https://github.com/PCarissa/GWU_rml/blob/main/assignments/assign_5_template.ipynb)

## Business value 
  The project demonstrates—on real HMDA data—how an **interpretable, bias‑remediated model (EBM)** can flag loans likely to be *high‑priced* (APR ≥ 150 bps) and supply the fairness documentation regulators expect. It gives executives and compliance teams a concrete template for technical review and rapid incident response, aligning with the transparency objective in Assignment 6.

## How the model is designed to be used**  
  *Offline* within the course repository to:  
  - Batch‑score the 2020 HMDA dataset (Assignment 1)  
  - Inspect global & local explanations (Assignment 2)  
  - Audit AIR fairness and apply remediation (Assignment 3)  
  - Probe security via model‑extraction & adversarial tests (Assignment 4)  
  - Stress‑test and debug via recession and residual analysis (Assignment 5)

## Intended Users
   * Primary intended uses: Educational project to demonstrate interpretable and fair ML modeling on HMDA data
   * Primary intended users: Students, researchers, and practitioners interested in responsible machine learning.
   * Out-of-scope use cases: Real-world mortgage decisioning without regulatory compliance checks or human oversight.

* **Additional‑purpose statement**  
  The model **must not** be used for real‑world mortgage decisioning or any production system without full regulatory compliance checks and human oversight; it is intended solely for educational demonstration on the 2020 HMDA training/test files.

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
   * How training data was divided into training and validation data: 70% training, 30% validation.
   * Number of rows in training and validation data:
   * Training rows: 112253
   * Validation rows: 48085

## Test Data
   * Source of test data: GWU Blackboard, email jphall@gwu.edu for more information
   * Number of rows in test data: 19831
   * State any differences in columns between training and test data: None

## Model details
   * Columns used as inputs in the final model: 'TERM_360', 'CONFORMING', 'DEBT_TO_INCOME_RATIO_MISSING', 'LOAN_AMOUNT_STD', 'LOAN_TO_VALUE_RATIO_STD', 'NO_INTRO_RATE_PERIOD_STD', 'INTRO_RATE_PERIOD_STD', 'PROPERTY_VALUE_STD', 'INCOME_STD', 'DEBT_TO_INCOME_RATIO_STD'
   * Column(s) used as target(s) in the final model: 'HIGH_PRICED'
   * Type of model: Explainable Boosting Machine (EBM)
   * Software used to implement the model: Python, scikit-learn
   * Version of the modeling software: 0.22.2.post1
   * Hyperparameters or other settings of your model :
     
            {'max_bins': 128,
             'interactions': 0,
             'learning_rate': 0.05,
             'min_samples_leaf': 10,
             'max_leaves': 7,
             'n_jobs': -1,
             'early_stopping_rounds': 100,
             'random_state': 12345}

## Quantitative Analysis
   * Models were assessed primarily with AUC and AIR. See details below:
     | Metric    | Test AUC | Validation AUC |
     |:--------:|:---------:|:--------------:|
     | AUC Score | 0.7682    | 0.8245         |
   * Table 1. AUC values across data partitions.
     | Group               | Validation AIR |
     |:------------------:|:--------------:|
     | Black vs. White     | 0.791          |
     | Asian vs. White     | 1.151          |
     | Female vs. Male     | 0.957          |
   * Table 2. Validation AIR values for race and sex groups.

## Assignment-wise Results Summary

#### Assignment 1: Model Training on Explainable Models
   * Objective: Train and compare GLM, Monotonic XGBoost, and EBM models on HMDA data
   * Key Models: GLM, XGBoost (monotonic), EBM
   * Validation AUCs: GLM - 0.7698 | XGBoost - 0.7920 | EBM - 0.8250
   * Observations: EBM achieved the best performance among explainable models. GLM served as baseline.

#### Assignment 2: Model Explanation and Feature Importance
   * Objective: Use global/local importance and partial dependence to compare model behaviors
   * Approach: Extract SHAP values, regression coefficients, and EBM scores
   * Visuals: Global bar plots, PDPs for key variables, local explanations at 10th/50th/90th percentiles
   * Observations: Models showed consistent directionality on top features, but differed in strength and interaction detection

#### Assignment 3: Fairness Testing and Remediation (AIR)
   * Objective: Test models for discrimination using AIR; improve without reducing AIR below 0.8 (0.8171)
   * Remediated EBM AIRs: Black vs White - 0.791 | Asian vs White - 1.151 | Female vs Male - 0.957
   * Observations: Grid search helped improve fairness while retaining model performance

#### Assignment 4: Red Teaming and Adversarial Testing
   * Objective: Simulate adversarial attacks on model via model extraction and counterexamples
   * Methods: Decision tree model extraction, adversarial input generation, attack simulation
   * Outcomes: Exposed model vulnerabilities to feature flipping and response skew
   * Observations: EBM showed resilience to mild attacks but lacked protection against well-crafted inputs

#### Assignment 5: Debugging and Robustness (Final Remediated EBM)
   * Objective: Stress test EBM under recession and improve residual error patterns
   * Stress Test Result: AUC degraded under recession conditions
   * Residual Fixes: Outlier removal and reweighting improved stability
   * EBM retrained with AUC - 0.8102 | EBM under-sampled AUC - 0.8077 | True Test - 0.8205
   * Observations: Final model achieved optimal tradeoff between fairness and performance


#### Figures 

* Assignment 1

![image](https://github.com/user-attachments/assets/98416845-2509-458a-9bec-4f3d5e3f57a9)

Figure 1. Histograms data exploration.

![image](https://github.com/user-attachments/assets/4023506c-11a1-4fd9-a0cc-4c908954ce2b)

Figure 2. Heatmaps correlations.

* Assignment 2

![image](https://github.com/user-attachments/assets/c93e2d8f-8e08-459f-86cf-40fac21f842d)

Figure 3. Global feature importance.

![image](https://github.com/user-attachments/assets/90ac6451-7707-465a-aeaa-1fb5af298f28)

Figure 4. Local feature importance

![image](https://github.com/user-attachments/assets/f9ed6a3d-8608-42ed-b4bc-c1842151c4df)

Figure 5. Partial dependence feature

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

### Ethical Considerations
##### Potential Negative Impacts:
* The adjusted EBM model may still carry indirect biases, even with improved AIR parity.
* Excessive reliance on fairness metrics like AIR may overlook other imbalances such as group-level precision and recall.
* Technical issues like float precision or unstable binning may cause scoring inconsistencies.
* Practical risk: during economic downturns, borrowers could be unjustly labeled as high-risk, limiting their credit access.

##### Potential Uncertainties:
* Changes in borrower behavior or regulations (e.g., interest rate caps) may reduce the model’s generalizability.
* Unforeseen interactions between features might produce unexpected behavior during real-time use.
* Without active monitoring, the model may face drift or be vulnerable to adversarial manipulation in production.

##### Unexpected Results:
* The updated EBM showed a slight drop in AUC but a gain in AIR, illustrating the tradeoff between fairness and accuracy.
* The feature no_intro_rate_period_std had an unexpectedly high impact in some EBM runs.







