---
title: t9k.em.keras.EMFitCallback
---

# t9k.em.keras.EMFitCallback

```python
EMFitCallback(run: t9k.em.run.Run)
```

Logs training metrics and retrieves hyperparameters.

## Examples

```python
from t9k.em.keras import EMFitCallback

model.fit(train_images,
          train_labels,
          epochs=10,
          validation_split=0.2,
          callbacks=EMFitCallback(run))
```

## Args

* **run** (*t9k.em.run.Run*)

    Run that the training process belongs to.

## Ancestors

* `keras.src.callbacks.Callback`
