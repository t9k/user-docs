---
title: t9k.aimd.lightning.AIMDCallback
---

# t9k.aimd.lightning.AIMDCallback

```python
AIMDCallback(trial: t9k.aimd.trial.Trial)
```

Logs metrics and retrieves hyperparameters.

## Examples

```python
trainer = Trainer(max_epochs=10,
                  callbacks=AIMDCallback(trial))
```

## Args

* **trial** (*t9k.aimd.trial.Trial*)

    Trial that the training and testing process belongs to.

## Ancestors

* `pytorch_lightning.callbacks.base.Callback`
