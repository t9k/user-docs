---
title: t9k.em.load_run
---

# t9k.em.load_run

```python
load_run(path: str, auto_upload: bool = False, folder: str = 'default', make_folder: bool = False, conflict_strategy: str = 'new') ‑> t9k.em.run.Run
```

Loads a Run from local or server.

This function will first search for the corresponding local path, followed by remote path. If the path is not found in either location, raise a `RuntimeError`.

In the case of the remote path, if the provided path does not start with '/', `/<current-user>/` is prepended to it.

## Examples

Load by local path:
```python
em.load_run(path='.em/runs/cnn_keras_220823_194728_4e48t2')
```

Load by remote path:
```python
em.load_run(path='/user/path/to/cnn_keras')
```

## Args

* **path** (*str*)

    Local directory of the Run, or path of the Run in server.

* **auto_upload** (*bool*)

    Whether to upload the Run and its data automatically and asynchronously. If False, all of the following args will not be used.

* **folder** (*str*)

    Path of the Folder to which the Run is uploaded. If the provided path does not start with '/', `/<current-user>/` is prepended to it. If `auto_upload` is False, this arg will not be used.

* **make_folder** (*bool*)

    If True and Folder with path `folder` does not exist, make the Folder and parent Folders as needed. If `auto_upload` is False, this arg will not be used.

* **conflict_strategy** (*str*)

    Strategy adopted when a Run with the same name as the Run to be uploaded already exists in the Folder, must be 'skip', 'error', 'new' or 'replace'. If 'skip', skip the upload; if 'error', error out; if 'new', upload with the alternative name of Run; if 'replace', delete the existing Run and upload. If `auto_upload` is False, this arg will not be used.

## Returns

A Run instance loaded.
