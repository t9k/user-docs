---
title: t9k.em.load_artifact
---

# t9k.em.load_artifact

```python
load_artifact(path: str) ‑> t9k.em.artifact.Artifact
```

Loads an Artifact from local or server.

This function will first search for the corresponding local directory, followed by remote path. If the path is not found in either location, raise a `RuntimeError`.

In the case of the remote path, if the provided path does not start with '/', `/<current-user>/` is prepended to it.

## Examples

Load by local path:
```python
em.load_artifact(path=
    '.em/artifacts/tensorboard_logs_220823_194728_4e48t2')
```

Load by remote path:
```python
em.load_artifact(path='/user/path/to/tensorboard_logs')
```

## Args

* **path** (*str*)

    Local directory of the Artifact, or path of the Artifact in server.

## Returns

An Artifact instance loaded.
