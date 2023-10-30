---
title: t9k.em.upload
---

# t9k.em.upload

```python
upload(path: str, folder: str = 'default', make_folder: bool = False, conflict_strategy: str = 'new') ‑> None
```

Upload local Runs or Artifacts.

## Examples

Upload a Run by its local directory:
```python
em.upload(path='.em/runs/cnn_keras_220823_194728_4e48t2')
```

Upload all Artifact under the parent directory:
```python
em.upload(path='.em/artifacts')
```

Specify the path of Folder to which the Run is uploaded:
```python
em.upload(path='.em/runs/cnn_keras_220823_194728_4e48t2',
              folder='image_classification/mnist')
```

## Args

* **path** (*str*)

    Local directory of the Run to be uploaded, or parent directory that contains one or more Runs.

* **folder** (*str*)

    Path of the Folder to which the Run is uploaded. If the provided path does not start with '/', `/<current-user>/` is prepended to it.

* **make_folder** (*bool*)

    If True and Folder with path `folder` does not exist, make the Folder and parent Folders as needed.

* **conflict_strategy** (*str*)

    Strategy adopted when a Run with the same name as the Run to be uploaded already exists in the Folder, must be 'skip', 'error', 'new' or 'replace'. If 'skip', skip the upload; if 'error', error out; if 'new', upload with the alternative name of Run; if 'replace', delete the existing Run and upload.
