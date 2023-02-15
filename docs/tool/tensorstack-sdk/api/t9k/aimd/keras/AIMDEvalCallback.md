---
title: t9k.aimd.keras.AIMDEvalCallback
---

# t9k.aimd.keras.AIMDEvalCallback

```python
AIMDEvalCallback(trial: t9k.aimd.trial.Trial)
```

Logs testing metrics.

## Examples

```python
from t9k.aimd.keras import AIMDEvalCallback

model.evaluate(test_images,
               test_labels,
               callbacks=AIMDEvalCallback(trial))
```

## Args

* **trial** (*t9k.aimd.trial.Trial*)

    Trial that the testing process belongs to.

## Ancestors

* `keras.callbacks.Callback`
