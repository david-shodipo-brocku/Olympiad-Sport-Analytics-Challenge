
# Task 3 Confusion Matrix Interpretation

Using the best leakage-safe model (log_reg) at threshold 0.48:

True negatives: 44 athletes were correctly predicted as non-medalists.
False positives: 13 athletes were predicted to medal but did not. These are over-selection risks — wasted high-performance resources.
False negatives: 4 athletes actually medalled but the model missed them. These are the most costly errors for talent identification because we lose real medal opportunities.
True positives: 17 athletes were correctly identified as medalists.

Because medalists are the minority class, accuracy alone is not enough.
A naive model that predicts no medal for everyone would be highly accurate but would catch zero true positives.
Precision, recall, F1, AUC, and the confusion matrix must all be read together to understand model quality.
