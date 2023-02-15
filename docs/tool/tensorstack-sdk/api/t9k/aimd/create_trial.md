---
title: t9k.aimd.create_trial
---

# t9k.aimd.create_trial

```python
create_trial(trial_path: Optional[str] = None, trial_name: Optional[str] = None, trial_params: Optional[dict] = None, folder_id: Optional[str] = None, folder_path: Optional[str] = None, make_folder: Optional[bool] = None, conflict_strategy: Optional[str] = None) ‑> t9k.aimd.trial.Trial
```

Creates and initializes a new Trial.

## Examples

Basic usage:
```python
from t9k import aimd

trial = aimd.create_trial(trial_name='cnn_keras',
                          folder_path='image_classification/mnist')
```

Provide initial parameters of Trial:
```python
params = {
    'batch_size': 32,
    'epochs': 1,
    'learning_rate': 0.001,
    'conv_channels1': 32,
    'conv_channels2': 64,
    'conv_channels3': 64,
    'conv_kernel_size': 3,
    'maxpool_size': 2,
    'linear_features1': 64,
}

trial = aimd.create_trial(trial_name='cnn_keras',
                          trial_params=params,
                          folder_path='image_classification/mnist')
```

Provide Trial config file:
```python
trial = aimd.create_trial(trial_path='./trial.yaml')
```
where the config file `trial.yaml` is like:
```python
trial_name: cnn_keras
folder_path: image_classification/mnist
trial_params:
  batch_size: 32
  epochs: 1
  learning_rate: 0.001
  conv_channels1: 32
  conv_channels2: 64
  conv_channels3: 64
  conv_kernel_size: 3
  maxpool_size: 2
  linear_features1: 64
```

## Args

* **trial_path** (*Optional[str]*)

    Local path of the Trial to load. If this arg is provided, all of the following args will be loaded from config file if they are not provided.

* **trial_name** (*Optional[str]*)

    Name of the Trial.

* **trial_params** (*Optional[dict]*)

    Initial hyperparameters of the Trial.

* **folder_id** (*Optional[str]*)

    ID of folder to which the Trial will be uploaded.

* **folder_path** (*Optional[str]*)

    Path of the folder to which the Trial will be uploaded. If `folder_id` is provided, `folder_path` will not be used; if neither `folder_id` or `folder_path` is provided, the Trial will be uploaded to folder with path `/default`.

* **make_folder** (*Optional[bool]*)

    If True and folder with `folder_path` does not exist, make the folder and parent folders as needed. Default to False if `trial_path` is not provided.

* **conflict_strategy** (*Optional[str]*)

    Strategy adopted when a Trial with the same name as the Trial to be uploaded already exists in the folder, must be `'skip'`, `'error'`, `'new'` or `'replace'`. If `'skip'`, skip the upload; if `'error'`, error out; if `'new'`, upload with the local name of Trial; if `'replace'`, delete the existing Trial and upload. Default to 'new' if `trial_path` is not provided.

## Returns

A Trial instance created and initialized.
