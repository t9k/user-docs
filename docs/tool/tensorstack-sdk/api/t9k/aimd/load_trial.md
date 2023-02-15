---
title: t9k.aimd.load_trial
---

# t9k.aimd.load_trial

```python
load_trial(trial_path: Optional[str] = None, trial_name: Optional[str] = None) ‑> t9k.aimd.trial.Trial
```

Loads a Trial from local by its name or path.

Priorities of the arguments: `trial_path` > `trial_name`.

If `trial_path` is provided, load from this local path.

If `trial_name` is provided, this function will search `TRIAL_PATH` for every sub-directory whose name matches `trial_name`. If 1 matches, load this Trial; if 0 or 2 or more match, raise a RuntimeError.

It is recommended to pass in the path or the alternative name of Trial to avoid ambiguity.

## Examples

Load by path:
```python
aimd.load_trial(trial_path=
    '.aimd/trials/mnist_keras_220823_194728_4e48t2')
```

Load by alternative name:
```python
aimd.load_trial(trial_name='mnist_keras_220823_194728_4e48t2')
```

Load by name:
```python
aimd.load_trial(trial_name='mnist_keras')  # might match multiple
```

## Args

* **trial_path** (*Optional[str]*)

    Local path of the Trial to load from.

* **trial_name** (*Optional[str]*)

    Name of the Trial to load by.

## Returns

A Trial instance loaded from local.
