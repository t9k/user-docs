---
title: t9k.em.create_run
---

# t9k.em.create_run

```python
create_run(config_path: Optional[str] = None, name: str = 'default', hparams: Optional[Dict[str, Any]] = None, labels: Optional[Sequence[str]] = None, description: str = '', auto_upload: bool = False, folder: str = 'default', make_folder: bool = False, conflict_strategy: str = 'new') ‑> t9k.em.run.Run
```

Creates and initializes a new Run.

The local files of Run are placed under the parent directory specified by the environment variable `EM_RUN_PARENT_DIR` (default is relative path `.em/runs`).

## Examples

Basic usage:
```python
from t9k import em

run = em.create_run(name='cnn_keras',
                    folder='cv/image-classification/mnist')
```

Provide initial parameters of Run:
```python
hparams = {
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

run = em.create_run(name='cnn_keras',
                    hparams=hparams,
                    folder_path='cv/image-classification/mnist')
```

Provide a Run config file:
```python
run = em.create_run(config_path='./run_config.yaml')
```
where the config file `run_config.yaml` is like:
```python
name: cnn_keras
hparams:
  batch_size: 32
  epochs: 1
  learning_rate: 0.001
  conv_channels1: 32
  conv_channels2: 64
  conv_channels3: 64
  conv_kernel_size: 3
  maxpool_size: 2
  linear_features1: 64
labels:
- Keras
description: Train a simple CNN model that classifies images of handwritten digits.
```

## Args

* **config_path** (*Optional[str]*)

    Local path of the Run config file. For all of the following args, the values parsed from the config file take precedence over values passed in.

* **name** (*str*)

    Name of the Run.

* **hparams** (*Optional[Dict[str, Any]]*)

    Initial hyperparameters of the Run.

* **labels** (*Optional[Sequence[str]]*)

    Labels of the Run.

* **description** (*str*)

    Description of the Run.

* **auto_upload** (*bool*)

    Whether to upload the Run and its data automatically and asynchronously. If False, all of the following args will not be used.

* **folder** (*str*)

    Path of the Folder to which the Run is uploaded. If the provided path does not start with '/', `/<current-user>/` is prepended to it. If `auto_upload` is False, this arg will not be used.

* **make_folder** (*bool*)

    If True and Folder with path `folder` does not exist, make the Folder and parent Folders as needed. If `auto_upload` is False, this arg will not be used.

* **conflict_strategy** (*str*)

    Strategy adopted when a Run with the same name as the Run to be uploaded already exists in the Folder, must be 'skip', 'error', 'new' or 'replace'. If 'skip', skip the upload; if 'error', error out; if 'new', upload with the alternative name of Run; if 'replace', delete the existing Run and upload. If `auto_upload` is False, this arg will not be used.

## Returns

A Run instance created and initialized.
