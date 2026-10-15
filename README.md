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

#### Conclusion

All of the models have a really close tuned validation score but for this porpose i would probably choose Olblique random forest as it's mean is the best and it would have the computational cost that adaboost has.

I think they match the trees used in each model and to justify we can look at the chose hyperparameters for the oblique random forest where the  chosen ones where the max_depth, min_samples_leaf and n_components in a model which is deep and the hyperparameters chosen for adaboost, which uses shallow trees and chose estimator_max_depth, n_estimators and learning_rate.

I would report the neted CV mean for the obique random forest as it seems to be a fast algorithm as well as a good algorithm, with a high precision and a fast training and validating running time.
