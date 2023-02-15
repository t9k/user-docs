---
title: t9k.aimd.upload_trial
---

# t9k.aimd.upload_trial

```python
upload_trial(trial_path: Union[str, Sequence[str], None] = None, trial_dir: Optional[str] = None, trial_name: Union[str, Sequence[str], None] = None, folder_id: Optional[str] = None, folder_path: Optional[str] = None, make_folder: bool = False, conflict_strategy: Optional[str] = None) ‑> None
```

Uploads one or multiple Trials that are saved locally.

For parameters `folder_id`, `folder_path` and `make_folder`, the values of the arguments passed in take precedence over values parsed from `_upload` field in Trial data file.

## Examples

Upload one Trial by its path:
```python
aimd.upload_trial(trial_path=
    '.aimd/trials/mnist_keras_220823_194728_4e48t2')
# or
aimd.upload_trial(trial_path=
    '/path/to/workspace/.aimd/trials/mnist_keras_220823_194728_4e48t2')
```

Upload all Trials under a directory:
```python
aimd.upload_trial(trial_dir='.aimd/trials')
```

Upload one Trial by its alternative name:
```python
aimd.upload_trial(trial_name='mnist_keras_220823_194728_4e48t2')
```

Upload multiple Trials by their alternative names:
```python
aimd.upload_trial(trial_name=['mnist_keras_220823_194728_4e48t2',
                              'mnist_torch_220823_195814_vjo18w'])
```

Provide arguments that are not provided in Trial metadata file:
```python
aimd.upload_trial(trial_name='mnist_keras_220823_194728_4e48t2',
                  folder_path='image_classification/mnist')
```

## Args

* **trial_path** (*Union[str, Sequence[str], None]*)

    Local path of the Trial to be uploaded, can be a path of one Trial or a sequence of paths of multiple Trials.

* **trial_dir** (*Optional[str]*)

    Local path of the directory that contains one or multiple Trials.

* **trial_name** (*Union[str, Sequence[str], None]*)

    Name of the Trial to be uploaded, can be a name of one Trial or a sequence of names of multiple Trials. `trial_name` can be name or alternative name of Trial, this function will search `TRIAL_PATH` for sub-directory whose name matches `trial_name`.

* **folder_id** (*Optional[str]*)

    ID of the folder to which the Trial is uploaded.

* **folder_path** (*Optional[str]*)

    Path of the folder to which the Trial is uploaded. If `folder_id` is provided, `folder_path` will not be used; if neither `folder_id` or `folder_path` is provided, the Trial will be uploaded to folder with path `/default`.

* **make_folder** (*bool*)

    If True and folder with `folder_path` does not exist, make the folder and parent folders as needed.

* **conflict_strategy** (*Optional[str]*)

    Strategy adopted when a Trial with the same name as the Trial to be uploaded already exists in the folder, must be `'skip'`, `'error'`, `'new'` or `'replace'`. If `'skip'`, skip the upload; if `'error'`, error out; if `'new'`, upload with the local name of Trial; if `'replace'`, delete the existing Trial and upload.
