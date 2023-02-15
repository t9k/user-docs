---
title: t9k.tuner.keras.AutoTuneEvalCallback
---

# t9k.tuner.keras.AutoTuneEvalCallback

```python
AutoTuneEvalCallback(metric='loss')
```

Logs testing metrics for AutoTune.

## Examples

```python
from t9k.tuner.keras import AutoTuneEvalCallback

model.evaluate(test_images,
               test_labels,
               callbacks=AutoTuneEvalCallback(metric='accuracy'))
```

## Args

* **metric**

    Name of the metric that is reported to tuner.

## Ancestors

* `keras.callbacks.Callback`
