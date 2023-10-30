---
title: t9k.em.lightning.EMCallback
---

# t9k.em.lightning.EMCallback

```python
EMCallback(run: t9k.em.run.Run)
```

Logs metrics and retrieves hyperparameters.

## Examples

```python
trainer = Trainer(max_epochs=10,
                  callbacks=EMCallback(run))
```

## Args

* **run** (*t9k.em.run.Run*)

    Run that the training and testing process belongs to.

## Ancestors

* `lightning.pytorch.callbacks.callback.Callback`
