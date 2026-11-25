# Baseline Predictive Pipeline -- ETAI

# 20260647 Miguel Lemos

## Comparing LR and DT

DT got a clear advantage in training data but its worse in the test data because of overfitting, LR is better has it as better accuracy in the test data even with a lower training accuracy

### DT 

Train accuracy: 0.829
Test accuracy:  0.631

### LR

Train accuracy: 0.678
Test accuracy:  0.679

## Results after Data cleanup and Preprocessing

### DT

Train accuracy: 0.792
Test accuracy:  0.613

### LR

Train accuracy: 0.676
Test accuracy:  0.657

## Comparison with week2's results

After the Data cleanup we can observe a drop in the accuracy of each model in traning and in testing.

At this time **LR** is still the best model for this purpose.

## Week 4 - Results after Cross Validation

### LR

Train accuracy: 0.677 
Validation accuracy: 0.675

### DT 

Train accuracy: 0.701 
Validation accuracy: 0.600

### RF

Train accuracy: 0.731
Validation accuracy: 0.647

## Week 5 - Hyperparameters tuning and nested Cross Validation

| Model | Default: CV mean ± std | Tuned: nested CV mean ± std | Tuning score (best trial) | Optimism | Chosen hyperparameters |
|---|---|---|---|---|---|
| Decision tree | 0.590 ±0.020 | 0.670 ±0.015 | 0.679 | +0.005 | {'model__max_depth': 9, 'model__min_samples_leaf': 95, 'model__criterion': 'gini'} |
| Logistic regression | 0.600 ±0.028 | 0.667 ±0.014 | 0.678 | +0.009 | {'max_depth': 19, 'min_samples_leaf': 72, 'criterion': 'gini'} |
| Random forest | 0.644 ±0.017 | 0.680 ±0.014 | 0.685 | +0.003 | {'model__n_estimators': 91, 'model__max_depth': 15, 'model__min_samples_leaf': 59, 'model__max_features': 0.5} |

#### Conclusion for week 5

Tuning has a positive impact in all models but the one who benefited the most was the decision tree model in which the gai. was bigger than the fold-to-fold std.

The best model is now Random Forests oposed to Logistic Regression which was better before.

The number I would report is the nested CV mean obtained as it reports the average precision, rather than the best score which can represent an outlier.

## Week 6 - Ensembles and Feature Engeneering

| Model | Default: CV mean ± std (gap) | Tuned: nested CV mean ± std (gap) | Tuning score (best trial) | Chosen hyperparameters |
|---|---|---|---|---|
| Logistic regression | 0.675 ±0.012 | — | — | — |
| Decision tree | 0.603 ±0.020 | 0.673 ±0.015 | 0.686 | {'model__max_depth': 9, 'model__min_samples_leaf': 93, 'model__criterion': 'gini'} |
| Random forest | 0.638 ±0.026 | 0.682 ±0.016 | 0.699 | {'model__max_depth': 18, 'model__min_samples_leaf': 34, 'model__max_features': 0.5} |
| Oblique random forest | 0.642 ±0.013 | 0.683 ±0.015 | 0.697 | {'model__estimator__tree__max_depth': 3, 'model__estimator__tree__min_samples_leaf': 3, 'model__estimator__project__n_components': 9} |
| AdaBoost | 0.668 ±0.013 | 0.683 ±0.015 | 0.698 | {'model__estimator__max_depth': 5, 'model__n_estimators': 236, 'model__learning_rate': 0.02335065047830805} |

#### Conclusion for week 6

All of the models have a really close tuned validation score but for this porpose i would probably choose Olblique random forest as it's mean is the best and it would have the computational cost that adaboost has.

I think they match the trees used in each model and to justify we can look at the chose hyperparameters for the oblique random forest where the  chosen ones where the max_depth, min_samples_leaf and n_components in a model which is deep and the hyperparameters chosen for adaboost, which uses shallow trees and chose estimator_max_depth, n_estimators and learning_rate.

I would report the neted CV mean for the obique random forest as it seems to be a fast algorithm as well as a good algorithm, with a high precision and a fast training and validating running time.

## Week 7 - New Boosting Methods and New Metrics

| Model | Tuned | Floor | Selection Metric (ROC AUC) |
|---|---|---|---|
| Gradient Boosting | True | 0.5 | 0.7279 ± 0.0147 |
| Gradient Boosting | False | 0.5 | 0.7275 ± 0.0159 |
| Random Forest | True | 0.5 | 0.7273 ± 0.0127 |
| Oblique Random Forest | True | 0.5 | 0.7273 ± 0.0141 |
| AdaBoost | True | 0.5 | 0.7262 ± 0.0155 |
| Logistic Regression | False | 0.5 | 0.7188 ± 0.0137 |
| Logistic Regression | True | 0.5 | 0.7184 ± 0.0134 |
| AdaBoost | False | 0.5 | 0.7180 ± 0.0153 |
| Decision Tree | True | 0.5 | 0.7179 ± 0.0185 |
| Hist Gradient Boosting | False | 0.5 | 0.7150 ± 0.0212 |
| Naive Bayes | False | 0.5 | 0.6891 ± 0.0106 |
| Random Forest | False | 0.5 | 0.6863 ± 0.0145 |
| Oblique Random Forest | False | 0.5 | 0.6779 ± 0.0185 |
| Decision Tree | False | 0.5 | 0.6078 ± 0.0251 |
| Dummy | False | 0.5 | 0.5000 ± 0.0000 |

### Conclusion for week 8

I chose ROC AUC as the selection metric because it's robust to unbalanced classes and it's different scoring methodology compared to, for example accuracy, it doesn't depend on thresholds.

## Week 8 - Feature Selection

| Model | Tuned | Floor | Selection Metric (ROC AUC) | Feature Selection
|---|---|---|---|---|
| XGBoost | False | 0.5 | 0.7041 ± 0.0180 | False
| XGBoost | False | 0.5 | 0.7034 ± 0.0207 | True

### Conclusions for week 8

Feature Selection didn't create a big difference in the ROC AUC score yet this could be because of the parameters chosen, yet this has shown that Feature Selection didn't add much to the scoren xgboost could already achieve.

All of the features where kept with the parameters given to the Feature Selection model. The features kept where: {juv_other_count, priors_count, juv_misd_count, sex, age_cat, c_charge_degree, juv_fel_count, age, priors_count_was_missing, c_charge_degree_was_missing}

Even the corrected pair test dindn't get affected that much.

I would probably not keep selection on as it's consuming computational resources while not doing much for the model.

## Week 9 - New Data

I chose Option A for this week's challenge

### Beyond COMPAS - New Data

#### Issues encountered

##### Problem 1
Description: At first main wasn't using the right config
Fix: Added sys.argv to catch the argument from the terminal

##### Problem 2
Description: Column names not on the dataframe, namely race or sex when they're selected int he sensitive attributes
Fix: The feature selected for sensitive attribute cannot be in the listed features

##### Problem 3
Description: score_text key error
Fix: Changes in the fairness report

#### Runs

| Run | Model | Tuned | Encoder | Scaler | Tuned Params | Mean ROC AUC | Std | Untuned | Fold 1 | Fold 2 | Fold 3 | Fold 4 | Fold 5 |
| :--- | :--- | :---: | :--- | :--- | :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| `20261117_113653` | `xgboost` | True | target | standard | `{'model__max_depth': 2, 'model__n_estimators': 293, 'model__learning_rate': 0.1062}` | **0.9108** | 0.0146 | 0.8994 | 0.9082 | 0.9106 | 0.9342 | 0.8938 | 0.9074 |
| `20261117_120820` | `xgboost` | True | target | standard | `{'model__max_depth': 2, 'model__n_estimators': 258, 'model__learning_rate': 0.1075}` | **0.9108** | 0.0152 | 0.9004 | 0.9125 | 0.9090 | 0.9347 | 0.8935 | 0.9043 |
| `20261117_113228` | `xgboost` | True | target | standard | `{'model__max_depth': 2, 'model__n_estimators': 104, 'model__learning_rate': 0.2722}` | **0.9103** | 0.0145 | 0.8968 | 0.9087 | 0.9138 | 0.9325 | 0.8937 | 0.9029 |
| `20261117_122405` | `xgboost` | True | target | standard | `{'model__max_depth': 4, 'model__n_estimators': 169, 'model__learning_rate': 0.0637}` | **0.9100** | 0.0167 | 0.9002 | 0.9099 | 0.9112 | 0.9338 | 0.8866 | 0.9085 |
| `20261117_120436` | `xgboost` | True | target | standard | `{'model__max_depth': 2, 'model__n_estimators': 137, 'model__learning_rate': 0.2411}` | **0.9092** | 0.0165 | 0.9010 | 0.9055 | 0.9078 | 0.9353 | 0.8894 | 0.9080 |
| `20261117_122255` | `xgboost` | False | target | standard | — | **0.9017** | 0.0142 | 0.9017 | 0.8935 | 0.9024 | 0.9255 | 0.8892 | 0.8978 |
| `20261117_095137` | `logistic_regression` | True | target | standard | `{'model__C': 15.7419}` | **0.8960** | 0.0147 | 0.8958 | 0.8930 | 0.8965 | 0.9185 | 0.8775 | 0.8946 |
| `20261117_094526` | `logistic_regression` | False | target | standard | — | **0.8959** | 0.0146 | 0.8959 | 0.8931 | 0.8964 | 0.9183 | 0.8773 | 0.8946 |
| `20261117_094924` | `logistic_regression` | False | target | standard | — | **0.8950** | 0.0148 | 0.8950 | 0.8928 | 0.8921 | 0.9184 | 0.8773 | 0.8947 |
| `20261117_095015` | `logistic_regression` | False | target | standard | — | **0.8950** | 0.0147 | 0.8950 | 0.8928 | 0.8921 | 0.9180 | 0.8772 | 0.8947 |

The features kept were `age, workclass, education_num, marital_status, occupation, relationship, sex, capital_gain, capital_loss, hours_per_week, native_country, v01, v02, v03, v04, v05, v06, v07,v08, v09, v10, v11, v12, v13, v14, v15, v16, v17, v18, v19, v20, v21, v22, v23, v24, v25, capital_gain_was_missing`

## Conclusion for Week 9

The hardest part of this delivery was adding the testing with the new csv. 
Overall adapting the pipeline to new data was reletively simple and required minimal changes.

I was having some dificulty achieving the scores but then i changed the model to xgboost instead of the linear regression i was using to be faster, and I instantly got the target scores I had been chasing.

## Week 10 - Missing Values and Deployment

#### Missing Values

##### Imputer runs

| Run | Model | Tuned | Encoder | Scaler | Tuned Params | Mean ROC AUC | Std | Untuned | Fold 1 | Fold 2 | Fold 3 | Fold 4 | Fold 5 | Imputer |
| :--- | :--- | :---: | :--- | :--- | :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :--- |
| `20261118_122628` | `xgboost` | False | target | standard | — | **0.7091** | 0.0167 | 0.7091 | 0.7110 | 0.6822 | 0.7186 | 0.7074 | 0.7262 | knn |
| `20261119_123722` | `xgboost` | False | target | standard | — | **0.7065** | 0.0148 | 0.7065 | 0.7038 | 0.6850 | 0.7123 | 0.7054 | 0.7259 | median |
| `20261118_124637` | `xgboost` | False | target | standard | — | **0.7060** | 0.0151 | 0.7060 | 0.7018 | 0.6840 | 0.7177 | 0.7037 | 0.7225 | iterative |
| `20261119_123649` | `xgboost` | False | target | standard | — | **0.7057** | 0.0127 | 0.7057 | 0.7044 | 0.6881 | 0.7137 | 0.7010 | 0.7214 | mean |

##### Which imputer should we keep?

We should keep all of the imputers because in certain situations they might be better for us, but for this purpose we should keep knn as it showed the best ROC-AUC.

I couldn't test random_forest as a imputer because I kept getting a the same `Early stopping criteria not reached` error all of the time.

#### Predicting new data

The command for it is `python predict.py data/compas_new_people.csv predictions.csv` and it's output is a predictions.csv with the predictions of the model supplied to the function.

## Week 11 - Anomaly Detection

This week I added the anomaly detetion to the pipeline, along with their own config section and ran it multiple times experimenting with the affects of each algorithm.

## Conclusion for Week 11

The best result I got was using no anomaly detetion at all, so we can conclude that the models benefit from the extra data even if some of it are outliers.

With anomaly detetion turned on we saw that isolation forest got better results for the model compared to LOF.