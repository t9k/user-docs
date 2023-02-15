---
title: t9k.tuner.keras.AutoTuneFitCallback
---

# t9k.tuner.keras.AutoTuneFitCallback

```python
AutoTuneFitCallback(metric='loss')
```

Logs training metrics for AutoTune.

## Examples

```python
from t9k.tuner.keras import AutoTuneFitCallback

model.fit(train_images,
          train_labels,
          epochs=10,
          validation_split=0.2,
          callbacks=AutoTuneFitCallback(metric='accuracy'))
```

## Args

* **metric**

    Name of the metric that is reported to tuner.

## Ancestors

* `keras.callbacks.Callback`
