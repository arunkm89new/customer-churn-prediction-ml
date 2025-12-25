# customer-churn-prediction-ml

Problem type: Supervised Learning → Binary Classification Goal: Predict whether a customer will churn (Yes/No)

Model Evaluation:

# Accuracy:

Without Regularization:
Accuracy on training set: 0.9296875 Accuracy on test set: 0.8046140195208518
Identified:
High variance - Over fitting

After applying L2 regualrization , gap bettween training and testing accuracy sginificantly reduced
Accuracy on training set: 0.8196022727272727
Accuracy on test set: 0.8044365572315882

This indicating model generalizes well and not overfit.

# Confusion Matrix

array([[3740,  382],
       [ 720,  793]])

Model predicts 720 not churn /missed churns.

# claasification report

            precision    recall  f1-score   support

           0       0.84      0.91      0.87      4122
           1       0.67      0.52      0.59      1513

    accuracy                           0.80      5635

macro avg 0.76 0.72 0.73 5635
weighted avg 0.79 0.80 0.80 5635

Class 1 (churn)
When model predict 67% is correct
it catches only 52% of actual churn.

# Fine Tuning

1. Adding Class weight

# Confusion Matrix

array([[3038, 1084],
       [ 337, 1176]])

Result : Earlier missed more churn, now catches most churns. still 1084 false postive (predict as churn)

2.  Classification report

                precision    recall  f1-score   support

               0       0.90      0.74      0.81      4122
               1       0.52      0.78      0.62      1513

        accuracy                           0.75      5635

    macro avg 0.71 0.76 0.72 5635
    weighted avg 0.80 0.75 0.76 5635

Result:
Now Model catches 78% of actual churns.

Summary:

After applying class weighting, the model significantly reduced missed churners while increasing false alarms, reflecting a deliberate trade-off to prioritize churn detection.

2. Fine Tuning with Threshold
   ### Decision Threshold Selection

The logistic regression model outputs churn probabilities.
Instead of using the default threshold of 0.5, the decision threshold was tuned to balance precision and recall.
A threshold of 0.45 was selected, as it significantly improved recall for churners while maintaining acceptable precision.
This choice reduces missed churners and aligns better with business priorities where retaining at-risk customers is more important than avoiding false alarms.

From evaluation:
Why 0.45 is best:

Recall is high (82% churners caught)

Precision still reasonable

F1-score is maximized

Fewer false alarms than lower thresholds

This is a balanced, defensible decision.

The final model achieved a ROC-AUC score of 0.84, indicating strong ability to distinguish between churners and non-churners across different decision thresholds. This demonstrates robust model performance despite class imbalance.

## Conclusion

This project addressed customer churn prediction as a supervised binary classification problem using logistic regression.
An end-to-end machine learning workflow was implemented, including exploratory data analysis, feature preprocessing, model training, evaluation, and fine-tuning.

A baseline logistic regression model showed reasonable accuracy but suffered from low recall for churners, indicating that many customers who eventually left were not identified.
To address this, L2 regularization was applied to control overfitting, and class-weight balancing was introduced to handle class imbalance and emphasize the importance of detecting churners.

Further improvements were achieved through decision threshold tuning.
By lowering the default threshold from 0.5 to 0.45, the model significantly increased recall for churners while maintaining acceptable precision.
This reduced the number of missed churners and aligned the model’s behavior with real-world business priorities, where retaining at-risk customers is more critical than avoiding false alarms.

Overall, the final model demonstrates a balanced bias–variance trade-off, strong generalization performance, and an evaluation strategy focused on meaningful business outcomes rather than accuracy alone.
Future improvements could include feature engineering, non-linear models such as decision trees or ensemble methods, and cost-sensitive optimization based on business impact.
