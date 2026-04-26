
# Bonus Multi-Class Model Discussion

The multi-class model predicts four classes:
**Gold**, **Silver**, **Bronze**, and **None**.

## Performance Metrics

- Accuracy: **0.551**
- Weighted F1: **0.624**
- Macro F1: **0.321**

## Why This Is Harder Than Binary Prediction

The binary medal model only asks whether an athlete medals at all.

This multi-class version must predict the exact podium result:
Gold vs Silver vs Bronze vs None.

That is substantially harder because Gold, Silver, and Bronze athletes often have very similar profiles in:

- World Cup preseason points
- Training load
- VO2max
- Olympic experience
- Country strength

Very small real-world margins can separate first from second place.

## Where The Model Struggles Most

The confusion matrix shows that most mistakes occur between neighbouring podium classes such as:

- Gold predicted as Silver
- Silver predicted as Bronze
- Bronze predicted as Silver

This is expected because these athletes are all elite performers.

The **None** class is generally easiest to identify because non-medalists are more numerous and usually farther from podium-level performance signals.

## Final Interpretation

The multi-class model is a useful advanced extension, but exact medal colour prediction is naturally more difficult than binary medal prediction.

For talent identification and funding decisions, the binary medal model remains more reliable and operationally practical.
