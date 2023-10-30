---
title: t9k.em.keras.EMEvalCallback
---

# t9k.em.keras.EMEvalCallback

```python
EMEvalCallback(run: t9k.em.run.Run)
```

Logs testing metrics.

## Examples

```python
from t9k.em.keras import EMEvalCallback

model.evaluate(test_images,
               test_labels,
               callbacks=EMEvalCallback(run))
```

## Args

* **run** (*t9k.em.run.Run*)

    Run that the testing process belongs to.

## Ancestors

* `keras.src.callbacks.Callback`
