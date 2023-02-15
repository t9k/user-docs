---
title: t9k.aimd.keras.AIMDFitCallback
---

# t9k.aimd.keras.AIMDFitCallback

```python
AIMDFitCallback(trial: t9k.aimd.trial.Trial)
```

Logs training metrics and retrieves hyperparameters.

## Examples

```python
from t9k.aimd.keras import AIMDFitCallback

model.fit(train_images,
          train_labels,
          epochs=10,
          validation_split=0.2,
          callbacks=AIMDFitCallback(trial))
```

## Args

* **trial** (*t9k.aimd.trial.Trial*)

    Trial that the training process belongs to.

## Ancestors

* `keras.callbacks.Callback`
